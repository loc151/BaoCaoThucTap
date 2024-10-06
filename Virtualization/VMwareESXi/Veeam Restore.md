## Hướng Dẫn Khôi Phục (Restore) Bằng Veeam Backup & Replication

## 1. Yêu Cầu Trước Khi Khôi Phục
- Đảm bảo có bản sao lưu hợp lệ trong **Backup Repository**.
- Đảm bảo hệ thống đích có đủ tài nguyên để khôi phục các máy ảo hoặc dữ liệu.
- Kiểm tra kết nối giữa **Veeam Backup Server** và hệ thống ảo hoá (ví dụ: ESXi).
- Đảm bảo rằng repository không bị lỗi hoặc mất kết nối.

## 2. Các Phương Pháp Khôi Phục
- **Full VM Recovery (Khôi Phục Máy Ảo Toàn Bộ):** Khôi phục toàn bộ máy ảo từ bản sao lưu.
- **File-Level Recovery (Khôi Phục Từng File):** Khôi phục từng file hoặc thư mục riêng lẻ từ bản sao lưu.
- **Instant VM Recovery:** Khởi chạy máy ảo trực tiếp từ bản sao lưu mà không cần khôi phục đầy đủ.

## 3. Khôi Phục Máy Ảo (Full VM Recovery)

3.1. **Mở Veeam Backup & Replication:**
   - Khởi chạy **Veeam Backup & Replication Console** trên máy chủ quản lý.

3.2. **Chọn Máy Ảo Cần Khôi Phục:**
   - Vào **Home** > **Backups** > **Disk** để xem danh sách các bản sao lưu.
   - Nhấp chuột phải vào bản sao lưu của máy ảo mà bạn muốn khôi phục và chọn **Restore entire VM**.
![image](https://github.com/user-attachments/assets/cc5a073f-0722-42ec-9780-57bc748171f4)

3.3. **Chọn Loại Khôi Phục:**
   - Chọn phương thức khôi phục phù hợp, ví dụ: **Restore to the original location** (Khôi phục đến vị trí ban đầu) hoặc **Restore to a new location** (Khôi phục đến vị trí mới).
![image](https://github.com/user-attachments/assets/01b3eac9-04de-41c9-b776-784cbbb17662)
![image](https://github.com/user-attachments/assets/69f43d67-d785-4006-a20f-8f1503bf1fcb)

3.4. **Cấu Hình Khôi Phục:**
   - Nếu chọn khôi phục đến vị trí mới, bạn sẽ phải nhập lại thông tin như tên máy ảo mới, chọn ESXi host và datastore để lưu trữ.

3.5. **Chạy Quá Trình Khôi Phục:**
   - Xác nhận các lựa chọn và nhấn **Finish** để bắt đầu quá trình khôi phục máy ảo.
![image](https://github.com/user-attachments/assets/f2c0e323-cc65-433a-8f36-7db1e1837bfe)
![image](https://github.com/user-attachments/assets/fe8a614a-d3ce-4062-9e02-7366049197c0)
![image](https://github.com/user-attachments/assets/2a94c2de-6c33-4bad-929b-1b131618dc43)

## 4. Kết quả kiểm thử:
- Kiểm thử trên hệ điều hành CentOS 7, chỉnh sửa hostname và thêm user vào. Tiến hành backup cấu hình này như trên

![image](https://github.com/user-attachments/assets/7c98a944-468c-4937-bc42-d7f7c1cc5853)

- Kết quả sau khi backup. Hostname lúc này đã trở về `localhost` và không còn user `anhldl` vừa mới tạo ở trên.

![image](https://github.com/user-attachments/assets/87298bd0-3854-41b5-b9a5-efad6df6df2a)
