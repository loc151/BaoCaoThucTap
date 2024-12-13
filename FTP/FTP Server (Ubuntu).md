# Cài đặt FTP Server trên Ubuntu 22.04

## Yêu cầu:
- Một máy ảo sử dụng hệ điều hành Ubuntu 22.04
- Cài đặt WinSCP trên máy sử dụng hệ điều hành Windows

## Khái niệm:
### 1. FTP Server:
- **FTP (File Transfer Protocol) server** là một máy chủ sử dụng giao thức FTP để truyền tải tệp giữa các máy tính qua mạng.
- FTP server cho phép người dùng tải lên (upload) và tải xuống (download) các tệp từ máy chủ, cũng như quản lý các tệp và thư mục trên máy chủ từ xa.

### 2. WinSCP: 
- **WinSCP (Windows Secure Copy)** là một tiện ích SFTP và FTP client miễn phí, mã nguồn mở dành cho hệ điều hành Windows.
- Tiện ích này giúp người dùng truyền tải file một cách an toàn giữa máy tính của bạn và máy tính từ xa

## Cài đặt:
### 1. Cập nhật Ubuntu:
```shell
sudo apt update && sudo apt upgrade
```

### 2. Cài đặt VSFTPD:
```shell
sudo apt install vsftpd
```

### 3. Kiểm tra trạng thái của VSFTPD:
```
systemctl status vsftpd --no-pager -l
```
- Trong đó:
  - **--no-pager**: Ngăn không cho đầu ra của lệnh được chuyển qua trình phân trang như `less` hoặc `more`
  - **-l**: Hiển thị đầu ra đầy đủ mà không cắt bớt các dòng dài, giúp xem toàn bộ thông tin mà không mất dữ liệu quan trọng
 
![image](https://github.com/user-attachments/assets/d280da13-be4e-4732-b3f3-07ef6a333ba7)

### 4. Tạo người dùng cho FTP:
- Tạo 2 user không có quyền truy cập `sudo` và chúng ta chỉ sử dụng nó để truy cập vào một thư mục cụ thể trong thư mục chính của nó để FTP đọc và ghi tệp.
```
sudo adduser ftpuser1
sudo adduser ftpuser2
```
![image](https://github.com/user-attachments/assets/afd12b47-2f34-40a5-9eb4-12df686ff84d)
- Làm tương tự với user **ftpuser2**

### 5. Tạo thư mục FTP:
- Tạo thư mục cho user **ftpuser1**:
```
sudo mkdir /home/ftpuser1/ftp
```

- Cấu hình quyền sở hữu:
```
sudo chown nobody:nogroup /home/ftpuser1/ftp
```

- Xóa quyền có thể ghi của thư mục FTP gốc:
```
sudo chmod a-w /home/ftpuser1/ftp
```

- Tạo một thư mục để tải lên các tệp sẽ chứa các tệp:
```
sudo mkdir /home/ftpuser1/ftp/upload1
```

- Cấp quyền sở hữu thư mục tải lên đã tạo cho user FTP:
```
sudo chown ftpuser1:ftpuser1 /home/ftpuser1/ftp/upload
```

-  Kiểm tra, tạo tệp demo bên trong thư mục tải lên:
```
echo "My FTP Server" | sudo tee /home/ftpuser1/ftp/upload/demo.txt
```

- Kiểm tra quyền thư mục FTP:
```
sudo ls -la /home/ftpuser1/ftp
```

![image](https://github.com/user-attachments/assets/6f3ab636-9fae-48c5-b717-6e95f0014b6e)

> Làm các bước tương tự với user `ftpuser2`

### 6. Cấu hình VSFTPD:
- Truy cập file `/etc/vsftpd.conf` để cấu hình:
```
sudo nano /etc/vsftpd.conf
```

- Kích hoạt người dùng ẩn danh, khi câu lệnh này được bật, người dùng có thể đăng nhập vào máy chủ FTP ma không cần tên người dùng và mật khẩu: `anonymous_enable=YES`
- Kích hoạt người dùng FTP local: `local_enable=YES`
- Cho phép tải file và thư mục lên FTP server: `write_enable=YES`
- Hạn chế người dùng local truy cập đến thư mục **home** của họ: `chroot_local_user=YES`
- Thêm các dòng sau để khi người dùng đăng nhập vào FTP server, nó sẽ định tuyến đến thư mục được truy cập:
```
user_sub_token=$USER
local_root=/home/$USER/ftp
```
- Thêm port passive:
```
pasv_min_port=30000
pasv_max_port=31000
```
- Cấu hình **VSFTPD** chỉ cho phép user truy cập vào máy chủ FTP nằm trong danh sách chứ không phải bất kỳ ai ngẫu nhiên:
```
userlist_enable=YES
userlist_file=/etc/vsftpd.userlist
userlist_deny=NO
```
![image](https://github.com/user-attachments/assets/9fbca153-efc0-4d94-96d1-f222e9aef146)

### 7. Cấu hình firewall cho phép port FTP:
```
sudo ufw allow 20,21,990/tcp
sudo ufw allow 30000:31000/tcp
```
- **Port 20**: Sử dụng cho dữ liệu FTP
- **Port 21**: Sử dụng để điều khiển FTP
- **Port 990**: Sử dụng cho FTPS
- **Port 30000-31000**: Sử dụng cho các kết nối dữ liệu trong chế độ Passive FTP

### 8. Thêm user vào danh sách không bị chặn:
```shell
echo "ftpuser1" | sudo tee -a /etc/vsftpd.userlist
echo "ftpuser2" | sudo tee -a /etc/vsftpd.userlist
```

### 9. Khởi động lại dịch vụ VSFTPD:
```
sudo systemctl restart vsftpd
```

## Kết quả:
- Kiểm tra kết nối FTP Server: Sử dụng **WinSCP**
![image](https://github.com/user-attachments/assets/47279b5e-33ce-4a42-9cd8-7e41a0293be2)

- Sau khi đăng nhập thành công, user `ftpuser1` chỉ có thể vào thư mục chỉ định local_root `/home/ftpuser1/ftp`, user `ftpuser2` chỉ có thể vào thư mục chỉ định local_root `/home/ftpuser2/ftp`:
![image](https://github.com/user-attachments/assets/f7f26d22-2d3e-46bd-9047-d27fd8473ff6)
![image](https://github.com/user-attachments/assets/17eee60e-888c-439d-a947-df37b3d0676c)
