# Thực hành trên linh kiện thật - Thao tác cơ bản với Switch.
## Để cài đặt các cấu hình với Switch, ta cần kết nối Switch Cisco với Server qua dây Console để thao tác định cấu hình.
- Kết nối cáp điều khiển rollover với cổng điều khiển RJ-45 của công tắc
- Kết nối đầu cáp còn lại vào cổng COM nối tiếp trên máy tính
- Vào Device Manager, kiểm tra phần Port (COM & LPT), nếu hiện như này tức là đã kết nối thành công <p>
 ![image](https://github.com/user-attachments/assets/4ea12a1d-5656-4b98-9e03-044f1e87b48d)
- Sử dụng MobaXsterm, mở kết nối phiên tới Switch thông qua Serial.
![image](https://github.com/user-attachments/assets/47d2de58-ad8f-45c9-8ea8-21537f18debc)
- Sau khi tạo phiên, nếu phiên phản hồi thông tin tức là kết nối phiên thành công.
### Thao tác cơ bản đặt hostname: 
- Sử dụng lệnh sau để đổi tên hostname
  ```
  Switch(config)#hostname new_name
  ```
- Hiển thị như này tức là đã đổi tên hostname thành công
![image](https://github.com/user-attachments/assets/0f5a66d8-32ba-42e6-bec4-33bce16346d3)

### IP Management: Quản lý địa chỉ IP được thực hiện để dễ dàng cấu hình và sửa chữa thiết bị từ xa. Để quản lý thiết bị qua giao diện web như Telnet hoặc SSH, cần định nghĩa 1 địa chỉ IP cho thiết bị. Nếu không có địa chỉ IP quản lý, ta sẽ phải truy cập console để quản lý switch.
- Để cấu hình địa chỉ IP quản lý cho Switch, thực hiện các bước sau:
