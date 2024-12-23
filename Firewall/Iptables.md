# Các câu lệnh với iptables
## Tổng quan:
- Hầu hết các bản phân phối của Linux đều bao gồm 1 loại tường lửa dựa trên máy chủ (host-based) được gọi là Netfilter (Iptables). Bộ lọc mạng là 1 tập những “hook” bên trong kernel của Linux, chúng cho phép kernel tạo ra những hàm callback đối với tầng Network. 1 hàm callback sẽ được gọi mỗi khi có gói tin đi qua hook tương ứng bên trong tầng mạng.
> Nói 1 cách đơn giản, “hook” là những quy tắc, Iptables sẽ phân loại và xử lý các gói tin vào/ra dựa theo các quy tắc được thiết lập từ trước.
---
## Cấu trúc:
- **Chain**: Có 5 chain trong iptables và mỗi chain chịu trách nhiệm cho một nhiệm vụ cụ thể. Các chain này là: **PREROUTING**, **INPUT**, **FORWARD**, **OUTPUT** và **POSTROUTING**. Giống như tên gọi của chúng, chúng chịu trách nhiệm về các packet ngay khi nhận được, hoặc ngay trước khi định tuyến ra bên ngoài.
- **Table**: các table khác nhau chịu trách nhiệm cho các nhiệm vụ khác nhau. Danh sách table bao gồm:  filter, nat, mangle, raw và security. Hai table đầu được sử dụng nhiều nhất. Table filter chịu trách nhiệm lọc (filter) và hạn chế các packet đến máy chủ. Table nat chịu trách nhiệm về chuyển đổi địa chỉ mạng (NAT – Network Address Translation).
- **target**: Các target chỉ định nơi packet sẽ đi. Điều này được quyết định bằng cách sử dụng các target của chính iptables:
  - ACCEPT (chấp nhận)
  - DROP (gỡ bỏ)
  - RETURN (quay trở lại)
  - Hoặc target của các extension module, phổ biến nhất là DNAT, LOG, MASQUERADE, REJECT, SNAT, TRACE và TTL.
  - Các target được chia thành có kết thúc và không kết thúc. Các target có kết thúc chấm dứt rule và các packet sẽ bị ngừng ở đó. Nhưng các target không kết thúc sẽ xử lý packet theo một cách nào đó và rule sẽ được thực hiện tiếp tục sau đó.
 
### 1. Chain: Mỗi chain chịu trách nhiệm cho một nhiệm vụ cụ thể:
- **PREROUTING**: chain này quyết định điều gì sẽ xảy ra với một packet ngay khi nó tới Network Interface. Chúng ta có các tùy chọn khác nhau như thay đổi packet (có thể là NAT), bỏ packet hoặc không làm gì cả và để nó tiếp tục di chuyển và được xử lý ở nơi khác trên đường đi.
- **INPUT**: Đây là một trong những chain phổ biến vì nó hầu như luôn chứa các rule nghiêm ngặt để kiểm soát truy cập từ internet gây hại cho máy tính của chúng ta. Nếu bạn muốn mở hay chặn một port thì đây là nơi bạn sẽ làm điều đó.
- **FORWARD**: chain này chịu trách nhiệm forward packet. Chúng ta có thể coi máy tính như một bộ định tuyến (router) và đây là nơi mà một số quy tắc (rule) có thể áp dụng để thực hiện công việc.
- **OUTPUT**: chịu trách nhiệm cho tất cả quá trình truy cập ra bên ngoài. Bạn không thể gửi một packet mà không được sự cho phép. Đó là nơi tốt nhất để hạn chế lưu lượng outgoing của bạn nếu bạn không chắc chắn mỗi ứng dụng đang giao tiếp qua cổng nào.
- **POSTROUTING**: chain này là nơi các packet để lại dấu vết cuối cùng, trước khi rời khỏi máy tính của chúng ta. Điều này được sử dụng để định tuyến (routing) trong số nhiều tác vụ khác để đảm bảo các packet được xử lý theo cách chúng ta muốn.
> Hầu hết các trường hợp, ta sẽ sử dụng thường xuyên chain INPUT & OUTPUT.

