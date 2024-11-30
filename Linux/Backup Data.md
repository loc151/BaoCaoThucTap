# `rsync` hoặc đồng bộ hóa từ xa là một tiện ích phần mềm cho các hệ thống giống Unix đồng bộ hóa hiệu quả các tệp và thư mục giữa hai máy chủ hoặc máy. 
- Một là nguồn hoặc máy chủ cục bộ mà từ đó các tệp sẽ được đồng bộ hóa, cái còn lại là máy chủ từ xa, trên đó quá trình đồng bộ hóa sẽ diễn ra.
- Về cơ bản có hai cách trong đó rsync can copy/sync data:
  - Sao chép/đồng bộ đến/từ 1 máy chủ khác qua bất kỳ trình kết nối từ xa như ssh.
  - Sao chép/đồng bộ hoá thông qua `rsync daemon` bằng TCP
- Cú pháp: `rsync local-file user@remote-host:remote-file`

## Cách hoạt động: 
- Rsync trước tiên sẽ sử dụng SSH để kết nối với user máy chủ từ xa và sẽ yêu cầu mật khẩu.
- Sau khi kết nối, nó sẽ gọi rsync của máy chủ từ xa, sau đó hai chương trình sẽ xác định những phần nào của tệp cục bộ cần được sao chép để tệp từ xa khớp với tệp cục bộ.
- Lưu ý hành vi sau của rsync:
  - Các tập tin không tồn tại trên máy chủ từ xa sẽ được sao chép.
  - Các tập tin đã được cập nhật sẽ được đồng bộ hóa, rsync sẽ chỉ sao chép các phần đã thay đổi của tập tin vào máy chủ từ xa.
  - Các tập tin giống hệt nhau sẽ không được sao chép vào máy chủ từ xa.

## Cấu trúc: 
```
rsync [options] source [destination]
```

- Các tuỳ chọn thông dụng:

|Options|Description|
|-----|-------------|
|-a, --archive|Điều này tương đương với việc sử dụng `-rlptgoD`. Chế độ lưu trữ bao gồm tất cả các tùy chọn cần thiết như sao chép tệp đệ quy, bảo toàn hầu hết mọi thứ (như liên kết tượng trưng, quyền truy cập tệp, quyền sở hữu người dùng & nhóm và dấu thời gian).|
|-v, --verbose|Theo mặc định, rsync hoạt động âm thầm. Sử dụng tùy chọn `-v` cung cấp thông tin về các tệp được chuyển và tóm tắt ở cuối. Thêm hai tùy chọn "-v" cung cấp cập nhật trạng thái về truyền delta và các tệp bị bỏ qua, cùng với nhiều thông tin hơn ở cuối. Nhiều tùy chọn `-v` thường được sử dụng để gỡ lỗi rsync.|
|-h, --human-readable format|Đầu ra ở định dạng con người có thể đọc được|
|-z, --compress|Nén dữ liệu tệp trong quá trình truyền|

### 1. Sử dụng `rsync` làm lệnh hiển thị danh sách: 
- Tương tự như lệnh `ls -l`, sử dụng lệnh như sau: `rsync [directory]`
![image](https://github.com/user-attachments/assets/5d75fc02-c3c0-437d-8969-40b8c79d6660)
