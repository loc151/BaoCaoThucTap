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
