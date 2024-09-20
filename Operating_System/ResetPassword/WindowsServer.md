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
- Sau khi giao diện cài đặt Windows Server xuất hiện, chọn **Repair your computer**
- Tại giao diện **Choose an option**, chọn *Troubleshoot*, sau đó chọn Command Prompt
![image](https://github.com/user-attachments/assets/d28848f7-27b4-4c25-bf04-db4071c2a363)

## 2.2. Đổi tên vào sao chép file:
- Trong cửa sổ Command Prompt, nhập các lệnh sau và nhấn Enter sau mỗi lệnh:
```
c:
cd windows\system32
ren Utilman.exe Utilman.exe.old
copy cmd.exe Utilman.exe
```
