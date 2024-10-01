## 1. Thêm kho dữ liệu mới:
![image](https://github.com/user-attachments/assets/1f9acbcd-6340-483b-89a8-6783ab391ce6)

![image](https://github.com/user-attachments/assets/baf544f8-acf3-4d4e-bfdf-250c89690cb8)

![image](https://github.com/user-attachments/assets/2f76e91f-aefc-4613-860a-f6a6ce1232e5)

![image](https://github.com/user-attachments/assets/a6dd308e-ed4a-4846-9e94-def4c8f58238)






## 2. Cách sửa lỗi: Failed to create VMFS datastore - Cannot change the host configuration file:
- Lỗi "Không thể thay đổi cấu hình máy chủ" khi cố gắng tạo kho dữ liệu VMFS. Sự cố này có thể phát sinh do một số lý do, chẳng hạn như phân vùng hiện có trên đĩa, kích thước khối không chính xác hoặc đĩa được sử dụng cho các mục đích khác như tệp scratch hoặc swap. Sau đây là các cách sửa lỗi:
## 2.1. Bật truy cập từ xa cho ESXi host:
- Tại giao diện web của ESXi, vào phần **Manage** -> **Service**, tìm dịch vụ có tên **TSM-SSH** và nhấn **Start** để khởi động dịch vụ này.
![image](https://github.com/user-attachments/assets/73dde756-4c29-43fb-878c-81cf7d45b0f6)

- Kết nối với ESXi host sử dụng SSH, trong trường hợp này sẽ sử dụng MobaXstrem:
![image](https://github.com/user-attachments/assets/02ac02e9-34b6-4f52-9967-5c9cc084c8c6)

## 2.2. Nhận diện các ổ đĩa gây ra vấn đề: 
- Dùng lệnh sau để hiển thị tất cả các ổ đĩa:
```
ls -lha /vmfs/devices/disks/
```
- Ở đây, ổ đĩa gây ra sự cố là `naa.6b083fe0ea52fb002e8e701f065993f6`
![image](https://github.com/user-attachments/assets/90d2ce8c-482f-4ac0-9bcd-d6cb4d6f195a)

## 2.3. Kiểm tra bảng phân vùng:
- Sử dụng lệnh sau để kiểm tra bảng phân vùng của ổ đĩa:
```
partedUtil getptbl /vmfs/devices/disks/<disk_ID>
```
- Trong đó: `<disk_ID>` là tên ổ đĩa cần kiểm tra lỗi:
![image](https://github.com/user-attachments/assets/b674baf1-2ba0-424e-83c6-e354a89a5589)

## 2.4. Thiết lập lại bảng phân vùng:
- Sử dụng lệnh sau để thiết lập lại bảng phân vùng theo kiểu `msdos`.
```
partedUtil setptbl /vmfs/devices/disks/<disk_ID> msdos
```
- Trong đó: `<disk_ID>` là tên ổ đĩa cần được thiết lập lại:
![image](https://github.com/user-attachments/assets/2c2dc459-748a-4794-bb31-97d3c4d4553e)

## 2.5. Thêm lại kho dữ liệu:
- Quay lại vSphere client và thử thêm đĩa làm kho dữ liệu VMFS:
- Làm lại các bước ở mục 1 và thêm datastore mới thành công:
![image](https://github.com/user-attachments/assets/c8690536-1fa0-411b-9f95-927d5dbe8f2c)
