# Swap memory
## 1. Khái niệm
- Swap Memory được sử dụng khi hệ thống quyết định rằng nó cần thêm bộ nhớ RAM cho quá trình hoạt động và bộ nhớ RAM hiện tại không còn đủ để sử dụng. Nếu điều đó xảy ra, các tài nguyên và dữ liệu tạm thời không hoạt động trên bộ nhớ RAM sẽ được di chuyển để lưu trữ vào không gian Swap để giải phóng bộ nhớ RAM và sử dụng cho việc khác
- Swap sẽ làm nhiệm vụ duy trì tất cả các hoạt động bình thường dù tốc độ chậm hơn thay vì phải dừng cả hệ thống khi đầy bộ nhớ RAM

## 2. Khi nào cần Swap memory
- Tối ưu hóa hệ thống bộ nhớ: Hệ thống sẽ di chuyển các tài nguyên và dữ liệu hiện không sử dụng trong bộ nhớ RAM đến Swap, điều này giúp hệ thống phục vụ cho các mục đích khác tốt hơn.
- Tránh các trường hợp không thể lường trước: Trong một số trường hợp không thể dự tính được bộ nhớ chương trình chuẩn bị chạy.
- Khi dùng một phần mềm yêu cầu hệ thống có hỗ trợ bộ nhớ Swap trong phần cài đặt.

## 3. Các loại không gian swap
- Linux swap có 2 dạng:
  - **Phân vùng swap (Swap Partition)**:
    - Là 1 phân vùng riêng biệt trên đĩa cứng được dành riêng cho việc swap
    - Phân vùng swap thường được tạo trong quá trình cài đặt hệ điều hành
  - **Tệp swap (Swap File)**:
    - Là 1 tệp trên hệ thống tệp có thể được sử dụng như không gian swap
    - Tệp swap có thể được tạo và cấu hình sao khi hệ điều hành đã được cài đặt 
- Để xem nó ở đâu dùng lệnh:

```sh
swapon -s 
or
free -h
free -m
```

- Trong đó:
  - `swapon -s`: Hiển thị thông tin về các phân vùng hoặc tệp swap đang được sử dụng trên hệ thống. Nó sẽ hiển thị 1 bảng với các cột thông tin sau. 
  ![image](https://github.com/user-attachments/assets/b620ae1e-3533-4f04-9928-70000377d7b5)
  - `Priority = -2`: Xác định thứ tự ưu tiên khi hệ thống sử dụng nhiều phân vùng swap. Giá trị -2 cho biết đây là 1 phân vùng swap có độ ưu tiên thấp
  - `free -m`: Hiển thị thông tin bộ nhớ dưới dạng MB
  - `free -h`: Hiển thị thông tin bộ nhớ với đơn vị phù hợp để hiển thị thông tin
  ![image](https://github.com/user-attachments/assets/40f3f8c2-99d9-43e4-b4eb-e5d78709123e)

## 4. Tạo file Swap
- Tạo Swap flie:
```sh
sudo dd if=/dev/zero of=/swapfile count=2048 bs=1MiB
```

- Trong đó:
  - `dd`: Lệnh sao chép và chuyển đổi dữ liệu
  - `if=/dev/zero`: Đặt tệp đầu vào là /dev/zero, 1 thiết bị đặc biệt tạo ra các byte có giá trị 0
  - `of=/swapfile`: Nơi lưu trữ dữ liệu được sao chép
  - `count = 2048`: Chỉ định số lượng khối dữ liệu cần sao chép
  - `bs = 1 MiB`: `Đặt kích thước của mỗi khối dữ liệu là 1 MiB`
- Kết quả: tạo ra 1 tệp swap có kích thước 2 GB chứa các byte có giá trị 0

![image](https://github.com/user-attachments/assets/db19ad51-5229-4476-9dab-6f4d5d04cdd5)


- Phân quyền cho `swapfile`. Chỉ có root user mới có quyền truy cập:
```sh
chmod 600 /swapfile
```

- Sử dụng `mkswap` để thiết lập file là file swap
```sh
mkswap /swapfile
```

![image](https://github.com/user-attachments/assets/b22a4649-1680-4695-aa93-e9dad4363520)

- Khởi động swap file
```sh
swapon /swapfile
```

- Mở file `/etc/fstab` và thêm vào cuối dòng sau để thiết lập swap khởi động cùng hệ điều hành:

```sh
sudo echo '/Swapfile swap swap defaults 0 0' | sudo tee -a /etc/fstab
```

## 5. Kiểm tra lại vùng Swap
```sh
swapon
```

![image](https://github.com/user-attachments/assets/ebfebc64-215e-483b-bcde-533c45b7f35e)

## 6. Giá trị Swappiness
- Tham số **Swappiness** cho biết thời điểm hệ thống sẽ chuyển từ bộ nhớ vật lý (RAM) sang bộ nhớ tạm **Swap**
- Giá trị từ Swappiness từ 0 - 100. Chỉ số này càng thấp thì máy linux sẽ tránh sử dụng swap file này, càng cao thì càng ưu tiên sử dụng.
- Ta có thê thay đổi giá trị này tại:
```sh
sudo nano /proc/sys/vm/swappiness
```

![image](https://github.com/user-attachments/assets/e50376e6-1507-47a5-9d3e-bd4d9c147619)

## 7. Xóa Swap file
- Để xóa File Swap, có thể deactive swap file:
```sh
swapoff -v /swapfile
```
- Xóa dòng khai báo swap tại file `/etc/fstab`
- Cuối cùng để xóa ta dùng lệnh `rm`
```sh
rm -rf /swapfile
```

## 8. Dung lượng cần thiết của bộ nhớ SWAP
- Nếu RAM ít hơn hoặc bằng 1Gb, thì nên sử dụng Swap có kích thước tối thiểu là bằng với lượng RAM
- Đối với RAM trên 1Gb, thì kích thước tối đa thường là gấp đôi lượng RAM. Nếu thiết lập kích thước của Swap quá lớn chính là đang lãng phí dung lượng ổ đĩa mặc dù Swap không được sử dụng
- Thời gian truy cập trên Swap sẽ chậm hơn so với trên RAM