### 2. Tables: 
Hầu hết thao tác sẽ sử dụng chính trên table filter. Nếu khi viết rule mà không chỉ định bất kỳ table nào, filter được sử dụng theo mặc định. Giải thích từng table:
- **filter**: là table được sử dụng nhiều nhất hàng ngày. Đó là lý do tại sao nó là table mặc định. Trong table này, bạn sẽ quyết định xem packet có được phép vào (input) hoặc ra (output) khỏi máy tính của bạn hay không. Nếu bạn muốn chặn một port để ngừng nhận bất cứ thứ gì, đây là điểm table bạn cần.
- **nat**: Table này là table phổ biến thứ hai và chịu trách nhiệm tạo kết nối mới. Đó là cách viết tắt của Network Address Translation.
- **mangle**: table này dùng để thay đổi dữ liệu bên trong các packet trước khi chúng đến hoặc ra khỏi máy tính.
- **raw**: table này xử lý packet raw chưa qua xử lý như tên gọi của nó. Chủ yếu là để theo dõi trạng thái kết nối. Chúng ta sẽ thấy các ví dụ về điều này bên dưới khi muốn cho các packet thành công từ kết nối SSH.
- **security**: có nhiệm vụ đánh dấu những gói tin có liên quan đến context của SELinux, nó giúp cho SELinux hoặc các thành phần khác hiểu được context SELinux và xử lý gói tin.
---
## Các câu lệnh cơ bản:
### 1. Hiển thị trạng thái của Iptables:
```
iptables -L -n -v
```
- `-L`: Liệt kê danh sách
- `-n`: cho output là số (không phân giải tên, dẫn đến hiệu suất nhanh hơn)
- `-v`: Thêm thông tin chi tiết
```shell
> Output
Chain INPUT (policy ACCEPT 0 packets, 0 bytes)
 pkts bytes target     prot opt in     out     source               destination

Chain FORWARD (policy ACCEPT 0 packets, 0 bytes)
 pkts bytes target     prot opt in     out     source               destination

Chain OUTPUT (policy ACCEPT 0 packets, 0 bytes)
 pkts bytes target     prot opt in     out     source               destination
```

### 2. Bắt đầu/Dừng/Khởi động lại dịch vụ: 
```
service iptables start
service iptables stop
service iptables restart
```
- Cũng có thể sử dụng lệnh `iptables` để dừng dịch vụ hoặc xoá các rule:
```
iptables -F
iptables -X
iptables -t nat -F
iptables -t nat -X
iptables -t mangle -F
iptables -t mangle -X
iptables -P INPUT ACCEPT
iptables -P OUTPUT ACCEPT
iptables -P FORWARD ACCEPT
```
- Trong đó:
  - `-F`: xoá tất cả các rule
  - `-X`: Xoá chain
  - `-t table_name`: chỉ định table để xoá rule hay chain
  - `-P`: thiết lập chính sách mặc định (DROP, REJECT hoặc ACCEPT)

### 3. Xoá rule:
- Để hiển thị số thứ tự của dòng và các thông tin khác của rule đang có, sử dụng:
```
iptables -L INPUT -n --line-numbers
iptables -L OUTPUT -n --line-numbers
iptables -L OUTPUT -n --line-numbers | less
iptables -L OUTPUT -n --line-numbers | grep 103.28.120.1
```
- Sau khi tìm được rule cần thao tác, ví dụ cần xoá dòng 5, sử dụng lệnh sau:
```
iptables -D INPUT 4
```
- Hoặc xoá theo source IP:
```
iptables -D INPUT -s 103.28.120.1 -j DROP
```
- `-D`: tuỳ chọn cho phép xoá rule từ chain được chỉ định

### 4. Thêm rule:
- Sử dụng lệnh kiểm tra thông tin số dòng lệnh. Ví dụ output như sau:
```shell
Chain INPUT (policy DROP)
num  target     prot opt source               destination
1    DROP       all  --  103.28.120.1         0.0.0.0/0
2    ACCEPT     all  --  0.0.0.0/0            0.0.0.0/0           state NEW,ESTABLISHED
```
- Để thêm rule vào giữa dòng 1 và 2, sử dụng lệnh:
```
iptables -I INPUT 2 -s 103.28.120.1 -j DROP
```
- Để xem rule vừa cập nhật, sử dụng:
```
iptables -L INPUT -n --line-numbers
```

```
> OUTPUT
Chain INPUT (policy DROP)
num  target     prot opt source               destination
1    DROP       all  --  202.54.1.1           0.0.0.0/0
2    DROP       all  --  202.54.1.2           0.0.0.0/0
3    ACCEPT     all  --  0.0.0.0/0            0.0.0.0/0           state NEW,ESTABLISHED
```

