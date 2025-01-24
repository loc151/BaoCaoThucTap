# Hướng Dẫn Cài Đặt RAID 1 Trên Máy Chủ Dell PowerEdge R620

RAID 1 là một cấu hình RAID phổ biến cung cấp khả năng dự phòng dữ liệu và hiệu suất đọc tốt. Hướng dẫn này sẽ giúp bạn cài đặt RAID 1 trên máy chủ Dell PowerEdge R620.

## Bước 1: Truy Cập Dell PERC

1. **Khởi Động và Truy Cập PERC**:
   - Khi máy chủ khởi động, bạn sẽ thấy thông báo của Dell PERC. Ngay khi máy chủ bắt đầu khởi động (trước khi vào hệ điều hành), nhấn phím **Ctrl + R** để vào giao diện cấu hình RAID.

   ![Dell PERC Screen](https://github.com/cuongnvvietis/NhanHoa/blob/main/Docs/Esxi/Picture/Raid/Screenshot_6.png)

## Bước 2: Tạo RAID 1

1. **Chọn Create Virtual Disk**:
   - Trong giao diện Dell PERC, nhấn **F2** chọn **Create Virtual Disk** để bắt đầu cấu hình RAID.
![image](https://github.com/user-attachments/assets/1cad9ebf-5012-4cc2-90d1-eb0de68567f1)


2. **Chọn RAID Level**:
   - Trong màn hình tiếp theo, chọn **RAID 1** từ danh sách các cấp RAID.
![image](https://github.com/user-attachments/assets/81865271-e966-4f3d-af00-521005a3a3b7)

3. **Chọn Các Ổ Đĩa**:
   - Chọn ít nhất hai ổ đĩa mà bạn muốn sử dụng cho RAID 1. Đảm bảo các ổ đĩa đã được kết nối và nhận diện bởi PERC.
![image](https://github.com/user-attachments/assets/ca29baf6-1967-41c5-8156-97c9675d6cba)


4. **Xác Nhận Cấu Hình**:
   - Kiểm tra lại cấu hình RAID 1 của bạn và chọn **OK** để xác nhận và tạo RAID 1.
![image](https://github.com/user-attachments/assets/111cbc4a-5e7f-4cec-bf9a-9824c818d2aa)

## Bước 3: Lưu Cài Đặt và Khởi Động Lại Máy Chủ

1. **Lưu Cài Đặt**:
   - Sau khi cấu hình xong, chọn **Save** và **Exit** để lưu các thay đổi.

2. **Khởi Động Lại Máy Chủ**:
   - Nhấn **Control + Alt + Delete** để khởi động lại máy chủ và các thay đổi có hiệu lực. 
