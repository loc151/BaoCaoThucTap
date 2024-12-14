# Cấu hình NTP Server trên Windows Server 2022

## Chuẩn bị:
- Một máy sử dụng hệ điều hành Windows Server 2022 đóng vài trò NTP Server
- Một máy sử dụng hệ điều hành Windows đóng vai trò NTP Client

## Cấu hình:
### Bước 1: Dừng dịch vụ Windows Time trong Services
- Mở **Task Manager** > **Services**. Tìm đến service có tên là **W32Time**, nhấp chuột phải và chọn **Stop**.
![image](https://github.com/user-attachments/assets/2af6d4dd-57e3-4441-8e91-998257477bb8)

### Buớc 2: Chỉnh sửa W32time trong regedit:
- **Mở Registry Editor**: Nhấn tổ hợp **Windows + R**, gõ `regedit` và nhấn OK
- Trong bảng **Registry Editor**, tìm theo đường dẫn sau:
```shell
HKEY_LOCAL_MACHINE > SYSTEM > CurrentControlSet > Services > W32Time > TimeProviders > NtpServer
```
- Ở mục **Enabled**, chọn **Modify**:
![image](https://github.com/user-attachments/assets/d6456656-2b5a-476f-822e-c5c2e5b1a71b)
- Sửa **Value data** từ 0 thành 1, nhấn OK để xác nhận:
![image](https://github.com/user-attachments/assets/34069aaf-02f7-4735-8068-f81fc853df9f)
- Thay đổi giá trị AnnounceFlags: truy cập **W23Time -> Config -> AnnouceFlags**, chọn **Modify** và sửa **ValueData** từ a thành 5:
![image](https://github.com/user-attachments/assets/73f3164f-ad41-4fbb-8a4b-9cfa1e427a5e)

### Bước 3: Khởi động lại NTP Service:
- **Cách 1**: Vào **Task Manager -> Services -> W32Time -> Start**:
![image](https://github.com/user-attachments/assets/2be13ae4-a8f8-4049-956e-7d623c04a34e)

- **Cách 2**: Thực thi các lệnh sau trong **CMD**:
```
net stop w32time
net start w32time
```
![image](https://github.com/user-attachments/assets/4cfe0513-0959-4faa-a652-faf49afef110)

### Bước 4: Cấu hình tường lửa Firewall:
#### Cách 1 (không khuyến khích): Tắt firewall: 
- Vào **Control Panel -> Windows Defender Firewall -> Turn off Windows Defender Firewall**
- Tắt cả 2 **Private & Public Network**
![image](https://github.com/user-attachments/assets/88295f6b-123e-4f06-b362-e5f15d210ef5)

#### Cách 2 (Ưu tiên): Mở cổng 123/UDP:
- Vào **Windows Defender Firewall -> Advanced settings -> Inbound Rules -> New Rule**:
![image](https://github.com/user-attachments/assets/77731b5e-fdb5-4913-9dad-a80ee879d179)
- Ở mục **Rule Type**, chọn **Port**
- Ở mục **Protocol and Ports**, chọn **UDP** với **Specific local ports = 123**:
![image](https://github.com/user-attachments/assets/f253d985-2381-4e77-8baa-111b7808f578)
- Ở mục **Action**, chọn **Allow the connection**
- Ở mục **Profile**, chọn các kết nối áp dụng luật (Domain, Private hoặc Public)
- Đặt tên cho luật và hoàn tất việc thiết lập
- Sau khi hoàn thành thiết lập port cho NTP, Rule sẽ thêm như sau:
![image](https://github.com/user-attachments/assets/8186eb37-3dfe-4594-a5be-e61d7641f1a9)

### Bước 5: Kiểm tra hoạt động của NTP:
- **Lưu ý**: Chỉnh **Time Zone** chính xác theo khu vực. Với NTP server tại Việt Nam, múi giờ sẽ là *UTC+7:00 Bangkok , Hanoi , Jakarta*
- Vào **Control Panel -> Date and Time -> Internet Time -> Change settings**:
![image](https://github.com/user-attachments/assets/f0f8c301-68ab-4064-8df4-2c9d46a2ae40)
- Chọn server phù hợp và chọn **Update now**:
- Sau khi chọn **Update now**, cần chờ vài giây để xác nhận cập nhật thời gian của đồng hồ. Hệ thống sẽ thông báo thành công cùng mốc thời gian hoàn thành: <p>
![image](https://github.com/user-attachments/assets/c9059437-2697-4df7-ba85-c642d2b19438)

### Bước 6: Tại NTP Client:
- Vào **Date and Time -> Internet Time**, chọn server cần đồng bộ chính là địa chỉ IP của NTP server vừa cấu hình (172.16.2.50): <p>
![image](https://github.com/user-attachments/assets/e4f2c9d3-167a-4d19-a333-3bdbde825b2f)
- Sau khi đồng bộ hệ thống sẽ trả về thông báo thành công:
![image](https://github.com/user-attachments/assets/03c8abb2-c1e9-4fb1-bbd0-042cf8e1885f)
- Xem số thời gian chênh lệch cần cộng trừ giữa các thiết bị với nhau:
```shell
w32tm /stripchart /computer:domainname_OR_ipaddress /dataonly /samples:5
```
- Thay domain name hoặc IP của server cần kiểm tra vào lệnh, sample sẽ là số lần chạy, kết quả trả về hiển thị như sau:
![image](https://github.com/user-attachments/assets/12d89bf4-0af8-4849-837d-e95540fd9a6c)
- Kết quả trên cho thấy máy client đã đồng bộ hoá thời gian với NTP server