### 5. Lưu rule:
```shell
service iptables save                              # CentOS/RHEL/Fedora
iptables-save > /root/my.active.firewall.rules     # Another Linux
```

### 6. Khôi phục rule:
```
service iptables restart                           # CentOS/RHEL/Fedora
iptables-restore > /root/my.active.firewall.rules  # Another Linux
```

### 7. Thiết lập chính sách tường lửa mặc định:
- Để loại bỏ toàn bộ lưu lượng, sử dụng lệnh sau:
```shell
iptables -P INPUT DROP
iptables -P OUTPUT DROP
iptables -P FORWARD DROP
iptables -L -v -n
```
- Nếu muốn mở traffic nào chỉ cần thay **DROP** = **ACCEPT**

### 8. Loại bỏ địa chỉ mạng nội bộ ở giao diện mạng công khai:
- Cách tốt nhất để chống giả mạo IP (IP spoofing) là chặn các dải địa chỉ IP private ở card mạng public. Sử dụng lệnh sau:
```shell
iptables -A INPUT -i eth1 -s 192.168.0.0/24 -j DROP
iptables -A INPUT -i eth1 -s 10.0.0.0/8 -j DROP
```
- Ngoài ra, các dải sau cũng là những dải địa chỉ IP có thể dùng để spoof:
  - 10.0.0.0/8 (lớp A)
  - 172.16.0.0/12 (lớp B)
  - 192.168.0.0/16 (lớp C)
  - 224.0.0.0/4 (multicast lớp D)
  - 240.0.0.0/5 (lớp E)
  - 127.0.0.0/8 (dải loopback)

### 9. Chặn 1 địa chỉ IP:
- Để chặn 1 địa chỉ hay 1 dải địa chỉ IP, sử dụng lệnh sau:
```shell
iptables -A INPUT -s 1.2.3.4 -j DROP
iptables -A INPUT -s 192.168.0.0/24 -j DROP
```

### 10. Chặn port:
- Ví dụ muốn chặn request đến/đi ở port 80, sử dụng lệnh:
```shell
iptables -A INPUT -p tcp --dport 80 -j DROP
iptables -A INPUT -i eth1 -p tcp --dport 80 -j DROP
iptables -A INPUT -p tcp -s 1.2.3.4 --dport 80 -j DROP
iptables -A OUTPUT -p tcp  -d 1.2.3.4 --dport 80 -j DROP
```

### 11. Chặn domain:
- Ví dụ muốn chặn Google.com, sử dụng lệnh sau:
```shell
iptables -A OUTPUT -p tcp -d www.google.com -j DROP
```

### 12. Ghi lại log loại bỏ gói:
- Lệnh sau giúp ta ghi lại log và loại bỏ gói tin IP giả mạo trên giao diện mạng public `eth1`:
```
iptables -A INPUT -i eth1 -s 10.0.0.0/8 -j LOG --log-prefix "IP_SPOOF A: "
iptables -A INPUT -i eth1 -s 10.0.0.0/8 -j DROP
```
- Log này sẽ được ghi vào file `/var/log/messages`

### 13. Giới hạn việc ghi lại log:
- Tùy chọn `-limit` có thể giới hạn số dòng log được ghi trong 1 khoảng thời gian, việc này có thể ngăn chặn file log bị tràn thông tin gây khó khăn khi phân tích. Ví dụ dưới đây giới hạn 7 dòng log mỗi 5 phút:
```shell
iptables -A INPUT -i eth1 -s 10.0.0.0/8 -m limit --limit 5/m --limit-burst 7 -j LOG --log-prefix "IP_SPOOF A: "
iptables -A INPUT -i eth1 -s 10.0.0.0/8 -j DROP
```

### 14. Loại bỏ hoặc cho phép lưu lượng theo địa chỉ MAC:
- Sử dụng tùy chọn –mac-source như sau:
```shell
iptables -A INPUT -m mac --mac-source 00:01:02:03:04:AB -j DROP
iptables -A INPUT -p tcp --destination-port 22 -m mac --mac-source 00:01:02:03:04:AB -j ACCEPT
```

