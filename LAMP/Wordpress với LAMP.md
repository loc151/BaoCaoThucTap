# Triển khai Wordpress với LAMP trên Ubuntu 22.04 
## LAMP:
LAMP là viết tắt của Linux, Apache, MySQL và PHP. Nó là một chồng các ứng dụng hoạt động cùng nhau trên một máy chủ web để lưu trữ một trang web. Mỗi chương trình riêng lẻ phục vụ một mục đích khác nhau, được kết hợp lại để tạo thành một giải pháp máy chủ web linh hoạt.
- Trong LAMP, Linux đóng vai trò là hệ điều hành của máy chủ xử lý tất cả các lệnh trên máy
- Apache là một phần mềm máy chủ web quản lý các yêu cầu HTTP để cung cấp nội dung cho trang web
- MySQL là một hệ quản trị cơ sở dữ liệu có chức năng duy trì dữ liệu của người dùng trên máy chủ
- PHP là một ngôn ngữ lập kịch bản cho phép giao tiếp phía máy chủ

## Cài đặt LAMP:
### 1. Cập nhật kho lưu trữ và nâng cấp các gói:
```
sudo apt update && apt upgrade -y
```
### 2. Cài đặt các gói ứng dụng cần thiết (Apache, MySQL, PHP):
```
sudo apt install apache2 ghostscript libapache2-mod-php mysql-server php php-bcmath php-curl php-imagick php-intl php-json php-mbstring php-mysql php-xml php-zip -y
```
- Kiểm tra xem Apache có hoạt động hay chưa: truy cập `http://localhost` hoặc địa chỉ IP của máy chủ đã cài:
![image](https://github.com/user-attachments/assets/ad9d5571-8b74-4977-a8b4-9b8bf03600dc)

### 3. Cài đặt Wordpress:
- Tạo thư mục nơi sẽ lưu trữ các tệp wordpress:
```
sudo mkdir -p /var/www/html
```
- Thay đổi quyền sở hữu của thư mục thành người dùng `www-data`:
```
sudo chown www-data: /var/www/html
```
- Cuộn các tệp zip từ trang wordpress chính thức và giải nén chúng vào thư mục đã tạo:
```
curl https://wordpress.org/latest.tar.gz | sudo -u www-data tar zx -C /var/www/html
```
- Tạo file cấu hình wordpress tại thư mục sau:
```
sudo nano /etc/apache2/sites-available/wordpress.conf
```
- Thêm các dòng sau vào file cấu hình:
```shell
<VirtualHost *:80>
    DocumentRoot /var/www/html/wordpress
    <Directory /var/www/html/wordpress>
        Options FollowSymLinks
        AllowOverride Limit Options FileInfo
        DirectoryIndex index.php
        Require all granted
    </Directory>
    <Directory /var/www/html/wordpress/wp-content>
        Options FollowSymLinks
        Require all granted
    </Directory>
</VirtualHost>
```
- Bật trang web wordpress, tắt trang web Apache mặc định:
```
sudo a2ensite wordpress
sudo a2dissite 000-default
sudo a2enmod rewrite
sudo systemctl restart apache2
```

### 4. Tạo dữ liệu trên MySQL:
- Đăng nhập và tạo bảng dữ liệu:
```
sudo mysql -u root
CREATE DATABASE wordpress;
```
- Tạo username và password:
```
CREATE USER admin@localhost IDENTIFIED BY 'password';
```
- Cấp đặc quyền cho user vừa tạo:
```
GRANT ALL PRIVILEGES ON *.* TO admin@localhost;
FLUSH PRIVILEGES;
```
- Khởi động lại MySQL và xác minh trạng thái của dịch vụ:
```
sudo service mysql start
sudo systemctl status mysql
```
![image](https://github.com/user-attachments/assets/a69ed3f5-2f52-4bdc-8fe8-c69d2757baf5)
- Sao chép tệp cấu hình WordPress vừa giải nén:
```
sudo -u www-data cp /var/www/html/wordpress/wp-config-sample.php /var/www/html/wordpress/wp-config.php
```
- Truy cập file vừa sao chép và cấu hình:
```sql
> sudo nano /var/www/html/wordpress/wp-config.php
define('DB_NAME', 'wordpress');
define('DB_USER', 'admin');
define('DB_PASSWORD', 'password');
define('DB_HOST', 'localhost');
```
![image](https://github.com/user-attachments/assets/225de1a6-fb62-43f9-8cfb-f5fb00dd7ca9)

### 5. Cài đặt PHPmyAdmin:
- Cài đặt giao diện người dùng đồ họa (GUI) để dễ sử dụng:
```
sudo apt install phpmyadmin php-mbstring php-zip php-gd php-json php-curl -y
```
![image](https://github.com/user-attachments/assets/3d79a173-b864-4e39-bbb0-eea55817f273)

- Kích hoạt sửa đổi để củng cố trang web sau này và khởi động lại Apache:
```
sudo phpenmod mbstring
sudo a2enmod headers
sudo systemctl restart apache2
```

## Kết quả: Truy cập địa chỉ IP để cấu hình Wordpress:
![image](https://github.com/user-attachments/assets/096ddce9-cff0-498f-8b2b-9f5ad4344924)
![image](https://github.com/user-attachments/assets/8432e686-960c-438d-ab6c-8ac825275eea)
![image](https://github.com/user-attachments/assets/58661339-50ab-454f-809f-42568934ee17)
![image](https://github.com/user-attachments/assets/acd3fdcd-d69c-4908-b800-ee243fd6cee5)
![image](https://github.com/user-attachments/assets/b8768b51-09f2-49f7-a4b7-496a4fef9d60)
![image](https://github.com/user-attachments/assets/3fbd17b7-f590-4bad-a087-976c2cefb627)
![image](https://github.com/user-attachments/assets/bfb2626c-6e3f-48c2-b37a-6b268eab0b34)
![image](https://github.com/user-attachments/assets/dd70e8e6-72fe-47eb-a9f1-1bb394f6017b)

