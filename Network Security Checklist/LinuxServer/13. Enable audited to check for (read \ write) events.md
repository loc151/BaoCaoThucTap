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
