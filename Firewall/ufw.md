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