### 15. Chặn hoặc cho phép gói Ping ICMP:
- Lệnh sau giúp chặn **ICMP ping**:
```shell
iptables -A INPUT -p icmp --icmp-type echo-request -j DROP
iptables -A INPUT -i eth1 -p icmp --icmp-type echo-request -j DROP
```
- Ta cũng có thể giới hạn chỉ phản hồi ping với những dải IP hoặc IP nhất định:
```shell
iptables -A INPUT -s 192.168.1.0/24 -p icmp --icmp-type echo-request -j ACCEPT
```
- Gói ICMP cũng có nhiều loại, ta có thể tận dụng để cấu hình sao cho phù hợp với nhu cầu:
```shell
iptables -A INPUT -p icmp --icmp-type echo-reply -j ACCEPT
iptables -A INPUT -p icmp --icmp-type destination-unreachable -j ACCEPT
iptables -A INPUT -p icmp --icmp-type time-exceeded -j ACCEPT
iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT
```

### 16. Mở 1 dải port:
```shell
iptables -A INPUT -m state --state NEW -m tcp -p tcp --dport 7000:7010 -j ACCEPT
```

### 17. Mở 1 dải IP:
```shell
iptables -A INPUT -p tcp --destination-port 80 -m iprange --src-range 192.168.1.100-192.168.1.200 -j ACCEPT
#Đối với NAT
iptables -t nat -A POSTROUTING -j SNAT --to-source 192.168.1.20-192.168.1.25
```

### 18. Thiết lập kết nối và restart iptables:
- Khi ta restart iptables, mặc định các kết nối đã thiết lập sẽ bị hủy khi các module sẽ bị gỡ khỏi hệ thống. Để tránh điều này ta có thể chỉnh sửa file sau và đặt trường IPTABLES_MODULES_UNLOAD thành no:
```
nano /etc/sysconfig/iptables-config
IPTABLES_MODULES_UNLOAD = no
```

### 19. Giới hạn số lượng kết nối cùng thời điểm tới máy chủ theo client IP:
```
iptables -A INPUT -p tcp --syn --dport 22 -m connlimit --connlimit-above 3 -j REJECT
iptables -p tcp --syn --dport 80 -m connlimit --connlimit-above 20 --connlimit-mask 24 -j DROP
```
- **–connlimit-above**: áp dụng luật nếu số kết nối vượt quá con số chỉ định
- **–connlimit-mask**: nhóm các máy khách theo độ dài tiền tố (prefix), giá trị có thể từ 0 đến 32 đối với IPv4

### 20. Liệt kê các rule NAT:
```
iptables -t nat -L -n -v
```

```shell
> OUTPUT
Chain PREROUTING (policy ACCEPT 496K packets, 29M bytes)
pkts bytes target prot opt in out source destination
43557 2613K DNAT tcp -- * * 0.0.0.0/0 192.168.184.8 tcp dpt:443 to:10.105.28.42:443
68700 4122K DNAT tcp -- * * 0.0.0.0/0 192.168.184.8 tcp dpt:80 to:10.105.28.42:80
15855 951K DNAT tcp -- * * 0.0.0.0/0 192.168.184.8 tcp dpt:444 to:10.105.28.45:444
16009 961K DNAT tcp -- * * 0.0.0.0/0 192.168.184.8 tcp dpt:81 to:10.105.28.45:81
63495 3810K DNAT tcp -- * * 0.0.0.0/0 192.168.184.8 tcp dpt:445 to:10.105.28.44:445
19615 1177K DNAT tcp -- * * 0.0.0.0/0 192.168.184.8 tcp dpt:82 to:10.105.28.44:82
Chain INPUT (policy ACCEPT 488K packets, 29M bytes)
pkts bytes target prot opt in out source destination

Chain OUTPUT (policy ACCEPT 3280 packets, 207K bytes)
pkts bytes target prot opt in out source destination

Chain POSTROUTING (policy ACCEPT 231K packets, 14M bytes)
pkts bytes target prot opt in out source destination
3832 230K MASQUERADE all -- * * 10.105.28.0/24 !10.105.28.0/24
```

### 21. Xoá rule NAT:
- Cú pháp chung:
```shell
iptables -t nat -v -L -n --line-number
iptables -t nat -v -L PREROUTING -n --line-number
iptables -t nat -v -L POSTROUTING -n --line-number
```

### 22. Chuyển hướng port A sang port B:
```shell
iptables -t nat -A PREROUTING -i $interfaceName -p tcp --dport $srcPortNumber -j REDIRECT --to-port $dstPortNumber
```

### 23. Reset bộ đếm gói tin:
```
iptables -Z
```
