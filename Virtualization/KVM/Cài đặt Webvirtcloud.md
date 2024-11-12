# Cài đặt Webvirtcloud trên Ubuntu 22.04

## Tổng quan
Webvirtcloud là một trong những công cụ quản lý máy ảo KVM. Nó có chức năng gần giống với virt-manager khi có thể kết nối đến nhiều host KVM để có thể quản lý tập trung các VM trên các máy đó. Nhưng nó có một ưu điểm đặc biệt hơn so với virt-manager đó là với virt-manager đó là ta chỉ có thể làm việc tại máy cài virt-manager. Còn với Webvirtcloud ta có thể làm việc với các VM ở bất kỳ đâu có internet.

## Yêu cầu: 
- Một máy cài đặt hệ điều hành Ubuntu server 20 có cấu hình tối thiểu 1 CPU, 1 GB RAM và có 1 card mạng.
- Ít nhất một máy Ubuntu đã cài đặt KVM để kiểm tra lại webvirtcloud đã hoạt động.

## Cài đặt Webvirtcloud tại Server: 
### 1. Cài đặt Nginx và các gói khác:
- Sử dụng các dòng lệnh sau để tải các gói cần thiết: 

```
apt-get install git virtualenv python3-virtualenv python3-dev python3-lxml libvirt-dev zlib1g-dev libxslt1-dev nginx supervisor libsasl2-modules gcc pkg-config python3-guestfs libsasl2-dev libldap2-dev libssl-dev -y
```

### 2. Cài đặt và cấu hình Webvirtcloud: 
- Tải xuống phiên bản WebVirtCloud mới nhất từ kho lưu trữ Git bằng lệnh:

```
git clone https://github.com/retspen/webvirtcloud
```

![image](https://github.com/user-attachments/assets/c84f3ead-9dcd-4d2c-9a95-89eb0add123e)

- Thay đổi thư mục thành webvirtcloud và sao chép tệp **setting.py**: 

```
cd webvirtcloud
cp webvirtcloud/settings.py.template webvirtcloud/settings.py
```

- Chỉnh sửa tệp settings.py và xác định khóa bí mật:

```
nano webvirtcloud/settings.py
```

![image](https://github.com/user-attachments/assets/0b54ff09-e151-48b8-a840-01270b4842fa)

- Sao chép tệp cấu hình **WebVirtCloud** vào thư mục `Nginx` và `Supervisor`:

```
cp conf/supervisor/webvirtcloud.conf /etc/supervisor/conf.d
cp conf/nginx/webvirtcloud.conf /etc/nginx/conf.d
```

- Mở tệp cấu hình Nginx để chỉnh sửa:
```
sudo nano /etc/nginx/conf.d/webvirtcloud.conf
```

- Đặt giá trị chính xác cho tên máy chủ và cấu hình các tệp log.
```nginx
server {
    listen 80;

    server_name webvirtcloud.example.com;
    access_log /var/log/nginx/webvirtcloud-access_log;
    error_log /var/log/nginx/webvirtcloud-error_log;
}
```

- Quay lại thư mục chính và di chuyển thư mục **webvirtcloud** sang thư mục **/srv**:

```
cd..
mv webvirtcloud /srv/
```

- Đặt quyền sở hữu thích hợp cho thư mục **webvirtcloud**:

```
chown -R www-data:www-data /srv/webvirtcloud/
```

- Thay đổi thư mục thành **webvirtcloud** và tạo một môi trường ảo: 

```
cd /srv/webvirtcloud/
virtualenv -p python3 venv
```

![image](https://github.com/user-attachments/assets/29b57002-baf4-44c2-953d-c30715adc56f)

- Kích hoạt môi trường ảo:

```
source venv/bin/activate
```


-  Cài đặt các phụ thuộc Python cần thiết:

```
pip3 install -r conf/requirements.txt
```

![image](https://github.com/user-attachments/assets/8e90423f-c873-4587-945e-6289401866bb)

- Chạy lệnh di chuyển để tạo tất cả các bảng:

```
python3 manage.py migrate
```

![image](https://github.com/user-attachments/assets/32ce930b-b5eb-49b5-9f72-5dca5fbd9890)

- Khởi động lại dịch vụ Nginx và Giám sát viên để áp dụng các thay đổi:

```
systemctl restart nginx
systemctl restart supervisor
```

- Xác minh trạng thái của Nginx:

```
systemctl status nginx
```
- Kiểm tra các dịch vụ được quản lý bởi supervisor xem có đang chạy không.
```bash
$ sudo supervisorctl status
novncd                           RUNNING   pid 3786, uptime 0:28:36
socketiod                        RUNNING   pid 3787, uptime 0:28:36
webvirtcloud                     RUNNING   pid 3788, uptime 0:28:36
```

![image](https://github.com/user-attachments/assets/7da718dc-088d-489f-aa68-d9cf595e2be5)

- Xác nhận dịch vụ đang hoạt động.
```bash
$ ss -tunelp|grep 8000
tcp   LISTEN 0      2048             127.0.0.1:8000      0.0.0.0:*    uid:33 ino:30133 sk:1001 cgroup:/system.slice/supervisor.service <-> 
```

### 3. Thiết lập KVM và Libvirt:
- Chạy tập lệnh sau để thiết lập KVM và Libvirt:

```
wget -O - https://bit.ly/36baWUu | sh
```
![image](https://github.com/user-attachments/assets/021e8225-7b57-4091-8fc7-c3da5681697d)

![image](https://github.com/user-attachments/assets/d0652dfb-fbc3-4b11-9748-96372e47561d)


![image](https://github.com/user-attachments/assets/a55559f2-6ee1-4886-ba3a-f03c238c6e1e)

- Thêm người dùng KVM vào nhóm dữ liệu www: 

```
adduser www-data kvm
```

### 4. Truy cập WebVirtCloud Dashboard 
- Truy cập URL cài đặt WebVirtCloud tại `http://yourserverhostname`.
- Thông tin đăng nhập mặc định là:
  - Tên đăng nhập: admin
  - Mật khẩu: admin

![image](https://github.com/user-attachments/assets/b628e1a3-a911-4b8f-942e-9a049eab30e6)

Thay đổi mật khẩu của người dùng admin:  
Sau khi đăng nhập, chuyển đến góc trên bên phải nơi tên người dùng admin được hiển thị. Nhấp vào tên người dùng để thấy menu xổ xuống.

Nhấp vào “Profile” > “Edit Profile” > “Change Password”.

![image](https://github.com/user-attachments/assets/68f28c97-7503-456c-acca-58ab97e8179f)

Nhập mật khẩu cũ là “admin“, sau đó nhập và xác nhận mật khẩu mới cho người dùng admin.

Đăng xuất khỏi bảng điều khiển quản trị và đăng nhập lại để kiểm tra mật khẩu mới.
