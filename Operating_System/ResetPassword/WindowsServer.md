# Reset Password
## 1. Trường hợp quên pass của user Administrator nhưng có user khác có quyền quản trị tương đương
### 1.1. Đăng nhập bằng tài khoản Admin khác:
- Sử dụng tài khoản Admin khác để đăng nhập vào Windows Server
![image](https://github.com/user-attachments/assets/84514a2a-3c2a-4a32-95ed-201b93222bda)

### 1.2. Mở Command Prompt:
- Nhấn tổ hợp `Windows + R`, nhập `cmd` và nhấn `Enter` để mở **Command Prompt**
![image](https://github.com/user-attachments/assets/c1ea3414-a08e-4e2c-93aa-e2cb63f47cdf)

### 1.3. Thay đổi mật khẩu:
- Trong Command Prompt, nhập lệnh sau để thay đổi mật khẩu cho tài khoản bị quên
```shell
net user <tên tài khoản> <mật khẩu mới>
```

- Sau khi thực hiện lệnh, nếu có thông báo **The command completed successfully** nghĩa là đã đổi mật khẩu thành công
![image](https://github.com/user-attachments/assets/db0a3bd1-a448-4a97-a074-faca8b10e66b)

- Đăng nhập lại user Adminstrator với mật khẩu mới:
![image](https://github.com/user-attachments/assets/78255957-7dad-434d-8c1b-7edd3d29a39d)

## 2. Trường hợp quên pass của user và không có user nào có quyền Administrator:
## 2.1. Khởi động từ đĩa Boot:
- Chuẩn bị USB chứa Windows Server tương ứng với phiên bản hệ điều hành đang sử dụng
- Trong máy Dell Server R620, chọn F11 để vào menu boot
- Sau khi giao diện cài đặt Windows Server xuất hiện, chọn **Repair your computer**:
![image](https://github.com/user-attachments/assets/732b88ee-f327-4eed-b51a-5a2839927c25)
![image](https://github.com/user-attachments/assets/6ef2aaa7-e432-44c4-b3a4-dfc281b884ce)

- Tại giao diện **Choose an option**, chọn *Troubleshoot*, sau đó chọn Command Prompt:
![image](https://github.com/user-attachments/assets/197d8487-b067-4be7-b017-d93778fc3a77)
![image](https://github.com/user-attachments/assets/d28848f7-27b4-4c25-bf04-db4071c2a363)

## 2.2. Đổi tên vào sao chép file:
- Trong cửa sổ Command Prompt, nhập các lệnh sau và nhấn Enter sau mỗi lệnh:
```
E:
cd windows\system32
ren Utilman.exe Utilman.old
copy cmd.exe Utilman.exe
```
![image](https://github.com/user-attachments/assets/c4f8981f-f77e-4b3e-b939-5b1c35ea6d84)

- Thoát giao diện Command Prompt với lệnh `exit`
- Chọn **Continue** để vào Windows Server 2019:
![image](https://github.com/user-attachments/assets/68d5eb59-824b-4c24-8473-745809772c44)

- Đặt password mới sau khi khởi động lại, nhấn tổ hợp `Windows U` hoặc nhấn chuột vào đây:
![image](https://github.com/user-attachments/assets/d7463661-e757-4b66-9be5-6e9721ce9dc7)

- Đặt lại password, dùng lệnh:
```
net user administrator new_password
```
![image](https://github.com/user-attachments/assets/9591775c-5909-4a24-8626-b105021abd4b)

- Đăng nhập lại với mật khẩu vừa thay đổi:
![image](https://github.com/user-attachments/assets/16f356cd-cbf6-458e-b2f9-36299efaddf8)

- Đăng nhập thành công.
