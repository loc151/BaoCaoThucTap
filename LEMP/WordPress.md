# Triển khai Wordpress với LEMP trên Ubuntu 22.04
## Yêu cầu:
- Đã cài đặt thành công LEMP (Linux, Nginx, MySQL và PHP) trên máy chủ hệ điều hành Ubuntu 22.04

## Cài đặt Wordpress:
### 1. Tạo cơ sở dữ liệu cho WordPress:
- Đăng nhập vào MySQL/MariaDB:
```
sudo mysql -u root -p
```
- Tạo cơ sở dữ liệu và người dùng cho WordPress:
```sql
CREATE DATABASE wordpress;
CREATE USER 'wordpressuser'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON wordpress.* TO 'wordpressuser'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```
![image](https://github.com/user-attachments/assets/fde34bc4-35f5-42f9-9058-60c5dd18c3e6)

### 2. Tải xuống và cài đặt WordPress:
- Chuyển đến thư mục **web root**:
```
cd /var/www/html
```
- Tải xuống **WordPress**:
```
sudo wget https://wordpress.org/latest.tar.gz
sudo tar -xvzf latest.tar.gz
sudo mv wordpress/* .
sudo rm -rf wordpress latest.tar.gz
```
- Thiết lập quyền sở hữu và truy cập:
```
sudo chown -R www-data:www-data /var/www/html
sudo chmod -R 755 /var/www/html
```

### 3. Cấu hình WordPress:
- Tạo tệp cấu hình và chỉnh sửa tệp **wp-config.php**:
```
sudo cp wp-config-sample.php wp-config.php
sudo nano wp-config.php
```
- Chỉnh sửa các dòng sau để kết nối với cơ sở dữ liệu:
```
define('DB_NAME', 'wordpress');
define('DB_USER', 'wordpressuser');
define('DB_PASSWORD', 'password');
```
![image](https://github.com/user-attachments/assets/ef8f3087-67b4-4e85-987e-435ae6854a07)

- Khởi động lại dịch vụ Nginx để xác định các cấu hình:
```
sudo systemctl restart nginx
```

## Kết quả:
- Mở trình duyệt và truy cập `http://your_domain_or_IP` để hoàn tất quá trình cài đặt WordPress thông qua giao diện web
![image](https://github.com/user-attachments/assets/7211445a-5654-44f4-bab1-85a6da1745dc)

- Giao diện sau khi đăng nhập:
![image](https://github.com/user-attachments/assets/c527ac37-066d-4b64-91db-ee8ebc19d0e0)
