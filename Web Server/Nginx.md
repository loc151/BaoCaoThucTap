# Nginx
## 1. Khái niệm: 
- Nginx là web server mã nguồn mở, được tạo ra để đáp ứng nhu cầu về dịch vụ web, reverse proxy, caching, cân bằng tải, media streaming và nhiều tính năng khác. Nginx được thiết kế để có hiệu suất và độ ổn định tối đa.
- Ngoài phục vụ cho dịch vụ web (HTTP), Nginx còn được dùng làm reverse proxy cho email (IMAP, POP3, SMTP), đồng thời làm reverse proxy và cân bằng tải cho TCP và UDP.

## Chuẩn bị: 
- Hệ thống chạy Ubuntu 22.04
- Người dùng có quyền sudo hoặc quyền root
- Sử dụng command-line trên terminal
- Đã cài phần mềm curl

## Cài đặt: 
### Bước 1: Cài đặt Nginx:
- Cập nhật danh sách repository và chạy lệnh cài đặt Nginx:
```
sudo apt update
sudo install nginx
```
- Kiểm tra xem **Nginx** đã cài hay chưa:
```
nginx -v
```

### Bước 2: Cấu hình tường lửa:
- Kiểm tra `ufw` có đang hoạt động hay không:
```
sudo ufw app list
```
- Cho phép truy cập phần mềm HTTP:
```
sudo ufw allow 'Nginx HTTP'
```
- Kiểm tra lại với lệnh sau:
```
sudo ufw status
```

### Bước 3: Kiểm tra web server
- Đảm bảo rằng dịch vụ đang chạy:
```
systemctl status nginx
```
- Nhập địa chỉ IP của server, nếu trang web hiện ra như này, tức web server hoạt động bình thường:

### Bước 4: Quản lý dịch vụ Nginx:
**1. Khởi động web server**:
```
sudo systemctl start nginx
```
**2. Dừng web server:**
```
sudo systemctl stop nginx
```
**3. Khởi động lại web server**: 
```
sudo systemctl restart nginx
```
**4. Reload web server mà không mất kết nối**: Thường được sử dụng trong trường hợp bạn thay đổi cấu hình và muốn Nginx cập nhật cấu hình vừa thay đổi:
```
sudo systemctl reload nginx
```
**5. Bật khởi động cùng hệ thống**: giúp Nginx tự khởi động cùng hệ thống sau khi bạn khởi động lại máy chủ
```
sudo systemctl enable nginx
```
**6. Tắt khởi động cùng hệ thống**:
```
sudo systemctl disable nginx
```
**7. Kiểm tra tình trạng của web server**:
```
sudo systemctl status nginx
```

### Bước 5: Cấu hình server block (virtual host)
- Tạo thư mục /var/www/your_domain.com/html để chứa mã nguồn website
