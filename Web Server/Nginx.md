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
sudo apt install nginx -y
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
![image](https://github.com/user-attachments/assets/996d594b-f4c6-4da1-8c58-3838b26816f6)

- Cho phép truy cập phần mềm HTTP:
```
sudo ufw allow 'Nginx HTTP'
```
- Kiểm tra lại với lệnh sau:
```
sudo ufw status
```
![image](https://github.com/user-attachments/assets/aad1dd47-e68c-45b0-bdc2-69b1cfa37517)

### Bước 3: Kiểm tra web server
- Đảm bảo rằng dịch vụ đang chạy:
```
systemctl status nginx
```
![image](https://github.com/user-attachments/assets/d57a4c80-d6a4-426a-87fd-119cd46dfcf2)
- Nhập địa chỉ IP của server, nếu trang web hiện ra như này, tức web server hoạt động bình thường:
![image](https://github.com/user-attachments/assets/bc7c7aae-e2fb-4ae3-b90d-482f628319c4)

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
- Tạo thư mục `/var/www/my_domain.com/html` để chứa mã nguồn website:
```
mkdir -p /var/www/my_domain.com/html
```
- Đặt quyền và chủ sỡ hữu cho thư mục:
```
sudo chown –R $USER:$USER /var/www/my_domain.com
sudo chmod –R 755 /var/www/my_domain.com
```
- Tạo một file `index.html` tại `/var/www/my_domain.com/html/` chứa nội dung sau:
```shell
<html>
    <head>
        <title>Welcome to my_domain!</title>
    </head>
    <body>
        <h1>Success!  The my_domain virtual host is working!</h1>
    </body>
</html>
```
- Tạo file cấu hình nginx cho tên miền my_domain.com:
```
sudo nano /etc/nginx/sites-available/my_domain.com
```
- Ghi nội dung sau vào tệp cấu hình nginx:
```shell
server {
        listen 80;
        listen [::]:80;

        root /var/www/my_domain.com/html;
        index index.html index.htm index.nginx-debian.html;

        server_name my_domain.com www.my_domain.com;

        location / {
                try_files $uri $uri/ =404;
        }
}
```
- Tạo một symbolic link để liên kết file `/etc/nginx/sites-available/my_domain.com` sang thư mục `/etc/nginx/sites-enabled/`. Nginx sẽ đọc các file cấu hình tại thư mục `/etc/nginx/sites-enabled/` mỗi khi khởi động:
```
sudo ln -s /etc/nginx/sites-available/my_domain.com /etc/nginx/sites-enabled/
```
- Kiểm tra cấu hình với lệnh:
```
sudo nginx –t
```
- Nếu kết quả hiển thị như bên dưới tức là đã cấu hình chính xác:

- Khởi động lại web server:
```
sudo systemctl restart nginx
```

