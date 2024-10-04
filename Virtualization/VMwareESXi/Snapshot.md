# Snapshot (trong ESXi): là 1 bản sao của tệp đĩa máy ảo (VMDK) tại 1 thời điểm nhất định. Nó ghi lại trạng thái của máy ảo, bao gồm cả bộ nhớ, các tệp đĩa và các thiết lập cấu hình:

## Lợi ích của Snapshot:
1. **Phục hồi nhanh chóng**: Giúp khôi phục máy ảo về trạng thái trước đó nếu xảy ra sự cố
2. **Thử nghiệm và phát triển**: Dễ dàng thử nghiệm các cấu hình mới mà không lo mất dữ liệu
3. **Tiết kiệm thời gian**: Tránh phải cài đặt lại máy ảo từ đầu khi gặp lỗi

## Lưu ý khi sử dụng snapshot: 
1. **Không nên giữ snapshot quá lâu**: Snapshot có thể chiếm nhiều dung lượng lưu trữ và ảnh hưởng đến hiệu suất
2. **Sử dụng snapshot cho các mục đích ngắn hạn**: Không nên sử dụng snapshot như 1 giải pháp sao lưu dài hạn

## 1. Tạo Snapshot: 
- Chọn 1 OS bất kỳ ở **Virtual Machines** trong ESXi Host, ở mục **Action**, chọn **Snapshots**, chọn **Take snapshot**:

![image](https://github.com/user-attachments/assets/cd6de3cc-31a5-4dba-9274-bbbbe3485710)

- Cung cấp thông tin về snapshot, bao gồm tên và mô tả (nếu cần). Chọn các tuỳ chọn bổ sung như *Snapshot the virtual machine’s memory* và *Quiesce guest file system* nếu cần:

![image](https://github.com/user-attachments/assets/e2529ce1-092b-44f3-a3b4-eaa79709e92d)

- Chọn **Take snapshot** để hoàn tất bước tạo snapshot.

## 2. Quản lý snapshot:
- **Xem danh sách snapshot**: nhấp chuột phải vào máy ảo và chọn **Snapshots > Manage Snapshots**

![image](https://github.com/user-attachments/assets/a3a6c883-758c-4743-a36f-24d4aceca3e9)

- Lúc này, danh sách các snapshot đã lưu sẽ hiện ra:

![image](https://github.com/user-attachments/assets/494ebc89-50ca-4cd2-9bb8-f3c7c9ed3ab6)

- **Khôi phục hoặc xoá snapshot**: Trong giao diện quản lý snapshot, có thể chọn để khôi phục (restore) hoặc xóa (delete) snapshot. Chọn snapshot cần khôi phục hoặc xóa, sau đó nhấp vào **Restore** hoặc **Delete**.
![image](https://github.com/user-attachments/assets/4a9b6c4e-5777-41d5-ad46-87bfefe3f1a9)
