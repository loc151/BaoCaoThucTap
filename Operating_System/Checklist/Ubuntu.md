# Checklist Ubuntu
## 1. Đổi cổng truy cập từ xa SSH:
- Sử dụng lệnh sau để truy cập file cấu hình:
```shell
nano /etc/ssh/sshd_config
```
- Sửa port 22 thành port 222
![image](https://github.com/user-attachments/assets/23d8418a-f11b-45cb-baf9-b493f35857b4)
- Nhấn Ctrl X và nhấn Y để lưu cấu hình 
- Sử dụng lệnh sau cài lại cấu hình ssh
```
sudo systemctl restart sshd
```
- Dùng lệnh sau để kiểm tra lại cấu hình ssh
```
sudo ss -tulp | grep ssh
```
![image](https://github.com/user-attachments/assets/8f9d4998-e527-411d-b9cf-8aa6f07160e4)

- Dùng MobaXstrem để truy cập SSH với cổng 222:
![image](https://github.com/user-attachments/assets/10dd9f3b-6555-494c-8436-3a90d35cb58a)

- Đăng nhập từ xa thành công với user *locanh*:
![image](https://github.com/user-attachments/assets/1816c887-9192-44a9-a743-4e053cb8a0be)


## 2. Đăng nhập bằng user khác:
- Tạo user mới:
![image](https://github.com/user-attachments/assets/406b4182-bdad-4f31-a7a2-71710ea11a75)

- Gán quyền sudo cho user mới:
```
sudo usermod -aG sudo <tên_user>
```
- Kiểm tra xem user được tạo đã có quyền sudo chưa.
```
sudo -l
```
- Nếu user có quyền sudo, lệnh này sẽ liệt kê các quyền sudo của user đó
![image](https://github.com/user-attachments/assets/3bbfa0d8-577c-47cc-bb8d-1ea6fa864e56)

## 3. Vô hiệu hoá tài khoản root: 
### 3.1. Khoá mật khẩu root: 
- Chạy lệnh sau để khoá mật khẩu, ngăn không cho đăng nhập trực tiếp vào tài khoản root (trong trường hợp này là anhldl):
```
sudo passwd -l root
```

### 3.2. Vô hiệu hoá đăng nhập SSH cho root:
- Mở file cấu hình SSH:
```
sudo nano /etc/ssh/sshd_config
```
- Tìm dòng `PermitRootLogin` sửa thành:
```
PermitRootLogin no
```
![image](https://github.com/user-attachments/assets/b271380c-150e-4bf7-957a-71a0465ef177)

- Lưu và thoát: nhấn `Ctrl X`, nhấn Y để lưu các thay đổi
- Khởi động lại dịch vụ SSH

### 3.3. Đăng nhập SSH để kiểm tra cấu hình:
- Sử dụng **MobaXstrem** để truy cập từ xa SSH với tài khoản root (anhldl). Nếu có thông báo `Access is denied` tức là tài khoản đó đã chặn không cho truy cập từ xa 
![image](https://github.com/user-attachments/assets/5a2f845e-0c7c-43d6-a09c-cc2ac3abc9b9)

- Sử dụng user khác để truy cập từ xa:
![image](https://github.com/user-attachments/assets/8d787ad8-f8cd-498d-828e-024a65527f53)

### 3.4. Cho phép hoặc chặn địa chỉ IP truy cập: 
