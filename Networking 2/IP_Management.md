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
  - Vào chế độ cấu hình VLAN 1:
    ```
    Switch(config)#interface vlan 1
    ```
  - Gán địa chỉ IP cho giao diện VLAN 1 (ở đây dùng IP là 172.16.4.247/20):
    ```
    Switch(config-if)#ip address 172.16.4.247 255.255.240.0
    ```
  - Kích hoạt giao diện VLAN 1:
    ```
    Switch(config-if)#no shutdown
    ```
  - Đặt mật khẩu để tăng cường bảo mật:
    ```
    Switch(config-if)#enable password new_password
    ```
  - Đặt cổng mặc định: (Cổng mặc định phải cùng lớp mạng với địa chỉ IP)
    ```
    Switch(config)#ip default-gateway 172.16.10.1
    ```
  - Sau khi cấu hình xong, kiểm tra lại cấu hình bằng lệnh:
    ```
    Switch#show ip interface brief
    ```
  - Nếu giao diện hiển thị như này tức là đã cấu hình thành công:
  ![image](https://github.com/user-attachments/assets/d346fa63-0159-4315-bde8-89f021f8891d)

### Clock time: Cấu hình thời gian hệ thống là rất quan trọng. Đồng bộ hoá hệ thống giữa tất cả các thiết bị trong mạng cung cấp 1 khung tham chiếu giữa chúng. Điều này là cần thiết để quản lý, bảo mật, lập kế hoạch và gỡ lỗi mạng, vì mọi sự kiện đều phụ thuộc vào thời gian xảy ra.
- Nếu không có việc đồng bộ, việc so khớp log giữa các thiết bị khi theo dõi việc xâm nhập bảo mật hoặc sử dụng mạng là không thể.
- Thời gian đồng bộ cũng giảm thiểu sự nhầm lẫn trong hệ thống tệp chia sẻ, vì thời gian sửa đổi cần phải nhất quán
- Các thiết bị Cisco Switch hỗ trợ giao thức Simple Network Time Protocol (SNTP). Khi được kích hoạt, switch tự động đồng bộ thời gian từ 1 máy chủ SNTP
- Để xem cài đặt thời gian hệ thống trên Switch, sử dụng lệnh:
  ```
  Switch#show clock [detail]
  ```
  Trong đó:
  - Actual Time: Thời gian hệ thống trên thiết bị. Điều này hiển thị múi giờ Giao thức cấu hình máy chủ động (DHCP) và từ viết tắt của múi giờ
  - Time source: Nguồn thời gian bên ngoài cho hệ thống
  - Time from Browser: Chỉ định xem ngày và giờ của công tắc có được đặt từ máy tính định cấu hình bằng cách sử dụng trình duyệt web
  - Time zone (Static): Múi giờ cho mục đích hiển thị
  - DHCP timezone: Chỉ định múi giờ và cài đặt Summer Time hoặc Daylight Saving Time (DST) của hệ thống có thể được lấy từ tuỳ chọn DHCP timezone 
- Quản lý cài đặt thời gian hệ thống trên switch bằng cách sử dụng cấu hình tự động hoặc cấu hình thủ công
  - Cài đặt thủ công:
    ```
    Switch#clock set [hh:mm:ss] [month] [day] [year]
    ```
  - Sau khi cấu hình xong, kiểm tra lại và thấy thời gian của Switch đã thay đổi, nguồn từ user cấu hình
  - Cài đặt tự động:
    ```
    Switch#configure terminal
    Switch(config)#clock source [sntp|browser]
    ```
    `sntp`: chỉ định máy chủ SNTP là nguồn đồng hồ bên ngoài
    `browser`: chỉ định rằng nếu đồng hồ hệ thống chưa được đặt thì nó sẽ đặt theo thông tin thời gian của trình duyệt web khi người dùng đăng nhập vào switch, thông qua HTTP hoặc HTTPS

### NTP (Network Time Protocol): dịch vụ quan trọng không chỉ cho các thiết bị của Cisco mà hầu hết mọi thiết bị mạng. Bất kỳ thiết bị nào cũng cần được đồng bộ hoá chính xác với nguồn thời gian đáng tin cậy như NTP server. NTP đảm bảo rằng tất cả các thiết bị trong mạng có cùng 1 thời gian chính xác, giúp hệ thống hoạt động ổn định và hiệu quả hơn.
- Cấu hình NTP:
  - Cần tạo 1 ACL cho phép tất cả lưu lượng trên Switch:
    ```
    access-list 101 permit ip any any
    ```
  - Áp dụng ACL cho 1 interface cụ thể (trường hợp này dùng GigabitEthernet 2/0/1)
    ```
    interface GigabitEthernet 2/0/1
    ip access-group 101 in
    ```
  - Xác định NTP Server để đồng bộ thời gian:
    ```
    ntp server 0.asia.pool.ntp.org (Domain name)
    ntp server 203.113.174.44 (IP VN NTP Server)
    ```
  - Sau khi cấu hình, kiểm tra trạng thái NTP bằng các lệnh:
    ```
    show ntp status
    show ntp associations
    ```
    ![image](https://github.com/user-attachments/assets/654b95e3-6155-41fd-909d-26864e3b6ea0)
    ![image](https://github.com/user-attachments/assets/681e6d05-e77c-4e77-83c7-3e11e53adda3)

  - Lúc này mới hoàn thành cấu hình nên NTP chưa được đồng bộ, cần 1 khoảng thời gian để tải lại cấu hình.
    ![image](https://github.com/user-attachments/assets/159f8fe0-1465-45f6-b18a-a6a92f036acc)
    ![image](https://github.com/user-attachments/assets/720033ec-189c-43e0-bac1-a70351c89b16)



    
