# Cài đặt VM trên Ubuntu

## A. Hướng dẫn thêm file ISO từ USB vào Ubuntu để cài đặt máy ảo

1. **Cắm USB vào máy tính**: Đảm bảo server đã nhận được USB khi cắm USB vào cổng.
2. **Xác định tên thiết bị USB**:
- Dùng lệnh sau để liệt kê các thiết bị USB và xác nhận xem server đã nhận USB:

![image](https://github.com/user-attachments/assets/4679f5b5-1f7c-49a3-b020-4557b77a9d68)

- Trường hợp này đang dùng USB của Kingston, và server đã nhận diện được USB này

3. **Mount USB**
- Xác định tên thiết bị USB: nhập lệnh `lsblk`:

![image](https://github.com/user-attachments/assets/fc5cb1a9-318b-4a43-b012-edc4a264cdec)

Lúc này, thiết bị USB xuất hiện với tên **sda1**

- Tạo 1 thư mục để mount USB:
```
sudo mkdir /mnt/usb
```

- Mount USB và thư mục này:
```
sudo mount /dev/sda1 /mnt/usb
```

- Kiểm tra xem các file ISO đã hiển thị hay chưa:

![image](https://github.com/user-attachments/assets/6b5903d0-a438-4ea3-bec3-d623b2f412d6)

- Sao chép file ISO:
```
sudo cp /mnt/usb/yourfile.iso /home/yourusername/
```

Thay `yourfile.iso` bằng tên file ISO và `yourusername` bằng tên người dùng.

![image](https://github.com/user-attachments/assets/0d2c51fb-eafc-4438-aebe-8db2a6f00195)

- Kiểm tra xem file ISO đã hiển thị trong thư mục đích:

![image](https://github.com/user-attachments/assets/670da93b-a3d2-4999-be10-8ae3b5279fcd)

## B. Cài đặt VM trên Ubuntu: 

## Bước 1: Mở Virt-Manager
1. Mở terminal và chạy lệnh sau để khởi động `virt-manager`:
    ```bash
    sudo virt-manager
    ```
2. Giao diện `virt-manager` sẽ được mở ra.

![image](https://github.com/user-attachments/assets/17ab85a6-5f2b-40b8-b9c3-3988973a8341)

## Bước 2: Tạo máy ảo mới
1. Trên giao diện `virt-manager`, nhấp vào File chọn **Create a new virtual machine** để bắt đầu tạo máy ảo mới.
2. **Chọn phương thức cài đặt**:
    - Chọn **Local install media (ISO image or CDROM)** nếu có file ISO.
    - Nhấn **Forward**.

![image](https://github.com/user-attachments/assets/2d624d2a-6b51-45e6-acc0-8bac9bc6e48e)

## Bước 3: Chọn file ISO cài đặt
1. Nhấp vào **Browse** để chọn file ISO của Ubuntu 20.04 (hoặc bất kỳ hệ điều hành nào muốn cài đặt).
2. Sau khi chọn file ISO, nhấn **Forward**.
   
![image](https://github.com/user-attachments/assets/17c555b6-9b72-4e79-b09b-6a198202189e)

## Bước 4: Chọn cấu hình phần cứng
1. **Bộ nhớ (RAM)**: Nhập 4096MB (4GB).
2. **CPU**: Chọn 4 CPU cho máy ảo.
3. Nhấn **Forward**.
   
![image](https://github.com/user-attachments/assets/70863b97-d8bc-4f35-bdc8-720277b39abd)
 
## Bước 5: Cấu hình ổ đĩa
1. **Create a disk image for the virtual machine**: Chọn tạo ổ đĩa mới và chọn dung lượng lưu trữ theo nhu cầu.
2. Nhấn **Forward**.
   
![image](https://github.com/user-attachments/assets/16c38fcd-bd61-4437-81a6-b92595af5c11)


## Bước 6: Đặt tên và xác nhận cấu hình
1. **Name**: Đặt tên cho máy ảo
2. Xác định card mạng muốn cấp cho VM
3. Đảm bảo rằng tất cả cấu hình đã được thiết lập đúng, sau đó nhấp **Finish** để hoàn tất quá trình tạo máy ảo.
   
![image](https://github.com/user-attachments/assets/99787bd8-412e-4648-9f54-14ed7edc35d0)

## Bước 7: Khởi động và cài đặt hệ điều hành
1. Sau khi máy ảo được tạo, nó sẽ tự động khởi động với file ISO mà bạn đã chọn. Bạn có thể tiến hành cài đặt Ubuntu như bình thường.
2. Chọn Begin Installation để tiến hành cài đặt VM
![image](https://github.com/user-attachments/assets/2dfec24d-3beb-41bd-ad46-dee45382fa77)

