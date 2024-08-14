# Báo cáo thực tập 2
## Công cụ làm việc trong quá trình thực tập
### Chat - Trao đổi: Qua Telegram (chủ yếu) hoặc Zalo.
### Github: Cách sử dụng Github:
1. Tạo tài khoản Git
2. Tạo Repository
3. Gửi link Repository 
### Cách sử dụng markdown trong Github:
1. Văn bản thuần:
- Heading: Sử dụng các đánh dấu `<h1>, <h2>, ..., <h6>` hoặc dùng dấu # tương ứng.
- Paragraph: Sử dụng đánh dấu `<p>` để xuống dòng giữa các văn bản.
- Italic: Sử dụng đánh dấu `<i>` hoặc thêm dấu `*`, `_` trước và sau từ cần in nghiêng.
- Bold: Sử dụng đánh dấu `<b>` hoặc thêm dấu `**`,``
- Italic & Bold: Sử dụng dấu `***` hoặc `___`
- Strikethrough: Sử dụng dấu `~` trước và sau từ cần gạch giữa
- Inline code: dùng 2 dấu ` ở trước và sau từ đó

2. Các khối:
- Blockquote: thêm dấu `>` vào trước mỗi dòng trích dẫn
- Ordered List: thêm các số, dấu chấm trước nội dung (dùng tab để phân cấp)
- Unordered List: thêm dấu `*` hoặc `-`hoặc `+` trước nội dung (dùng  tab để phân cấp)
- Block Code: Dùng 3 dấu ` ở trước và sau đoạn code đó
- Table: Ngăn cách bởi dấu | và các đầu bảng với thân bảng bằng :---

3. Đặc biệt:
- Đường kẻ ngang: sử dụng 3 dấu * hoặc - hoặc _ trên 1 dòng
- Liên kết:
  - Trực tiếp: Paste link như bình thường
  - Gián tiếp: dùng `[text](link)`
- Hình ảnh:
  - Trực tiếp: Paste ảnh như bình thường
  - Gián tiếp: dùng `![text](link image)` hoặc `![](link image);`
- Icon: sử dụng `:[icon]`
- Checkbox: đánh dấu như list và thêm 1 cặp ngoặc vuông `[]` hoặc `[x]`
- Escape markdown: thêm dấu `\` trước những kí hiệu
  
### Phần mềm SSH:
1. `PuTTY:` là một phần mềm mã nguồn mở miễn phí được sử dụng để kết nối và quản lý các thiết bị từ xa thông qua giao thức mạng như SSH, Telnet, rlogin và serial
- Cài đặt PuTTY: tải phiên bản mới nhất trên trang web
- Thu thập thông tin kết nối: cần biết ít nhất 4 thông tin:
  - IP server
  - SSH Port (port 22)
  - SSH username
  - SSH password
- Kết nối với server:
  - Khi kết nối lần đầu với server, có thể thấy cảnh báo về host key của server không được lưu trữ trong registry, ấn `Yes` để kết nối.
  - Sau khi kết nối thành công sẽ xuất hiện một cửa số terminal. Nó sẽ yêu cầu username và password.
  ![image](https://github.com/user-attachments/assets/323ff7ae-dac7-4f07-8358-43921da77323)
  - Sau khi đăng nhập thành công, ta có thể nhập vào cửa sổ terminal. Bây giờ đã kết nối với server và mọi thứ nhập vào cửa sổ terminal sẽ được gửi đến server.
  ![image](https://github.com/user-attachments/assets/05f5bf16-bd0d-4c5e-a277-83d0cd6ba727)
- Ưu điểm: 
  - Miễn phí và phổ biến
  - Giao diện đơn giản
- Nhược điểm:
  - Chỉ kết nối được 1 phiên
  - Không lưu mật khẩu
  - Thiếu tính năng
2. `SecureCRT:` là phần mềm bảo mật dữ liệu quan trọng trong máy tính, cung cấp cho người sử dụng các tính năng và sự lựa chọn hoàn hảo cho việc bảo mật thông tin các dữ liệu quan trọng trên máy tính cá nhân, hỗ trợ người dùng truy cập an toàn từ xa, truyền tập tin và dữ liệu qua đường truyền an toàn chống rò rỉ thông tin đến người nhận
- Cài đặt SecureCRT: tải phiên bản mới nhất trên trang web
- Các thông tin kết nối cần thiết tương tự như `PuTTY`
- Kết nối với server:
  - Sử dụng `Quick Connect`, nhập `Host IP` và username. Sau đó sẽ hiển thị cảnh báo khi kết nối với server, chọn `Accept & Save` để tiếp tục.
  - Sau khi nhập mật khẩu tương ứng, ta đã kết nối thành công tới server và thao tác tương tự PuTTY
  ![image](https://github.com/user-attachments/assets/03777924-e006-4151-877d-b5cdd658ad9c)
- Ưu điểm:
  - Đa chức năng và giao diện nâng cao
  - Tích hợp thanh nút
  - Bảo mật mạnh mẽ
- Nhược điểm:
  - Ghi chú phiên kết nối khó khăn
  - Theo dõi tệp nhật ký tương đối phức tạp

3. `MobaXterm:` là ứng dụng thiết bị đầu cuối đa chức năng, được thiết kế đặc biệt để chạy hđh Windows, hỗ trợ quản lý VPS và máy chủ từ xa thông qua giao thức SSH cũng như nhiều giao thức khác.
- Các tính năng nổi bật:
  - Giao diện đơn giản và thân thiện
  - Hỗ trợ đa giao thức kết nối: tích hợp nhiều giao thức như SSH, Telnet, RDP, FTP, SFTP, X11, ... cho phép người dùng kết nối và quản lý nhiều loại máy chủ từ xa thông qua 1 giao diện duy nhất, tiết kiệm thời gian và công sức.
  - Quản lý nhiều phiên SSH cùng lúc
  - Tích hợp nhiều công cụ và Git
  - Bảo mật cao
- Cài đặt MobaXterm: tải phiên bản mới nhất trên trang chủ
- Các chức năng cơ bản:
  - SSH tới 1 server Linux
  - Kết nối Telnet tới 1 thiết bị mạng
  - Network scan
  - Port scan
### Phần mềm RemoteDesktop
### VmWare Workstation
### Cap màn hình: LightShot
### Vẽ mô hình: Draw.io
