# Cài đặt và sử dụng tường lửa CSF
## Giới thiệu:
- **CSF (Config Server Security & Firewall)** là tường lửa Stateful Packet Inspection (SPI) mã nguồn mở phổ biến giúp bảo vệ hệ thống trên hệ điều hành Linux.
- Ngoài các tính năng cơ bản của Firewall là filter packet in/out thì CSF còn hỗ trợ ngăn chặn các cuộc tấn công như Brute Force, ddos …
- CSF có thể cấu hình block/restrict port để giới hạn port truy cập. Đồng thời CSF duy trì danh sách whitelist và blacklist để kiểm soát truy cập.
- CSF cũng cung cấp Connection Limiting để giới hạn số lượng kết nối, Rate Limiting để giới hạn tần số truy cập, Real Time Block List và Port Scan Tracking (chống Scan Port).

## Cài đặt CSF:
- **Bước 1**: Vô hiệu hoá UFW (do Ubuntu đang có sắn tường lửa UFW, cần tắt để tránh xung đột)
```
sudo ufw disable
```

- **Bước 2**: Cài đặt các thành phần phụ thuộc cần thiết cho **CSF**
```
sudo apt install perl zip unzip libwww-perl liblwp-protocol-https-perl
```

- **Bước 3**: Tải xuống và cài đặt CSF:
```
cd /usr/src
sudo rm -fv csf.tgz
sudo wget https://download.configserver.com/csf.tgz
sudo tar -xzf csf.tgz
cd csf
sudo sh install.sh
```

