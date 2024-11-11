# Cấu hình hệ thống: 
## 1. Cấu hình kết nối mạng:
### Kiểm tra thông tin NIC (Network Interface Card)
- Kiểm tra thông tin các card mạng hiện có trên hệ thống
```
ip
ifconfig
```
- Lưu ý: Nếu ifconfig không có sẵn trên hệ thống, sử dụng lệnh sau để cài đặt:
```
sudo apt install net-tools
```

![image](https://github.com/user-attachments/assets/730363d7-a7c7-4a12-969c-20ef30bfeb63)

![image](https://github.com/user-attachments/assets/a0fd886e-79c9-44e0-81f4-4970371ab1f4)

- Cấu hình IP tĩnh: Mở tệp sau để cấu hình các thông số mạng như tên card mạng, địa chỉ ip, gateway, ... Cấu hình xong cần lưu lại để hệ thống áp dụng cấu hình mạng.

```sh
sudo nano /etc/network/interfaces                  #Ubuntu/Debian
sudo vi /etc/sysconfig/network-scripts/ifcfg-eth0  #CentOS/RHEL   
```

### Kiểm tra kết nối mạng:
- Sử dụng lệnh "ping" để kiểm tra kết nối mạng
- Kiểm tra kết nối mạng của cấu hình NIC:
![image](https://github.com/user-attachments/assets/b2d2bca0-df6e-49e6-82f4-b6031715f5b4)

- Kiểm tra kết nối của cấu hình mạng cục bộ:
![image](https://github.com/user-attachments/assets/50771732-ad18-40a7-9243-1e9575c4f956)

- Kiểm tra cấu hình mạng:
![image](https://github.com/user-attachments/assets/542d99fd-3479-4f55-8359-f015f6253455)

- Kiểm tra cấu hình DNS:
![image](https://github.com/user-attachments/assets/b86d3514-69ae-4f43-9134-78dc20a9dff5)
