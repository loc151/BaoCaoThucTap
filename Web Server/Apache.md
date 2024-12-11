# Apache HTTP Server:
## Khái niệm:
- Apache là phần mềm *web server* mã nguồn mở miễn phí
- **Web server**: là công cụ giúp cho server (máy chủ) và client (máy khách) có thể giao tiếp với nhau
## Đặc điểm:
**1. Mã nguồn mở**: cho phép người dùng tự do tải về, sử dụng, và chỉnh sửa mã nguồn theo nhu cầu. <p>
**2. Đa nền tảng**: Chạy trên nhiều hệ điều hành khác nhau, bao gồm Linux, Windows và macOS <p>
**3. Module linh hoạt**: Hỗ trợ nhiều module mở rộng, cho phép người dùng thêm các tính năng như bảo mật, cân bằng tải, và hỗ trợ các ngôn ngữ lập trình khác nhau. <p>
**4. Hiệu suất cao**: Apache được tối ưu hóa để xử lý nhiều yêu cầu đồng thời, giúp cải thiện hiệu suất và độ tin cậy của web server. <p>
**5. Hỗ trợ đa giao thức**: hỗ trợ nhiều giao thức truyền tải dữ liệu như HTTP, HTTPS, và FTP <p>

## Yêu cầu:
- Một máy ảo hệ điều hành Ubuntu 22.04
- User **root** hoặc user có quyền sudo
- Kích hoạt tường lửa

## Cài đặt:
### Bước 1: Cài đặt web server Apache:
```
sudo apt update
sudo apt install apache2
```

### Bước 2: Thay đỏi cài đặt tường lửa: 
- Trước khi kiểm tra Apache, cần chỉnh sửa một số cấu hình tường lửa để cho phép truy cập từ bên ngoài vào port mặc định của web:
```
sudo ufw app list
```
- Danh sách output: <p>
![image](https://github.com/user-attachments/assets/139df06f-2728-4608-88e5-a1174369437f)

- Trong đó:
  - **Apache**: chỉ mở port 80 (lưu lượng không được mã hoá)
  - **Apache Full**: Mở port 80 và 443 (lưu lượng được mã hoá bằng TLS/SSL)
  - **Apache Secure**: Chỉ mở port 443 (được mã hoá bằng TLS/SSL)
- Vì chưa cấu hình SSL nên chỉ cần cho phép lưu lượng trên port 80:
```
sudo ufw allow 'Apache'
```
![image](https://github.com/user-attachments/assets/736916cd-fabb-479c-b973-039f297b7eb2)

### Bước 3: Kiểm tra web server:
- Kiểm tra trạng thái của dịch vụ:
```
sudo systemctl status apache2
```
![image](https://github.com/user-attachments/assets/c6e33b18-ee1f-474e-b933-6251e2f37e54)

- Truy cập landing page của Apache qua địa chỉ IP của server (192.16.2.100). Nếu hiển thị như này tức là Apache hoạt động bình thường:
![image](https://github.com/user-attachments/assets/e0647013-435e-4b59-8424-2464182fa782)

### Bước 4: Quản lý tiến trình Apache: 
**1. Dừng web server**: 
```
sudo systemctl stop apache2
```

**2. Khởi động web server**:
```
sudo systemctl start apache2
```

**3. Restart dịch vụ**:
```
sudo systemctl restart apache2
```

**4. Reload dịch vụ (thay đổi cấu hình mà không cần ngắt kết nối)**:
```
sudo systemctl reload apache2
```

**5. Vô hiệu hoá tính năng tự khỏi động Apache mỗi khi server boot**:
```
sudo systemctl disable apache2
```

**6. Bật lại tính năng ở phần 5**:
```
sudo systemctl enable apache2
```

### Bước 5: Thiết lập Virtual Host: 
- Khi sử dụng web server Apache, có thể sử dụng các virtual host (tương tự như các server block – khối server – trong Nginx) để đóng gói các chi tiết cấu hình và lưu trữ nhiều miền từ một server.
- Apache trên Ubuntu 22.04 đã enable sẵn một server block, được cấu hình để cung cấp tài liệu từ thư mục `/var/www/html`. Nếu chỉ host một trang thì không có vấn đề gì, nhưng đối với số lượng trang lớn thì sẽ khó quản lý. Thay vì chỉnh sửa trực tiếp `/var/www/html`, nên tạo một cấu trúc thư mục trong `/var/www` cho trang **anhldl**, để nguyên `/var/www/html` làm thư mục mặc định để cung cấp nếu request của client không khớp với bất kỳ trang nào
- Tạo thư mục mới trong thư mục `/var/www`:
```
sudo mkdir /var/www/anhldl
```
- Gán quyền truy cập thư mục bằng biến môi trường `$USER`:
```
sudo chown -R $USER:$USER /var/www/anhldl
```
- Quyền truy cập các root của web nên chính xác:
```
sudo chmod -R 755 /var/www/anhldl
```
- Tạo 1 trang mẫu `index.html` bằng 1 text editor bất kỳ:
```
sudo nano /var/www/anhldl/index.html
```
- Trong file `index.html`, thêm đoạn HTML sau:
```shell
<html>
    <head>
        <title>Welcome to anhldl!</title>
    </head>
    <body>
        <h1>Success!  The anhldl virtual host is working!</h1>
    </body>
</html>
```
- Tạo 1 file virtual host với các directive chính xác, giúp cho Apache có thể cung cấp nội dung:
```
sudo nano /etc/apache2/sites-available/anhldl.conf
```
- Thêm đoạn sau vào file và lưu:
```shell
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    ServerName anhldl.com
    ServerAlias www.anhldl.com
    DocumentRoot /var/www/anhldl
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
- Trong đó:
  - **DocumentRoot**: được cập nhật thành thư mục mới
  - **ServerAdmin**: Đặt thành địa chỉ email và admin của trang
  - **ServerName**: Thiết lập domain cơ sở khớp với định nghĩa virtual host
  - **ServerAlias**: Định nghĩa các tên khác nên được khớp như những tên cơ sở
- Chạy tệp tin vừa cấu hình:
```
sudo a2ensite anhldl.conf
```
- Vô hiệu hoá trang mặc định:
```
sudo a2dissite 000-default.conf
```
- Kiểm tra lỗi cấu hình, nếu output là **Syntax OK** tức không có lỗi gì:
```
sudo apache2ctl configtest
```
- Khởi động lại dịch vụ Apache để áp dụng các thay đổi:
```
sudo systemctl restart apache2
```

## Kết quả: Truy cập địa chỉ IP của server (192.16.2.100). Nếu kết quả hiển thị như ảnh tức là đã cấu hình thành công:
![image](https://github.com/user-attachments/assets/141972e9-e610-4efc-b98d-8cf034a21e72)
