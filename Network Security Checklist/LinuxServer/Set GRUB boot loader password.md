## 11.  Set GRUB boot loader password:
- Để cài mật khẩu cho bộ nạp khởi động GRUB, ta dùng lệnh:
```
sudo grub-mkpasswd-pbkdf2
```
- Sau khi sử dụng lệnh trên, nhập mật khẩu và nhập lại để xác nhận, hệ thống sẽ trả ra mật khẩu dưới dạng hàm băm:
![image](https://github.com/user-attachments/assets/5edae5c2-926c-4eea-93ed-06c09e4a438e)

- Sao chép hàm băm mật khẩu vào clipboard. Điều này bao gồm phần bắt đầu bằng “grub”. Tiếp theo, chúng ta sẽ thực hiện một số chỉnh sửa đối với tệp cấu hình GRUB `/etc/grub.d/00_header`:
```
sudo nano /etc/grub.d/00_header
```

- Ở cuối tệp này, ta cần dán đoạn mã sau, đồng thời thay `linuxconfig` bằng tên tài khoản người dùng và thay `INSERT-HASH` bằng mã băm mật khẩu đã tạo trước đó.
```
cat << EOF
set superusers="linuxconfig"
password_pbkdf2 linuxconfig INSERT-HASH
EOF
```

- Sau khi thực hiện thay đổi từ bước trước, ta có thể thoát và lưu các thay đổi của mình vào tệp cấu hình GRUB. Sau đó, thực hiện lệnh update-grub với quyền root để cài đặt mật khẩu GRUB có hiệu lực.
```
sudo update-grub
```
- Khởi động lại hệ thống.

## 12. Disable interactive hotkey startup at boot:
- Để tắt phím tắt tương tác khi khởi động trong Linux, ta chỉnh sửa file cấu hình liên quan
- Mở file sau:
```
sudo nano /etc/sysconfig/init
```
- Tìm dòng lệnh bắt đầu bằng `PROMPT`. Nếu nó không tồn tại, ta thêm lệnh đó vào:
```
PROMPT=no
```
- Giải thích: Thiết lập này sẽ vô hiệu hoá lời nhắc khởi động tương tác, ngăn người dùng nhấn phím `I` trong quá trình khởi động để vào chế độ tương tác. Điều này giúp bảo mật quá trình khởi động bằng cách đảm bảo các dịch vụ được cấu hình sẽ khởi động mà không cần can thiệp thủ công.
- Lưu cấu hình và đóng file.
- Khởi động lại hệ thống để áp dụng các thay đổi

## 13. Enable auditd to check for read/write events: 
- `Auditd`: là công cụ mạnh mẽ giúp theo dõi và ghi lại các sự kiện liên quan đến bảo mật trên hệ thống.
### 13.1. Cài đặt **auditd**:
```
sudo apt-get install auditd audispd-plugins
```
![image](https://github.com/user-attachments/assets/cdd9a6a9-0ee5-492e-9bd6-b00a05223abe)

### 13.2. Cấu hình **auditd**:
- Mở file cấu hình:
```
sudo nano /etc/audit/auditd.conf
```
- Thêm các quy tắc để thực hiện theo dõi sự kiện đọc/ghi. Ví dụ, để theo dõi tất cả các lệnh `execve` (thực thi chương trình)
```
-a always,exit -F arch=b64 -S execve
-a always,exit -F arch=b32 -S execve
```
![image](https://github.com/user-attachments/assets/e0c900da-a166-4b83-b4ba-f7a052d31bff)

- Khởi động lại dịch vụ `auditd`
```
sudo service auditd restart
```
### 13.3. Kiểm tra các sự kiện:
- Sử dụng lệnh `ausearch` để tìm kiếm các sự kiện trong log
```
ausearch -m execve
```
### 13.4. Tạo báo cáo: 
- Sử dụng lệnh `aureport` để tạo báo cáo từ các log đã ghi lại:
```
aureport -x --summary
```

## 14. Secure any Apache servers:
### 14.1. Apache web server:
- **Apache** là một phần mềm web server mã nguồn mở miễn phí.
- Tên đầy đủ của nó là Apache HTTP Server.
- Apache giúp phục vụ các trang web và ứng dụng web thông qua giao thức HTTP và HTTPS
### 14.2. Cài đặt Apache:
- Cập nhật hệ thống: Chạy lệnh sau để cập nhật danh sách gói:
```
sudo apt update
```
- Cài đặt Apache:
```
sudo apt install apache2
```
- Kiểm tra trạng thái Apache: Nếu Apache đang chạy, trạng thái hiển thị là "active(running)"
```
sudo systemctl status apache2
```
![image](https://github.com/user-attachments/assets/cf481679-0427-4313-8539-935bfe746630)

- Cấu hình tường lửa: Nếu đang sử dụng UFW, cần cho phép lưu lượng HTTP và HTTPS:
```
sudo ufw allow 'Apache'
sudo ufw allow 'Apache Full'
```
- Kiểm tra cài đặt: Mở trình duyệt và nhập địa chỉ IP của máy chủ hoặc `localhost`. Nếu Apache được cài đặt thành công, ta sẽ thấy trang chào mừng mặc định của Apache
![image](https://github.com/user-attachments/assets/5d9bd8c0-a6c6-44d7-b4c5-03ee3ddd9e29)

## Cấu hình bảo mật cho Apache servers:
### 14.3. Ẩn thông tin phiên bản và hệ điều hành:
- Mở file cấu hình Apache, thêm và chỉnh sửa các dòng sau:
  - Ubuntu/Debian: `/etc/apache2/apache2.conf`
  - CentOS/Fedora: `/etc/apache2/httpd.conf`
    
```
ServerSignature Off
ServerTokens Prod
```
- Khởi động lại *Apache*:
```
sudo systemctl restart apache2    # Ubuntu/Debian
sudo systemctl restart httpd      # CentOS/Fedora
```

### 14.4. Vô hiệu hoá danh sách thư mục: 
- Đảm bảo rằng Apache không hiển thị danh sách thư mục nếu không có file index
- Thêm hoặc chỉnh sửa trong file cấu hình
```shell
<Directory /var/www/html>
    Options -Indexes
</Directory>
```

### 14.5. Cập nhật Apache thường xuyên:
- Đảm bảo luôn sử dụng phiên bản mới nhất của Apache để bảo vệ khỏi các lỗ hổng bảo mật:
```
sudo apt update && sudo apt upgrade apache2  # Ubuntu/Debian
sudo yum update httpd                        # CentOS/Fedora
```

### 14.6. Sử dụng mod_security và mod_evasive: 
- Cài đặt và cấu hình các module này để bảo vệ chống lại các cuộc tấn công DoS và các lỗ hổng bảo mật khác:
```
sudo apt install libapache2-mod-security2 libapache2-mod-evasive  # Ubuntu/Debian
sudo yum install mod_security mod_evasive                         # CentOS/Fedora
```

### 14.7. Hạn chế quyền truy cập:
- Chỉ cho phép truy cập vào các thư mục cần thiết và hạn chế truy cập vào các file nhạy cảm:
```shell
<Directory /var/www/html>
    AllowOverride None
    Require all granted
</Directory>
<Directory /var/www/html/private>
    Require all denied
</Directory>
```

### 14.8. Sử dụng HTTPS: 
- Cài đặt và cấu hình chứng chỉ SSL để mã hoá lưu lượng truy cập giữa máy chủ và người dùng:
```
sudo apt install certbot python3-certbot-apache  # Ubuntu/Debian
sudo yum install certbot python3-certbot-apache  # CentOS/Fedora
sudo certbot --apache
```

### 14.9. Giới hạn kích thước yêu cầu: 
- Đặt giới hạn kích thước yêu cầu để ngăn chặn các cuộc tấn công từ chối dịch vụ:
```
LimitRequestBody 10485760  # Giới hạn kích thước yêu cầu là 10MB
```

## 15. Install and configure UFW:
- UFW (Uncomplicated Firewall): là 1 công cụ quản lý tường lửa đơn giản trên Linux
- UFW cung cấp 1 giao diện dòng lệnh dễ sử dụng để quản lý các quy tắc tường lửa, giúp đơn giản hoá việc cấu hình so với iptable truyền thống
- UFW cho phép thiết lập các quy tắc để kiểm soát lưu lượng mạng vào và ra khỏi hệ thống 1 cách dễ dàng
## Cấu hình UFW:
- **Cập nhật hệ thống**
- Cài đặt **UFW**: Sử dụng lệnh:
```
sudo apt install ufw
```
- **Kiểm tra trạng thái của UFW**: Mặc định UFW sẽ tắt, sử dụng câu lệnh để kiểm tra:
```
sudo ufw status
```
- **Thiết lập chính sách mặc định**: Thiết lập chính sách mặc định để từ chối mọi lưu lượng truy cập đến và cho phép mọi lưu lượng truy cập đi:
```
sudo ufw default deny incoming
sudo ufw default allow outgoing
```

- **Cho phép truy cập từ xa SSH**:
```
sudo ufw allow ssh
```
- Truy cập từ xa SSH thành công:
![image](https://github.com/user-attachments/assets/e890dd81-f242-48fc-8f6f-5ae9c6469636)

- **Bật UFW**: Bật UFW để khởi động tường lửa
```
sudo ufw enable
```

- **Cho phép các cổng cụ thể**: Có thể cho phép các cổng cụ thể khi cần. Ví dụ, để cho phép lưu lượng HTTP và HTTPS
```
sudo ufw allow http
sudo ufw allow https
```
![image](https://github.com/user-attachments/assets/ca452c22-089b-4295-bfac-16bff21ad067)

- **Kiểm tra lại trạng thái của UFW**: Đảm bảo rằng UFW đang bật và các luật được thực thi
```
sudo ufw status verbose
```
![image](https://github.com/user-attachments/assets/9a4495d3-2494-477e-a5aa-8b5cf3cc3b3a)

