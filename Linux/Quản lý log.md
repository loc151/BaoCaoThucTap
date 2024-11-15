![image](https://github.com/user-attachments/assets/9af50f0b-5012-408c-a2a5-c597511b74e5)# Quản lý nhật ký - log
## Khái niệm: Log là các tệp chứa thông tin về các sự kiện và hoạt động của hệ thống. Các tệp nhật ký này rất quan trọng để theo dõi, phân tích và khắc phục sự cố hệ thống
## Chức năng:
- **Ghi lại các sự kiện**: Log ghi lại các sự kiện xảy ra trong hệ thống, bao gồm thông tin về khởi động, tắt máy, lỗi hệ thống và các hoạt động của người dùng
- **Giám sát hệ thống**: Quản trị viên hệ thống sử dụng log để giám sát hoạt động của hệ thống và phát hiện các vấn đề tiềm ẩn
- **Khắc phục sự cố**: Khi xảy ra sự cố, log cung cấp thông tin chi tiết giúp xác định nguyên nhân và khắc phục vấn đề

## Cơ chế ghi nhật ký:
![image](https://github.com/user-attachments/assets/7793d9da-ce12-4f68-a036-a3a8f33fa1ba)

1. **Syslog**:
- Là 1 hệ thống quản lý log trong Linux
- Nó được sử dụng để thu thập, lưu trữ và quản lý các thông báo từ các thành phần khác nhau của hệ thống, bao gồm kernel, các dịch vụ hệ thống và các ứng dụng
- Nó được thực hiện bằng **Syslog Daemon (syslogd)**
- Chức năng của **Syslog**:
  - Thu thập thông báo
  - Lưu trữ thông báo
  - Quản lý thông báo
- Khởi động cùng hệ thống:
```
/etc/init.d/syslog {start | stop | reload}
```
- Cấu hình của syslog được lưu trong tệp `/etc/syslog.conf` hoặc `/etc/rsyslog.conf`

2. **Tệp cấu hình /etc/rsyslog.conf**
- Các dòng của tệp cấu hình có dạng:
```
facility.priority  action
```
- Trong đó:
  - **Facility**: Nguồn gốc sinh ra thông báo
  - **Priority**: Mức độ quan trọng của thông báo
  - **Action**: Thao tác thực hiện khi nhận được thông báo
 
- Các loại Facility:

|Facility|Ý nghĩa|
|---|-------|
|auth:|Thông báo về bảo mật hệ thống liên quan đến việc xác thực|
|authpriv:|Thông báo về bảo mật hệ thống liên quan đến quyền truy cập|
|cron:|Thông báo của crond|
|ftp:|Thông báo về dịch vụ ftp|
|kern:|Thông báo của nhân hệ điều hành|
|lpr:|Thông báo của hệ thống in ấn lpr|
|mail:|Thông báo liên quan đến email|
|news:|Thông báo liên quan đến news service|
|syslog:|Thông báo của syslogd|
|user:|Thông báo của các ứng dụng user|
|uucp:|Copy file bằng UUCP (Unix to Unix Copy)|
|daemon:|Chung của các daemon|
|local0-7:|Định nghĩa user|

- Các loại Priority:

|Priority|Ý nghĩa|
|---|-------|
|emerg|Thông báo khẩn "cấp cứu"|
|alert|Báo động|
|crit|Lỗi phần cứng, không thể khắc phục|
|err|Lỗi thông thường|
|warning|Cảnh báo|
|notice|Nhắc nhở|
|info|Thông tin|
|debug|Thông tin kỹ thuật|

- Action:

|Ký hiệu|Thao tác|
|---|-------|
|/file_name|Ghi vào tệp file_name|
|@hostname|Chuyển đến máy host name|
|user_name|Gửi thông báo cho NSD user_name|
|*|Gửi thông báo cho tất cả user đang đăng nhập vào hệ thống|

![image](https://github.com/user-attachments/assets/3ed0826a-1e8b-40be-83ee-684f48b632a6)
