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
systemctl restart sshd
```
- Dùng lệnh sau để kiểm tra lại cấu hình ssh
```
sudo ss -tulp | grep ssh
```
![image](https://github.com/user-attachments/assets/8f9d4998-e527-411d-b9cf-8aa6f07160e4)

- Dùng MobaXstrem để truy cập SSH với cổng 222:
![image](https://github.com/user-attachments/assets/10dd9f3b-6555-494c-8436-3a90d35cb58a)

## 2. Đăng nhập bằng user khác:
- Tạo user mới:
![image](https://github.com/user-attachments/assets/406b4182-bdad-4f31-a7a2-71710ea11a75)

- Gán quyền sudo cho user mới:
```
sudo usermod -aG sudo <tên_user>
```
- Kiểm tra xem user được tạo đã có quyền sudo chưa.
