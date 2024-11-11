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
- ![image](https://github.com/user-attachments/assets/b2d2bca0-df6e-49e6-82f4-b6031715f5b4)

- Kiểm tra kết nối của cấu hình mạng cục bộ:
![image](https://github.com/user-attachments/assets/50771732-ad18-40a7-9243-1e9575c4f956)

- Kiểm tra cấu hình mạng:
- ![image](https://github.com/user-attachments/assets/542d99fd-3479-4f55-8359-f015f6253455)

- Kiểm tra cấu hình DNS:
![image](https://github.com/user-attachments/assets/b86d3514-69ae-4f43-9134-78dc20a9dff5)

- Kiểm tra đường đi của các gói tin: `traceroute`
![image](https://github.com/user-attachments/assets/407b3f9e-c548-4624-ad9a-b0299bac7ddb)

- Lệnh **route**: sử dụng để hiển thị và thao tác với bảng định tuyến của hệ thống. Bảng định tuyến xác định cách các gói tin được chuyển tiếp từ máy tính nguồn đến các mạng khác
  - Hiển thị bảng định tuyến: `route -n`
  ![image](https://github.com/user-attachments/assets/bbb96dd0-7bd4-419f-9229-89582901ea10)

  - Thêm route mới: `sudo route add -net network_address netmask subnet_mask gw gateway_address`
  - Xoá route: `sudo route del -net network_address netmask subnet_mask`

## 2. Các tệp cấu hình mạng:
- `/etc/init.d/network` (Ubuntu 18 trở xuống) hoặc `/etc/network` (Ubuntu 18 trở lên): Bật/tắt/khởi động lại dịch vụ mạng
- `etc/network/interfaces` (Ubuntu 18 trở xuống) hoặc `/etc/netplan/*.yaml` (18 trở lên): Cấu hình chung về mạng 
- `/etc/hostname`: Chứa tên máy chủ (hostname) của hệ thống
- `/etc/hosts`: Ánh xạ tên máy chủ đến địa chỉ IP. Nó được sử dụng để giải quyết vấn đề tên máy chủ cục bộ mà không cần truy vấn DNS
![image](https://github.com/user-attachments/assets/c70e0f5b-151a-48f5-9040-70b8cf1d8aac)

- `/etc/resolv.conf`: Chứa thông tin về máy chủ DNS mà hệ thống sẽ sử dụng để giải quyết tên miền:
![image](https://github.com/user-attachments/assets/c242593b-d31a-4a54-80b0-5939a5f0a89f)

- `/etc/nsswitch` hoặc `/etc/nsswitch.conf`: Thông tin về dịch vụ tên và thứ tự truy vấn của các nguồn:
![image](https://github.com/user-attachments/assets/655163c9-e685-4cea-9044-7dfec30f876e)
