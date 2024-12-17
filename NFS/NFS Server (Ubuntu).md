# Cài đặt NFS Server với máy Ubuntu 22.04 

## Yêu cầu: 
- Một máy Ubuntu 22.04 đóng vai trò là NFS Server (172.16.2.21)
- Một máy Ubuntu 22.04 đóng vai trò Client (172.16.2.197)
- User có quyền `sudo`
- Thiết lập tường lửa và mạng private

## Tại NFS Server:
### 1. Cài đặt gói dịch vụ NFS Server:
```
sudo apt update
sudo apt install nfs-kernel-server -y
```
### 2. Tạo các thư mục chia sẻ:
- **Lưu ý**: Superuser có thể thực hiện mọi hành động tại bất cứ vị trí nào trên hệ thống. Tuy nhiên các thư mục được mount bằng NFS không thuộc hệ thống mà chúng được mount. Do đó mặc định máy chủ NFS từ chối thực hiện các hoạt động được yêu cầu từ superuser. Điều này có nghĩa là superuser trên client không thể viết file với tư cách root, phân quyền sở hữu hoặc thực hiện bất cứ thao tác superuser nào khác trên NFS mount.
- **Trường hợp 1**: Xuất 1 mount đa dụng: sử dụng hành vi mặc định của NFS để giới hạn quyền tương tác của user root client khi tương tác với server host.
```
mkdir /var/nfs/share -p
```
- Do đang tạo thư mục với quyền sudo nên thư mục này thuộc sở hữu của root trên host:
```
ls -la /var/nfs/share
```
![image](https://github.com/user-attachments/assets/07a4b138-2182-4e72-ae33-7a5ab9757d33)
- NFS sẽ chuyển tất cả tác vụ của root trên client thành thông tin đăng nhập **nobody:nogroup** như một biện pháp bảo mật. Do đó, cần thay đổi quyền sở hữu thư mục để phù hợp với thông tin đăng nhập này:
```
sudo chown nobody:nogroup /var/nfs/share
```
- **Trường hợp 2**: Chia sẻ thư mục `/home`: Mục đích để chia sẻ các thư mục home của người dùng được lưu trữ trên host cho các client server. Đồng thời cho phép các administrator đáng tin cậy trên các client server truy cập dễ dàng để quản lý người dùng.

### 3. Cấu hình NFS Export:
- Vào file sau để cấu hình NFS:
```
sudo nano /etc/exports
```
- Tạo dòng cho mỗi thư mục dự định chia sẻ:
![image](https://github.com/user-attachments/assets/39fdd3e5-1174-4c0d-b0a8-bdcc1a4de171)
- Giải thích dòng lệnh:
  - `rw`: Tùy chọn này cho phép máy client đọc và ghi vào volume.
  - `sync`: Tùy chọn cho phép máy client ghi các thay đổi vào ổ đĩa trước khi phản hồi. Điều này giúp cho môi trường ổn định và nhất quán hơn nhờ việc phản ánh trạng thái thực tế của ổ đĩa từ xa. Tuy nhiên nó cũng làm giảm tốc độ hoạt động của các file.
  - `no_subtree_check`: Tùy chọn này ngăn chặn việc kiểm tra nhánh con (subtree checking), quá trình mà host phải thực hiện để xem file có còn thực sự khả dụng trong cây thư mục đã xuất không. Điều này có thể gây ra nhiều vấn đề khi file được đổi tên trong khi client đang mở nó. Tốt nhất trong các trường hợp, bạn nên tắt subtree checking.
  - `no_root_squash`: Mặc định, NFS dịch các yêu cầu từ root user từ xa thành non-privileged user trên server. Đây là một tính năng bảo mật để ngăn chặn tài khoản root trên client sử dụng file system của host như root. Lệnh no_root_squash sẽ vô hiệu hóa hành vi này cho một số phần chia sẻ.
- Sau khi đã cấu hình xong, khởi động lại máy chủ NFS:
```
sudo systemctl restart nfs-kernel-server
```

### 4. Cấu hình firewall: 
- Kiểm tra trạng thái firewall:
```
sudo ufw status
```
- Cho phép lưu lượng của NFS đi qua:
```
sudo ufw allow from client_ip to any port nfs
```
![image](https://github.com/user-attachments/assets/8172d413-ca54-4795-bc48-bc4deb39c9d1)
- Xác nhận xem rule đã được thêm hay chưa:
![image](https://github.com/user-attachments/assets/6a75e014-f2a0-4d40-99c0-689238bac457)

## Tại NFS Client:
### 1. Cài đặt gói dịch vụ NFS Client:
```
sudo apt update
sudo apt install nfs-common -y
```

### 2. Tạo mountpoint và mount thư mục trên Client: (Sau khi hoàn thành bước 4 của NFS Server)
- Tạo các thư mục:
```
sudo mkdir -p /nfs/share
sudo mkdir -p /nfs/home
```
- Mount file cần chia sẻ. Các lệnh này sẽ mount các file chia sẻ từ máy host đến các máy client
```
sudo mount host_ip:/var/nfs/share /nfs/share
sudo mount host_ip:/home /nfs/home
```
- Kiểm tra xem mount đã thành công chưa: `df -h`
![image](https://github.com/user-attachments/assets/83ff5264-ce63-484d-9ad2-6c79b9f26e92)

- Kiểm tra xem có bao nhiêu không gian đang được sử dụng với mỗi mountpoint: `du -sh /nfs/home`
![image](https://github.com/user-attachments/assets/eca6898c-c0f9-42a7-9306-8ea48c9a59a7)

### 3. Kiểm tra truy cập NFS:
- **Trường hợp 1**: Share dùng chung:
  - Ghi một file kiểm tra vào tệp `/var/nfs/share`:
  ```
  sudo touch /nfs/share/share.test
  ```
  - Kiểm tra quyền sở hữu file:
  ```
  ls -l /nfs/share/share.test
  ```
- Do mount volume này mà không thay đổi hành vi mặc định của NFS, đồng thời tạo file dưới dạng root user của client thông qua lệnh sudo, cho nên quyền sử hữu của file vẫn mặc định là nobody:nogroup. Client `superuser` sẽ không thể thực hiện các hoạt động quản trị tính năng thông thường như thay đổi chủ sở hữu file hoặc tạo thư mục mới cho một nhóm user trên folder share được mount bằng NFS này.
![image](https://github.com/user-attachments/assets/ba4e7aba-0514-48a6-acbe-6547c4ac3188)

- **Trường hợp 2**: Share thư mục `home`:
  - Để so sánh quyền hạn của share dùng chung và share thư mục home, tạo một file trong `/nfs/home` tương tự:
  ```
  sudo touch /nfs/home/home.test
  ```
  - Kiểm tra quyền sở hữu file:
  ```
  ls -l /nfs/home/home.test
  ```
- Tạo `home.test` với quyền root bằng cách sử dụng lệnh `sudo` tương tự như cách tạo file `share.test`. Tuy nhiên trong trường hợp này, `home.test` được sở hữu bởi root do bạn đã ghi đè lệnh hành vi mặc định khi chỉ định tùy chọn no_root_squash trên mount này. Điều này cho phép người dùng root trên client thao tác như root và giúp việc quản trị tài khoản người dùng thuận tiện hơn. Ta cũng không cần phải cấp quyền truy cập root cho người dùng trên host nữa.
![image](https://github.com/user-attachments/assets/da37dae0-ff12-4f74-a973-c7d183b9c441)

### 4. Mount các thư mục NFS từ xa khi khởi động: 
- Mount các thư mục NFS từ xa khi khởi động bằng cách thêm vào file `/etc/fstab` trên client:
- Thêm mỗi dòng sau cho mỗi folder share:
```
host_ip:/var/nfs/share      /nfs/share   nfs auto,nofail,noatime,nolock,intr,tcp,actimeo=1800 0 0
host_ip:/home               /nfs/home      nfs auto,nofail,noatime,nolock,intr,tcp,actimeo=1800 0 0
```

### 5. Ngắt kết nối NFS remote share:
- Sử dụng các lệnh sau để ngắt kết nối thư mục từ xa:
```
cd ~
sudo umount /nfs/home
sudo umount /nfs/share
```
- Kiểm tra lại xem đã ngắt kết nối chưa: `df -h`
![image](https://github.com/user-attachments/assets/037941b0-f922-46ad-bc4f-b0329a0fe5c3)
