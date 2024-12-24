# Tổng quan về ufw
## Khái niệm:
- UFW (Uncomplicated Firewall) là một công cụ quản lý tường lửa được phát triển bởi Canonical, công ty đứng sau hệ điều hành Ubuntu. UFW được thiết kế để đơn giản hóa việc cấu hình tường lửa trên Linux, giúp người dùng dễ dàng thiết lập và quản lý các quy tắc tường lửa mà không cần phải sử dụng các lệnh phức tạp của iptables.
---
## Tính năng:
- **Dễ sử dụng**: UFW cung cấp các lệnh ngắn gọn và dễ nhớ, giúp người dùng dễ dàng mở hoặc chặn các cổng mạng.
- **Cấu hình mặc định an toàn**: UFW mặc định chặn tất cả các kết nối đến và cho phép tất cả các kết nối đi ra ngoài, giúp bảo vệ hệ thống khỏi các cuộc tấn công từ bên ngoài.
- **Hỗ trợ IPv6**: UFW hỗ trợ cả IPv4 và IPv6, giúp bảo vệ hệ thống trong môi trường mạng hiện đại.
- **Tích hợp với các dịch vụ phổ biến**: UFW có thể dễ dàng cấu hình để cho phép hoặc chặn các dịch vụ phổ biến như SSH, HTTP, HTTPS, và nhiều dịch vụ khác.
---
## Cách cài đặt và sử dụng:
- Cập nhật hệ thống trước khi cài đặt:
```shell
sudo apt update
sudo apt upgrade -y
```
- Kiểm tra xem **UFW** đã cài sẵn trên máy chưa: `which ufw`
- Nếu không nhận được kết quả nào, nghĩa là ufw chưa được cài đặt trong máy. Sử dụng lệnh sau để cài đặt:
```shell
sudo apt install ufw
```
- Mặc định sau khi cài đặt, ufw sẽ không được kích hoạt. Bạn cần giữ nguyên như thế. Chỉ kích hoạt UFW sau khi đã thực hiện những bước cấu hình căn bản:
```
sudo ufw status
```
> OUTPUT: Status: inactive
---
## Cấu hình căn bản:
### Thiết lập chế độ mặc định:
- Chặn truy cập từ bên ngoài vào máy chủ:
```shell
sudo ufw default deny incoming
```

```shell
> OUTPUT
Default outgoing policy changed to 'allow'
(be sure to update your rules accordingly)
```

- Cho phép kết nối từ máy chủ ra bên ngoài:
```shell
sudo ufw default allow outgoing
```

```shell
> OUTPUT
Default outgoing policy changed to 'allow'
(be sure to update your rules accordingly)
```

### Mở cổng kết nối SSH:
- Cần mở cổng kết nối SSH trước khi kích hoạt UFW. Nếu không, sẽ không thể truy cập vào máy chủ được nữa, do thiết lập mặc định đã chặn mọi kết nối từ bên ngoài vào.
- Sử dụng **OpenSSH**: `sudo ufw allow OpenSSH`
- Sử dụng tên dịch vụ `ssh`: `sudo ufw allow ssh`
- Sử dụng cổng 22: `sudo ufw allow 22`
---
## Kích hoạt UFW:
- Trước khi kích hoạt, kiểm tra lại các quy tắc đã được thiết lập trên UFW
```shell
sudo ufw show added
```

- Kích hoạt UFW:
```
sudo ufw enable
```
- Hệ thống sẽ cảnh báo việc kích hoạt UFW có thể gây gián đoạn kết nối SSH. Do bạn đã cấu hình mở cổng SSH nên sẽ không gặp vấn đề nào cả. Chọn y và bấm Enter để xác nhận.
```shell
> OUTPUT
Command may disrupt existing ssh connections. Proceed with operation (y|n)? y
Firewall is active and enabled on system startup
```

- Kiểm tra lại tình trạng hoạt động của UFW:
```shell
sudo ufw status verbose
```

```
> OUTPUT
Status: active
Logging: on (low)
Default: deny (incoming), allow (outgoing), deny (routed)
New profiles: skip

To                         Action      From
--                         ------      ----
22/tcp (OpenSSH)           ALLOW IN    Anywhere                  
22/tcp (OpenSSH (v6))      ALLOW IN    Anywhere (v6)
```
---
## Cấu hình UFW nâng cao:
### 1. Mở kết nối cho web server Apache/Nginx:
- Dịch vụ web server HTTP sử dụng cổng 80, mở kết nối bằng lệnh:
```shell
sudo ufw allow http
hoặc
sudo ufw allow 80
```
- Dịch vụ web server HTTPS sử dụng cổng 443, mở kết nối bằng lệnh:
```shell
sudo ufw allow https
hoặc
sudo ufw allow 443
```
- Cũng có thể mở kết nối HTTP và HTTPS chỉ theo tên của Web Server: **sudo ufw allow 'Apache Full'** (nếu máy chủ đang cài web server Apache) hoặc **sudo ufw allow 'Nginx Full'** (nếu máy chủ đang cài web server Nginx)

