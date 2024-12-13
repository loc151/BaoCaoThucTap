# Cài đặt NTP Server trên Ubuntu 22.04
## Bước 1: Kiểm tra giờ hiện tại của server và cập nhật giờ địa phương:
```
date
timedatectl
timedatectl set-timezone Asia/Ho_Chi_Minh
```
![image](https://github.com/user-attachments/assets/e3bc714d-2b16-4105-a000-f16679bcbd8c)

## Bước 2: Cập nhật danh sách các gói phần mềm và cài đặt NTP Server:
```
sudo apt update
sudo apt install ntp -y
```

## Bước 3: Kiểm tra cài đặt:
- Xác minh xem cài đặt NTP đã thành công hay không:
```
sntp --version
```
![image](https://github.com/user-attachments/assets/11353246-8b6b-4e24-b6e4-44e7bf941475)

## Bước 4: Cấu hình NTP Server: 
```
sudo nano /etc/ntp.conf
```

## Bước 5: Thay thế các dòng NTP pool bằng các dòng phù hợp với khu vực hiện tại:
```
pool 0.vn.pool.ntp.org iburst
pool 1.vn.pool.ntp.org iburst
pool 2.vn.pool.ntp.org iburst
pool 3.vn.pool.ntp.org iburst
```
![image](https://github.com/user-attachments/assets/325546aa-809c-45b0-b9af-7d3e16056b92)

## Bước 6: Lưu tệp cấu hình và khởi động lại dịch vụ NTP:
```
sudo systemctl restart ntp
```

## Bước 7: Kiểm tra trạng thái của NTP:
```
sudo systemctl status ntp
```
![image](https://github.com/user-attachments/assets/927a812b-efd2-4f65-a614-3b9487448375)

## Bước 8: Cấu hình tường lửa cho phép lưu lượng NTP đi qua cổng 123/UDP:
```
sudo ufw allow 123/udp
```

## Bước 9: Kiểm tra đồng bộ hoá thời gian:
```
ntpq -p
```
![image](https://github.com/user-attachments/assets/20e03b01-df4d-4f65-987f-53fb351ac319)

- Trong đó:
  - **remote**: Tên hoặc địa chỉ IP của máy chủ NTP.
  - **refid**: Tham chiếu ID của máy chủ NTP.
  - **st**: Stratum của máy chủ NTP (mức độ gần gũi với nguồn thời gian chính xác).
  - **t**: Loại kết nối (u: unicast, b: broadcast, l: local, p: pool).
  - **when**: Thời gian kể từ lần đồng bộ hóa cuối cùng (tính bằng giây).
  - **poll**: Khoảng thời gian giữa các lần đồng bộ hóa (tính bằng giây).
  - **reach**: Trạng thái tiếp cận của máy chủ NTP (giá trị nhị phân).
  - **delay**: Độ trễ của kết nối (tính bằng mili giây).
  - **offset**: Độ lệch thời gian giữa máy chủ NTP và hệ thống của bạn (tính bằng mili giây).
  - **jitter**: Độ dao động của độ trễ (tính bằng mili giây).


![image](https://github.com/user-attachments/assets/28cdd90c-bf2b-4e21-870f-32c323517a67)
![image](https://github.com/user-attachments/assets/5576269c-8c0c-4c3e-bece-536b7ae314c4)
![image](https://github.com/user-attachments/assets/49d4de24-f0e2-46da-89ab-4646ea70c9db)
![image](https://github.com/user-attachments/assets/3457853d-fb50-4448-a3d2-19b0fb02d106)


 
