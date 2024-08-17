# Báo cáo thực tập 4
## Networking
### HTTPS: Giao thức được sử dụng để giao tiếp giữa trình duyệt người dùng và trang web. Nó cũng giúp trong việc chuyển dữ liệu. Nó là biến thể an toàn của HTTP. Để làm cho việc truyền dữ liệu an toàn hơn, nó được mã hoá. Mã hoá là cần thiết để đảm bảo an ninh trong khi truyền thông tin nhạy cảm như mật khẩu, thông tin liên lạc
- Cách hoạt động:
  - Thiết lập giao tiếp giữa trình duyệt và máy chủ web. Nó sử dụng giao thức SSL và TLS. Kết nối SSL chịu trách nhiệm mã hoá và giải mã dữ liệu đang được trao đổi để đảm bảo an toàn dữ liệu
  ![image](https://github.com/user-attachments/assets/2f480fe4-a078-478f-962e-1d0fec5844a4)
- Mã hoá:
  - HTTPS truyền dữ liệu ở định dạng được mã hoá. Do đó, HTTPS bảo vệ các trang web khỏi việc phát thông tin của họ theo cách mà bất kỳ ai nghe lén trên mạng để có thể dễ dàng nhìn thấy. Có 2 loại khoá khác nhau được sử dụng để mã hoá
    - Khoá riêng: Được sử dụng để giải mã dữ liệu đã được mã hoá bằng khoá công khai. Nó nằm ở phía máy chủ và được kiểm soát bởi chủ sở hữu của trang web.
    - Khoá công khai: Có bản chất công khai và có thể truy cập được cho tất cả người dùng giao tiếp với server. Khoá riêng được sử dụng để giải mã dữ liệu đã được mã hoá bằng khoá công khai
- Ưu điểm:
  - Giao tiếp an toàn: HTTPS thiết lập 1 liên kết truyền thông an toàn giữa hệ thống giao tiếp bằng cách cung cấp mã hoá trong quá trình truyền
  - Tính toàn vẹn dữ liệu: Bằng cách mã hoá dữ liệu, HTTPS đảm bảo tính toàn vẹn dữ liệu. Ngay cả khi dữ liệu bị xâm phạm tại bất kỳ thời điểm nào, tin tặc sẽ không thể đọc hoặc sửa đổi dữ liệu được trao đổi
  - Quyền riêng tư và bảo mật: HTTPS ngăn kẻ tấn công truy cập dữ liệu được trao đổi thụ động, từ đó bảo vệ quyền riêng tư và bảo mật của người dùng
  - Hiệu suất nhanh hơn: HTTPS mã hoá dữ liệu và giảm kích thước của nó. Kích thước nhỏ hơn để truyền dữ liệu nhanh hơn

### File Transfer Protocol (FTP): là giao thức truyền thông tiêu chuẩn. FTP bảo vệ người dùng khỏi những khác biệt về hệ điều hành, thư mục, cấu trúc, ... và truyển dữ liệu hiệu quả và đáng tin cậy. FTP có thể truyền các tập tin ASCII, EBCDIC, hoặc hình ảnh. 
- Các loại FTP:
  - FTP ẩn danh: được bật trên 1 số trang web có tệp sẵn có để truy cập công cộng. Người dùng có thể truy cập các tệp này mà không cần bất kỳ tên người dùng hoặc mật khẩu nào. Thay vào đó, tên người dùng được đặt thành ẩn danh và mật khẩu mặc định là dành cho client. Quyền truy cập của người dùng rất hạn chế
  - FTP được bảo vệ bằng mật khẩu: Tương tự FTP ẩn danh nhưng điểm thay đổi là việc sử dụng tên người dùng và mật khẩu
  - FTP Secure (FTPS): còn được gọi là FTP SSL. Đây là phiên bản truyền dữ liệu FTP an toàn hơn. Bất cứ khi nào kết nối FTP được thiết lập, TLS sẽ được bật
  - FTP qua SSL/TLS rõ ràng (FTPES): giúp nâng cấp kết nối FTP từ cổng 21 lên kết nối được mã hoá
  - FTP bảo mật (SFTP): không phải là giao thức FTP nhưng nó là tập hợp con của Giao thức SSP, vì nó hoạt động trên cổng 22
- Cách hoạt động:
  - Người dùng phải đăng nhập vào máy chủ FTP, có thể có 1 số máy chủ có thể truy cập nội dung mà không cần đăng nhập, được gọi là FTP ẩn danh
  - Client có thể bắt đầu cuộc trò chuyện với server khi yêu cầu tải xuống tệp
  - Người dùng có thể bắt đầu các chức năng khác nhau như tải lên, xoá, đổi tên, sao chép, ... trên server
  - FTP có thể hoạt động trên các chế độ khác nhau như chế độ Active hoặc Passive
  ![image](https://github.com/user-attachments/assets/345c624e-69f8-49eb-9b76-f0095641a9a0)
- Các loại kết nối trong FTP:
  - Kiểm soát kết nối: FTP sử dụng kết nối điều khiển để gửi thông tin điều khiển như nhận dạng người dùng, mật khẩu, lệnh truy xuất, ... Kết nối điều khiển được bắt đầu trên cổng số 21
  - Kết nối dữ liệu: Bắt đầu trên cổng số 20. FTP gửi thông tin điều khiển ngoài băng tần vì nó sử dụng kết nối điều khiển riêng. Một số giao thức gửi dòng tiêu đề yêu cầu và phản hồi cũng như dữ liệu trong cùng 1 kết nối TCP.
- FTP Session: khi phiên FTP được bắt đầu giữa client và server, máy client sẽ khởi tạo kết nối TCP điều khiển với phía server. Client gửi thông tin kiểm soát về điều này. Khi server nhận được thông tin này, nó sẽ bắt đầu kết nối dữ liệu với máy client. Tuy nhiên, kết nối điều khiển vẫn hoạt động trong suốt phiên của người dùng. FTP cần duy trì trạng thái về người dùng trong suốt phiên
- FTP Client: FTP hoạt động theo mô hình client-server. FTP client là 1 chương trình chạy trên máy tính của người dùng, cho phép người dùng nói chuyện và nhận tệp từ máy tính từ xa. Đó là 1 tập hợp các lệnh thiết lập kết nối giữa 2 máy chủ, giúp truyền tệp và sau đó đóng kết nối
- Các kiểu dữ liệu FTP:
  - ASCII: mô tả 1 tệp văn bản ASCII trong đó mỗi dòng được biểu thị bằng loai điểm đánh dấu cuối dòng đã đề cập trước đó
  - EBCDIC: Đối với các tệp sử dụng bộ ký tự EBCDIC của IBM, loại này về mặt khái niệm giống với ASCII
  - Image: Tệp không có cấu trúc bên trong chính thức và được truyền từng byte một mà không cần xử lý
  - Local: các tệp chứa dữ liệu theo byte logic có số bit khác 8 có thể được xử lý bằng loại dữ liệu này
- FTP Replies:
  - 200 - Command Okay
  - 530 - Not logged in
  - 331 - Username OK, need a password
  - 502 - Command not implemented
  - 503 - Bad sequence of commands
- Đặc điểm của FTP:
  - Sử dụng TCP làm giao thức lớp vận chuyển
  - Rất tốt cho việc truyền tập tin đơn giản
  - Các lỗi trong quá trình truyền tải phải được máy chủ TFTP xử lý
  - Chỉ sử dụng một kết nối thông qua cổng 69
  - TFTP sử dụng giao thức bước khoá đơn giản (Mỗi gói dữ liệu cần được xác nhận). Do đó lưu lượng bị hạn chế
- Vấn đề bảo mật của FTP:
  - Thông tin không thể đi qua 1 đường hầm an toàn, vì vậy không có mã hoá. Tin tặc sẽ không cần phải vất vả với mã hoá để truy cập hoặc thay đổi dữ liệu có thể sử dụng được nếu chúng có thể chặn giao dịch FTP
  - Dữ liệu vẫn có thể bị chặn và sử dụng sai mục đích nếu hệ thống của nhà cung cấp dịch vụ bị tấn công, ngay cả với lưu trữ đám mây FTP.
  - Do đó, dữ liệu được gửi qua FTP là mục tiêu để giả mạo, nghe lén, brute force và các loại tấn công khác diễn ra một cách chậm rãi. Tin tặc có thể kiểm tra đường truyền FTP và cố gắng tận dụng mọi sai sót chỉ bằng cách quét cổng
  - FTP sử dụng mật khẩu văn bản rõ ràng, mật khẩu chưa được mã hoá - là 1 trong những lỗi bảo mật chính của nó
- Ưu điểm:
  - Các tệp có thể được chia sẻ giữa 2 máy trên mạng
  - Tốc độ là 1 trong những lợi ích chính
  - Không cần phải hoàn thành mọi thao tác để lấy toàn bộ tệp nên hiệu quả hơn
  - An toàn vì cần sử dụng username và password để đăng nhập FTP server
  - Di chuyển các tập tin qua lại qua FTP
- Nhược điểm:
  - Giới hạn kích thước tệp
  - Không hỗ trợ nhiều hơn 1 máy thu
  - Không mã hoá dữ liệu
  - Không được bảo mật <p>

**Sự khác biệt giữa FTP và SFTP**

|FTP|SFTP|
|:---|:---|
|Kênh bảo mật không được cung cấp để truyền tệp giữa các máy chủ|Được cung cấp|
|Chạy trên cổng 21|22|
|Không mã hoá dữ liệu trước khi gửi|Có|
|Làm cho việc tải lên và tải xuống các tập tin mà không có bất kỳ sự bảo mật nào|Duy trì bảo mật đầy đủ của dữ liệu bằng cách sử dụng khoá SSH|
