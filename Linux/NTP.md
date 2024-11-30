# Network Time Protocol (NTP)
- **NTP (Network Time Protocol)** trong Linux là một giao thức mạng được sử dụng để đồng bộ hóa thời gian trên các máy tính trong mạng. Đồng bộ hóa thời gian là quan trọng để đảm bảo rằng các máy tính trong mạng hoạt động theo cùng một thời gian chuẩn.
- Trong hệ điều hành Linux, bạn có thể cấu hình NTP bằng cách sử dụng các công cụ và dịch vụ như ntpd hoặc chronyd để quản lý và đồng bộ hóa thời gian.

## Cấu hình timezone: 
- **Bước 1:** Liệt kê các múi giờ có sẵn: `timedatectl list-timezones`
- **Bước 2:** Thiết lập múi giờ thích hợp: `sudo timedatectl set-timezone Asia/Saigon`
- **Bước 3:** Kiểm tra lại múi giờ sau khi thiết lập: `timedatectl`
![image](https://github.com/user-attachments/assets/571bb74e-eca5-4442-b2d3-a7c5023d483c)

### Cấu hình NTP với 'ntp'
- Câu lệnh:
```
sudo apt-get update
sudo apt-get install ntp
```

- **Cấu hình NTP**: Sau khi cài đặt, có thể chỉnh sửa tệp cấu hình của ntp. Tệp cấu hình chính thường là /etc/ntp.conf. Bạn có thể chỉ định các máy chủ NTP khác để đồng bộ thời gian từ chúng.
- Khởi động và kích hoạt dịch vụ NTP: 
```sh
systemctl start ntp
systemctl enable ntp
```

### Cấu hình NTP với `chronyd`
- **Cài đặt chronyd**: `# yum install chrony`
- **Cấu hình chrony**: Chỉnh sửa tệp cấu hình chính /etc/chrony.conf để cấu hình máy chủ NTP.
- **Khởi động và kích hoạt chronyd**:
```sh
systemctl start chronyd
systemctl enable chronyd
```
