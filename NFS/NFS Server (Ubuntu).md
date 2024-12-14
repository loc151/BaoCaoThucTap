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
