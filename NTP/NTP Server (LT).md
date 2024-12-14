# NTP Server:
## 1. Khái niệm:
- **NTP Server** là 1 máy tính được sử dụng để đồng bộ thời gian cho các máy tính khác trên mạng.
- NTP Server sử dụng giao thức Network Time Protocol (NTP) để truyền thông tin thời gian giữa các máy tính
  
## 2. Cách hoạt động:
- NTP hoạt động bằng cách sử dụng thuật toán Marzullo để tính toán độ trễ giữa hai máy tính.
- NTP server sẽ gửi một gói tin thời gian đến máy tính client.
- Máy tính client sẽ tính toán độ trễ của gói tin và gửi lại cho NTP server.
- NTP server sẽ sử dụng độ trễ này để tính toán thời gian hiện tại của máy tính client.
![image](https://github.com/user-attachments/assets/a666bc81-d505-4dc0-9edb-a3a379f897de)

## 3. Ứng dụng: 
- NTP có độ chính xác cao, có thể đạt tới mili giây và được sử dụng cho nhiều ứng dụng như:
  - Đồng bộ thời gian cho các máy tính trong mạng
  - Đảm bảo tính toàn vẹn của dữ liệu
  - Thống kê thời gian thực
  - Giám sát mạng

## 4. Ưu điểm của NTP:
- Đảm bảo tính chính xác của thời gian
- Tăng cường bảo mật
- Tăng hiệu suất của các ứng dụng
- Tăng cường khả năng tương tác của các hệ thống
