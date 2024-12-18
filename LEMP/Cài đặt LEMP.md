# Cài đặt LEMP trên Ubuntu 22.04
## LEMP:
- Thuật ngữ LEMP là một nhóm phần mềm nguồn mở thường được cài đặt cùng nhau để cho phép máy chủ lưu trữ các trang web động và ứng dụng web. LEMP được viết tắt từ 4 thành phần của nó:
	+ L - Hệ điều hành Linux
	+ E - Nginx (Engine x) một máy chủ web
	+ M - Hệ quản trị cơ sở dữ liệu MySQL hoặc MariaDB
	+ P - Ngôn ngữ lập trình PHP

## Cài đặt LEMP:
### Cài đặt Nginx:
- **Bước 1**: Cập nhật danh sách các gói phần mềm có trên hệ thống:
```
sudo apt update && sudo apt upgrade -y
```
---
- **Bước 2**: Cài đặt Nginx:
```
sudo apt install nginx -y
```
- Sau khi cài đặt, sử dụng các lệnh sau để quản lý Nginx:
```
systemctl start nginx      // Khởi động dịch vụ Nginx
systemctl stop nginx       // Dừng dịch vụ Nginx
systemctl reload nginx     // Tải lại dịch vụ Nginx
systemctl restart nginx    // Khởi động lại dịch vụ Nginx
systemctl enable nginx     // Thiết lập Nginx khởi động cùng hệ thống
systemctl disable nginx    // Vô hiệu hoá Nginx khởi động cùng hệ thống
systemctl status nginx     // Xem trạng thái dịch vụ Nginx
```
![image](https://github.com/user-attachments/assets/3270aa38-9180-4d91-8788-7ca88f203b0e)
- Khởi động và kích hoạt Nginx để chạy cùng hệ thống:
```
sudo systemctl start nginx
sudo systemctl enable nginx
```
- Kiểm tra xem NginX có hoạt động được hay chưa: Điền IP của máy chủ cài Nginx:
![image](https://github.com/user-attachments/assets/e5e39dd0-9f74-4e20-9db7-9b4080d2651d)

- Bật tường lửa cho phép dịch vụ Nginx:
```
sudo ufw status
sudo ufw allow "Nginx Full"
```
---
- **Bước 3**: Cài đặt MariaDB:
```
sudo apt install mariadb-server -y
```
- Sau khi cài đặt hoàn tất, sử dụng các lệnh sau để quản lý **MariaDB**:
```
systemctl start mariadb      // Khởi động dịch vụ mariadb
systemctl stop mariadb       // Dừng dịch vụ mariadb
systemctl restart mariadb    // Khởi động lại dịch vụ mariadb
systemctl enable mariadb     // Thiết lập mariadb khởi động cùng hệ thống
systemctl disable mariadb    // Vô hiệu hoá mariadb khởi động cùng hệ thống
systemctl status mariadb     // Xem trạng thái dịch vụ mariadb
```
- Khởi động và kích hoạt MariaDB chạy cùng hệ thống:
```
sudo systemctl start mariadb
sudo systemctl enable mariadb
```
- Cấu hình bảo mật cho MariaDB:
```
sudo mysql_secure_installation
```
- Khi được nhắc nhập mật khẩu, ta có thể nhấn Enter để trống hoặc cập nhật mật khẩu mới
- Sau đó làm các bước để thiết lập mật khẩu. Cuối cùng, tập lệnh sẽ yêu cầu định cấu hình một số biện pháp bảo mật, bao gồm:
  - Xóa người dùng ẩn danh?
  - Không cho phép đăng nhập từ xa?
  - Xóa cơ sở dữ liệu thử nghiệm và truy cập vào nó?
  - Tải lại bảng đặc quyền ngay bây giờ
![image](https://github.com/user-attachments/assets/70d842b9-b5d1-491d-9d3b-c6f736fe7830)
![image](https://github.com/user-attachments/assets/06a3c1e2-d58b-425b-869a-a37fb1f37ebf)

- Kiểm tra xem MariaDB có hoạt động không:
```
mysql -u root -p
```
- Nhập mật khẩu. Nếu truy cập thành công tức hoạt động ổn định:
![image](https://github.com/user-attachments/assets/5f880252-a9aa-4a14-bb9c-849c86f5ecfa)
---

- **Bước 4**: Cài đặt PHP:
- Thêm kho lưu trữ **Ondřej PPA**:
```
sudo apt install software-properties-common
sudo add-apt-repository ppa:ondrej/php
sudo apt update
```
- Cài đặt từng phiên bản PHP:
   - **PHP 8.1**:  
     ```bash
     sudo apt-get install php8.1 php8.1-fpm -y
     sudo apt-get install php8.1-mysql php8.1-mbstring php8.1-xml php8.1-gd php8.1-curl -y
     ```  
   - **PHP 8.0**:  
     ```bash
     sudo apt-get install php8.0 php8.0-fpm
     sudo apt-get install php8.0-mysql php8.0-mbstring php8.0-xml php8.0-gd php8.0-curl
     ```  
   - **PHP 7.4**:  
     ```bash
     sudo apt-get install php7.4 php7.4-fpm
     sudo apt-get install php7.4-mysql php7.4-mbstring php7.4-xml php7.4-gd php7.4-curl
     ```  
   - **PHP 7.3**:  
     ```bash
     sudo apt-get install php7.3 php7.3-fpm
     sudo apt-get install php7.3-mysql php7.3-mbstring php7.3-xml php7.3-gd php7.3-curl
     ```  
   - **PHP 7.2**:  
     ```bash
     sudo apt-get install php7.2 php7.2-fpm
     sudo apt-get install php7.2-mysql php7.2-mbstring php7.2-xml php7.2-gd php7.2-curl
     ```  
   - **PHP 7.1**:  
     ```bash
     sudo apt-get install php7.1 php7.1-fpm
     sudo apt-get install php7.1-mysql php7.1-mbstring php7.1-xml php7.1-gd php7.1-curl
     ```  
   - **PHP 5.6**:  
     ```bash
     sudo apt-get install php5.6 php5.6-fpm
     sudo apt-get install php5.6-mysql php5.6-mbstring php5.6-xml php5.6-gd php5.6-curl
     ```
  - Kiểm tra phiên bản PHP đang hoạt động và trạng thái của dịch vụ:
  ```
  php -v
  systemctl status php8.1-fpm.service
  ```
  ![image](https://github.com/user-attachments/assets/8ba558a0-8e31-4aa4-b87d-a7ae2c98fa56)
---

- **Bước 5**: Cấu hình Nginx để sử dụng PHP:
```shell
> sudo nano /etc/nginx/sites-available/default

  location ~ \.php$ {
    fastcgi_pass unix:/run/php/php8.1-fpm.sock;
    fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    include fastcgi_params;
    include snippets/fastcgi-php.conf;
  }
```
![image](https://github.com/user-attachments/assets/0b214aab-97e9-49a6-8f6a-596e3e756a40)
- Kiểm tra cấu hình Nginx và khởi động lại dịch vụ:
```
sudo nginx -t
sudo systemctl restart nginx
```
![image](https://github.com/user-attachments/assets/909c00d3-87c7-422d-9e6c-d0c53ad8fabf)

---
- **Bước 6**: Kiểm tra LAMP: Tạo 1 tệp PHP và thêm nội dung sau để kiểm tra:
```
> sudo nano /var/www/html/info.php

<?php
phpinfo();
?>
```
---
## Kết quả: Mở trình duyệt và truy cập `http://your_domain_or_IP/info.php` để kiểm tra thông tin PHP
![image](https://github.com/user-attachments/assets/38764974-f044-4952-afc4-47c10daa76f4)