### 2. Mở kết nối theo cổng mạng:
```shell
sudo ufw allow <port>
```
- Ví dụ: Mở thêm kết nối cổng 873 cho dịch vụ truyền tải file qua mạng `rsync`
```
sudo ufw allow 873
```
- Có thể mở cùng lúc 1 dãy port , nhưng phải kết hợp thêm giao thức (udp / tcp) vào lệnh. Ví dụ:
```
sudo ufw allow 6000:6007/tcp
sudo ufw allow 6000:6007/udp
```

### 3. Cho phép kết nối theo địa chi IP:
```
sudo ufw allow form <IP>
```
- Có thể quy định thêm cổng kết nối để giới hạn truy cập cho IP. Ví dụ muốn cho phép địa chỉ IP 123.123.123.123 kết nối vào cổng 22 (SSH), sử dụng lệnh sau:
```shell
sudo ufw allow from 123.123.123.123 to any port 22
```

### 4. Cho phép kết nối theo Subnet:
- Có thể thay thế IP bằng Subnet để cho phép kết nối theo lớp mạng.
- Ví dụ: cho phép dãy IP từ 10.0.1.1 đến 10.0.1.254, sử dụng lệnh sau:
```shell
sudo ufw allow from 10.0.1.0/24
```

### 5. Chặn kết nối:
- Sử dụng tham số `deny` để chặn kết nối vào máy chủ
- Chặn kết nối HTTP: `sudo ufw deny http`
- Chặn địa chỉ IP: `sudo ufw deny from <IP>`
- Chặn cổng 25 từ máy chủ ra bên ngoài (mục đích nhằm chặn dịch vụ email SMTP): `sudo ufw deny out 25`

### 6. Xoá kết nối theo thứ tự:
- Để xoá quy tắc theo số thứ tự, cần liệt kê các quy tắc theo thứ tự bằng lệnh:
```
sudo ufw status numbered
```
- Kết quả:
```shell
> OUTPUT
Status: active

     To                         Action      From
     --                         ------      ----
[ 1] OpenSSH                    ALLOW IN    Anywhere                  
[ 2] 80/tcp                     ALLOW IN    Anywhere                  
[ 3] OpenSSH (v6)               ALLOW IN    Anywhere (v6)             
[ 4] 80/tcp (v6)                ALLOW IN    Anywhere (v6)
```

- Nếu muốn xoá kết nối dịch vụ HTTP, số thứ tự 2, dùng lệnh:
```
sudo ufw delete 2
```
```shell
Deleting:
 allow 80
Proceed with operation (y|n)? y
Rule deleted
```

### 7. Xoá kết nối UFW theo tên hoặc cổng mạng:
- Ví dụ : Xoá kết nối dịch vụ HTTP bằng 1 trong 2 cách sau:
```shell
sudo ufw delete allow http
hoặc
sudo ufw delete allow 80
```
- Khi sử dụng cách xoá kết nối theo tên hoặc cổng mạng, cả hai quy tắc của IPv4 và IPv6 đều sẽ bị xoá.

### 8. Kiểm tra tình trạng hoạt động của UFW:
- Sử dụng lệnh: `sudo ufw status verbose`
```shell
> OUTPUT
Status: active
Logging: on (low)
Default: deny (incoming), allow (outgoing), deny (routed)
New profiles: skip

To                         Action      From
--                         ------      ----
22/tcp (OpenSSH)           ALLOW IN    Anywhere                  
80/tcp                     ALLOW IN    Anywhere                  
22/tcp (OpenSSH (v6))      ALLOW IN    Anywhere (v6)             
80/tcp (v6)                ALLOW IN    Anywhere (v6)
```

### 9. Tắt hoặc thiết lập lại UFW:
- Vô hiệu hoá UFW: `sudo ufw disable`
> OUTPUT: Firewall stopped and disabled on system startup
- Khi vô hiệu hoá ufw, các quy tắc đã thiết lập vẫn được giữ nguyên, không bị xoá. Khi kích hoạt lại các quy tắc cũng sẽ xuất hiện trở lại
- Xoá hết các quy tắc đã thiết lập và cấu hình UFW lại từ đầu: `sudo ufw reset`