- **Bước 4**: Xác minh module iptables cần thiết đã được cài đặt:
```
sudo perl /usr/local/csf/bin/csftest.pl
```
![image](https://github.com/user-attachments/assets/c314867f-b6ce-41cd-9092-a57b646bc482)

- **Bước 5**: Cấu hình CSF: Cần vô hiệu hoá chế độ **TESTING** để khởi động *lfd daemon (Login Fail Detect daemon)*:
```shell
> sudo nano /etc/csf/csf.conf
# TESTING = 1
TESTING = 0
```
![image](https://github.com/user-attachments/assets/4cd53ef7-e500-4899-8074-57417308f484)

- **Bước 6**: Khởi động lại và kiểm tra CSF:
```
# systemctl restart {csf,lfd}
# systemctl enable {csf,lfd}
# systemctl is-active {csf,lfd}
# csf -v
```
![image](https://github.com/user-attachments/assets/51feab22-27e4-4e56-849d-fa7392b997a2)

## Cấu hình CSF: 
- Cấu hình được thực hiện bằng cách chỉnh sửa các file config khác nhau mà CSF đi kèm. Các file đó nằm trong `/etc/csf`
- Các config files chính bao gồm:
- **csf.conf**: File cấu hình chính, nó có các ghi chú, giải thích chức năng của từng option
- **csf.allow**: Danh sách các địa chỉ IP được phép thông qua tường lửa (whitelist)
- **csf.deny**: Danh sách các địa chỉ IP không được phép thông qua tường lửa (blacklist)
- **csf.ignore**: Danh sách các địa chỉ IP mà lfd bỏ qua mà không block nếu phát hiệm vi phạm rule
- **csf.(*)ignore**: Các file ignore khác, liệt kê các files, users, IP và lfd bỏ qua. - Nếu sửa đổi bất kỳ file nào được liệt kê ở trên ta cần restart csf và lfd để chúng có hiệu lực

## Sử dụng CSF:
### 1. Mở port:
- Mở port là thao tác giúp cho các client ở bên ngoài có thể truy cập vào các port trên server (incomming traffic) hoặc cho phép server mở các kết nối ra ngoài (outgoing traffic). Thực hiện mở port trong file `csf.conf`
- Tham số **TCP_IN/TCP_OUT** và **UDP_IN/UDP_OUT** dùng để khai báo danh sách port, các port được cách nhau bằng dấu phẩy
- Cho phép truy cập vào (incomming) các TCP port trên server:
```shell
# Allow incoming TCP ports
TCP_IN = "20,21,22,25,53,80,110,143,443,465,587,993,995"
```

- Cho phép server kết nối ra (outgoing) tới các TCP port bên ngoài:
```shell
# Allow outgoing TCP ports
TCP_OUT = "20,21,22,25,53,80,110,113,443,587,993,995"
```

- Cho phép truy cập tới (incomming) các UDP port trên server
```shell
# Allow incoming UDP ports
UDP_IN = "20,21,53,80,443"
```

- Cho phép server kết nối ra (outgoing) tới các UDP port bên ngoài
```shell
# Allow outgoing UDP ports
# To allow outgoing traceroute add 33434:33523 to this list
UDP_OUT = "20,21,53,113,123"
```

### 2. Portflood CSF:
- Tính năng này cung cấp khả năng bảo vệ chống lại các cuộc tấn công flood vào port, chẳng hạn như ddos. Có thể chỉ định số lượng kết nối được phép trên 1 port trong khoảng thời gian nào đó.
- Cấu trúc: `Port;protocol;hit count;interval seconds`
- Ví dụ: **PORTFLOOD = "22;tcp;5;300,80;tcp;20;5"**
- Ý nghĩa:
  - Nếu IP nào có hơn 5 kết nối TCP trong vòng 300s thì sẽ chặn không cho IP đó kết nối đến cổng 22
  - Nếu IP nào có hơn 20 kết nối TCP đến cổng 80 trong vòng 5s thì sẽ chặn không cho IP đó kết nối đến cổng 80

### 3. Port Knocking:
- **Port Knocking** cho phép client thiết lập kết nối tới một port trên server nhưng bình thường port này không được open public
- Server chỉ cho phép clients kết nối tới port chính sau khi client phải hoàn thành một chuỗi knock port thành công.
- Tính năng này yêu cầu liệt kê các cổng không sử dụng (ít nhất 3).
- Các cổng chọn không sử dụng và xuất hiện trong **TCP_IN/UDP_IN**. Cổng được mở cũng không được xuất hiện trong **TCP_IN/UDP_IN**
- Cấu trúc: `openport;protocol;timeout;port1;port2;port3;port4…portN`
- Ví dụ: **PORTKNOCKING = "22;tcp;20;100;200;300;400"**
- Ý nghĩa: Mở cổng tcp 22 trong 20s tới địa chỉ IP đang kết nối với các kết nối mới sau khi các cổng 100, 200, 300, 400 đã được truy cập, mỗi lần cách nhau 20s

### 4. Connection limit:
- Tính năng này có thể sử dụng để giới hạn số lượng kết nối đang hoạt động từ một địa chỉ IP đến mỗi cổng. Khi được cấu hình đúng cách có thể tránh được các hành vi lạm dụng trên server, chẳng hạn như các cuộc tấn công ddos:
- Cấu trúc: `port;limit`
- Ví dụ: **CONNLIMIT = "22;1,80;20"**
- Ý nghĩa:
  - Chỉ cho phép 5 kết nối mới đồng thời tới cổng 22 trên mỗi địa chỉ IP
  - Chỉ cho phép 20 kết nối mới đồng thời tới cổng 80 trên mỗi địa chỉ IP

### 5. CSF Allow/Deny IP theo port và protocol:
- Có thể thêm các filter port và IP bằng cấu trúc: `tcp/udp|in/out|s/d=port|s/d=ip|u=uid|`
- Cấu hình trong 2 file `/etc/csf/csf.allow` và `/etc/csf/csf.deny`
- Ý nghĩa:
  - **tcp/udp**: Xét giao thức tcp hoặc udp
  - **in/out**: Incomming traffic hoặc outgoing traffic
  - **s/d = port**: Áp dụng cho source port hoặc destination port (hoặc ICMP type). Có thể khai báo range port bằng cách sử dụng dấu “_”, ví dụ 2000_3000
  - **u/g = UID**: UID hoặc GID của source packet, áp dụng vào outgoing connection. Lúc này, giá trị của s/d = IP sẽ bị bỏ qua
- Ví dụ:
  - TCP kết nối vào đến port 80 từ IP `11.22.33.44`: **tcp|in|d=80|s=11.22.33.44|**
  - TCP kết nối ra đến port 22 đến IP `11.22.33.44`: **tcp|out|d=22|d=11.22.33.44|**
- Chú ý: nếu dấu `|` bị bỏ qua, giao thức mặc định được đặt thành `tcp`, hướng kết nối mặc định được đặt thành `in`
  - TCP kết nối vào đến port 22 từ IP `44.33.22.11`: **d=22|s=44.33.22.11**
  - TCP kết nối ra đến từ port 80 từ UID 99: **tcp|out|d=80|u=90**
  - ICMP kết nối ra đến từ port 80 từ UID 99: **icmp|out|d=80|u=99**
  - ICMP kết nối vào, ping từ 44.33.22.11: **icmp|in|d=ping|s=44.33.22.11**

### 6. Port Scan Tracking – Chống Scan Port:
- **Port scan** là một phương pháp để xác định cổng nào trên mạng được mở
- **CSF** có khả năng chặn các địa chỉ IP tham gia vào quá trình port scan bằng cách sử dụng tính năng **Port Scan Tracking**.
- Tính năng này hoạt động bằng cách quét các gói tin bị Iptables block trong syslog. Nếu địa chỉ IP tạo port block được ghi lại log nhiều hơn giá trị *PS_LIMIT* trong vòng *PS_INTERVAL* giây, địa chỉ IP sẽ bị chặn
- Ví dụ: Khi `PS_INTERVAL` được đặt ở giá trị mặc định là 300 và `PS_LIMIT` được đặt ở 10, bất kỳ địa chỉ IP nào được ghi lại hơn 10 lần trong khoảng thời gian 300 giây sẽ bị chặn

## Login Failure Daemon (LFD):
- **LFD** là một tiến trình nằm trong CSF (ConfigServer Security & Firewall) kiểm tra định kỳ các mối đe dọa tiềm ẩn đối với máy chủ.
- LFD tìm kiếm các cuộc tấn công cũng như các nỗ lực đăng nhập sai (brute-force) và nếu tìm thấy sẽ chặn địa chỉ IP cố gắng tấn công máy chủ đó.
- LFD theo dõi logs liên tục, do đó có thể phản ứng trong vài giây sau khi phát hiện những nỗ lực đó.
- Nó cũng giám sát trên từng giao thức, vì vậy nếu các nỗ lực được thực hiện trên các giao thức khác nhau trong một khoảng thời gian ngắn, tất cả các nỗ lực đó sẽ được tính và được coi là nguy cơ tiềm ẩn với máy chủ

### 1. Application Trigger:
```
LF_SSHD = 5
LF_SSHD_PERM = 1
```
- LF_SSHD: Ngưỡng đăng nhập sai tối đa, nếu vượt quá số lượng này, IP sẽ bị block
- LF_SSHD_PERM: Thời gian block. Giá trị “1” là block vĩnh viễn, giá trị cao hơn là block tạm thời trong vài giây

### 2. Cảnh báo qua email (email alert):
```shell
# Leave this option empty to use the To: field setting in each alert template
LF_ALERT_TO = “”

# By default, lfd will send alert emails using the relevant alert template from
# the From: address configured within that template. Setting the following
# option will override the configured From: field in all lfd alert emails
#
# Leave this option empty to use the From: field setting in each alert template
LF_ALERT_FROM = “”

# By default, lfd will send all alerts using the SENDMAIL binary. To send using
# SMTP directly, you can set the following to a relaying SMTP server, e.g.
# “127.0.0.1”. Leave this setting blank to use SENDMAIL
LF_ALERT_SMTP = “”
```

### 3. Login Tracking – Theo dõi các đăng nhập thất bại:
- Login tracking là một phần mở rộng của lfd, nó theo dõi các lần đăng nhập POP3, IMAP và giới hạn chứng ở mức X kết nối mỗi giờ cho mỗi tài khoản trên mỗi địa chỉ IP.
- Nó sử dụng iptables để chỉ chặn kẻ xâm phạm đến cổng giao thức thích hợp, xóa chúng mỗi giờ và bắt đầu đếm các lần đăng nhập mới kể từ khi xóa. - - Tất cả các block này chỉ là tạm thời và có thể được xóa thủ công bằng cách khởi động lại csf

### 4. Directory Watching – Theo dõi thư mục:
- Directory watching cho phép lfd kiểm tra `/tmp` và `/dev/shm` và các thư mục thích hợp khác để tìm các file đáng ngờ, các script exploit

## IP Block List – Cập nhật danh sách IP cần chặn:
- Tính năng này cho phép csf và lfd tải xuống định kỳ danh sách địa chỉ IP và CIDR từ published block hoặc black list. Danh sách blocklists được khai báo trong file: `/etc/csf/csf.blocklists`
- Cấu trúc: **NAME|INTERVAL|MAX|URL**
- Trong đó:
  - **Name**: List name với tất cả các ký tự chữ cái viết hoa không có khoảng trắng và tối đa 25 ký tự – tên này sẽ được sử dụng làm Iptables chain name
  - **INTERVAL**: Khoảng thời gian làm mới để tải xuống danh sách, tối thiểu phải là 3600s và tối đã 86400s
  - **MAX**: Đây là số lượng địa chỉ IP tối đa để sử dụng từ danh sách, giá trị bằng 0 có nghĩa là tất cả IP đều được sử dụng
  - **URL**: URL để tải xuống danh sách
 
## CSF Allow/Deny theo Quốc gia:
- Cho phép và từ chối các truy cập quốc tế và server của mình. Để làm như vậy vân nhập country code vào danh sách được phân tách bởi dấu phẩy
- Khi sử dụng `CC_ALLOW`, IP sẽ được allow mà không quan tâm đến Port. Ta có thể sử dụng CC_ALLOW_PORT để cho phép truy cập từ các quốc gia nhưng vẫn dựa trên port
```
# Each option is a comma separated list of CC’s, e.g. “US,GB,DE”
CC_ALLOW_PORTS = “VN”

# All listed ports should be removed from TCP_IN/UDP_IN to block access from
# elsewhere. This option uses the same format as TCP_IN/UDP_IN
#
# An example would be to list port 21 here and remove it from TCP_IN/UDP_IN
# then only countries listed in CC_ALLOW_PORTS can access FTP
CC_ALLOW_PORTS_TCP = “80,443”
CC_ALLOW_PORTS_UDP = “53”
```
- Tương tự với `CC_DENY`

## Sử dụng Command Line:
- CSF deny IP: Chặn không cho IP 1.1.1.1 truy cập đến server
```
csf -d 1.1.1.1
```
- CSF allow IP: Cho phép IP 1.1.1.1 truy cập đến server
```
csf -a 1.1.1.1
```
- CSF undeny IP: Remove 1.1.1.1 đang bị chặn
```
csf -dr 1.1.1.1
```
- CSF unallow IP: Remove 1.1.1.1 đang được cho phép kết nối đến server
```
csf -ar 1.1.1.1
```
- Kiểm tra trạng thái csf:
```
csf -l
```
- Reload csf:
```
csf -r
```
- Dừng csf:
```
csf -s
```
- Vô hiệu hoá csf:
```
csf -f
```
- Cập nhật csf:
```
csf -u
```
- Dừng dịch vụ csf và lfd:
```
csf -e
```
- Khởi động lại csf service:
```
systemctl restart csf.service
```
