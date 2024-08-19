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

### Simple Mail Transfer Protocol (SMTP): là 1 giao thức lớp ứng dụng. Client muốn gửi thư mở 1 kết nối TCP đến SMTP server và sau đó gửi thư qua kết nối. SMTP server là chế độ nghe luôn bật. Ngay sau khi nó lắng nghe kết nối TCP từ bất kì client nào, quá trình SMTP sẽ bắt đầu kết nối thông qua cổng 25. Sau khi thiết lập thành công kết nối TCP, quá trình client sẽ gửi thư ngay lập tức.
- Giao thức SMTP: Mô hình SMTP có 2 loại:
  - End-to-end: được sử dụng để giao tiếp giữa các tổ chức khác nhau trong khi phương pháp lưu trữ và chuyển tiếp được sử dụng trong 1 tổ chức. Một SMTP client muốn gửi thư sẽ liên hệ trực tiếp với SMTP server của đích để gửi thư đến đích. SMTP server sẽ giữ thư cho chính nó cho đến khi nó được sao chép thành công vào SMTP của người nhận
  - SMTP client là client khởi tạo phiên, hay client-SMTP và SMTP server là máy chủ phản hồi yêu cầu phiên, hay receiver-SMTP. Client-SMTP sẽ bắt đầu phiên và receiver-SMTP sẽ phản hồi yêu cầu.
  - Phương pháp lưu trữ và chuyển tiếp
- Mô hình hệ thống: Người dùng giao dịch với tác nhân người dùng (UA). Để trao đổi thư bằng TCP, tác nhân chuyển đổi thư (MTA) được sử dụng. Người dùng gửi thư không phải đối phó với MTA vì quản trị viên hệ thống có trách nhiệm thiết lập MTA cục bộ. MTA duy trì 1 hàng đợi thư nhỏ để có thể lên lịch gửi thư lặp lại trong trường hợp người nhận không có sẵn. MTA gửi thư đến hộp thư và thông tin sau đó có thể tải xuống bởi các tác nhân người dùng.
![image](https://github.com/user-attachments/assets/f16fe938-c108-4a0e-952b-0be7c8247e81)
- Các thành phần:
  - Mail User Agent (MUA): 1 ứng dụng máy tính giúp gửi và truy xuất thư. Nó chịu trách nhiệm tạo thư email để chuyển đến Mail Transfer Agent (MTA)
  - Mail Submission Agent (MSA): 1 chương trình máy tính nhận thư MUA và tương tác với Mail Transfer Agent (MTA) để chuyển thư
  - Mail Transfer Agent (MTA): Phần mềm có công việc chuyển thư từ hệ thống này sang hệ thống khác với sự trợ giúp của SMTP
  - Mail Delivery Agent (MDA): Hệ thống giúp chuyển thư đến hệ thống địa phương
- Cách hoạt động:
  - Giao tiếp giữa người gửi và nhận: Tác nhân người dùng của người gửi chuẩn bị tin nhắn và gửi nó đến MTA. Trách nhiệm của MTA là chuyển thư qua mạng đến MTA của người nhận. Để gửi thư, 1 hệ thống phải có MTA client và để nhận thư, hệ thống phải có MTA server
  - Gửi email: Thư được gửi bởi 1 loạt các tin nhắn yêu cầu và phản hồi giữa client và server. Thông điệp được gửi qua bao gồm 1 tiêu đề và 1 nội dung. 1 dòng *null* được sử dụng để chấm dứt tiêu đề thư và mọi thứ sau dòng *null* được coi là nội dung của thư, là 1 chuỗi kí tự ASCII. Nội dung thư chứa thông tin thực tế được đọc bởi biên lai
  - Nhận email: Tác nhân người dùng ở phía máy chủ kiểm tra hộp thư tại 1 khoảng thời gian cụ thể. Nếu nhận được bất kỳ thông tin nào, nó sẽ thông báo cho người dùng về thư. Khi người dùng cố gắng đọc thư, nó sẽ hiển thị 1 danh sách các email với mô tả ngắn về từng thư trong hộp thư. Bằng cách chọn bất kỳ thư nào, người dùng có thể xem nội dung của nó trên thiết bị đầu cuối.
  ![image](https://github.com/user-attachments/assets/b6587008-2a99-4855-9941-1d84477e039a)
- SMTP Envelope:
  - Mục đích:
    - Chứa thông tin hướng dẫn gửi email giữa các máy chủ
    - Khác với tiêu đề và nội dung email và không hiển thị người nhận email
  - Nội dung:
    - **Địa chỉ người gửi:** Chỉ định nơi email bắt nguồn
    - **Địa chỉ người nhận:** Cho biết nơi gửi email
    - **Thông tin định tuyến:** Giúp máy chủ xác định đường dẫn gửi email
  - So sánh với thư thông thường:
    - SMTP Envelope như địa chỉ trên phong bì vật lý cho thư thông thường
    - SMTP Envelope hướng các máy chủ email về nơi gửi email
  - SMTP Command:
    
|Keyword|Command form|Description|Usage|
|:---|:---|:---|:---|
|HELO|HELO<SP><domain><CRLF>|Cung cấp nhận dạng của người gửi, tức tên server|Bắt buộc|
|MAIL|MAIL<SP>FORM:<reverse-path><CRLF>|Chỉ định người khởi tạo thư|Bắt buộc|
|RCPT|RCPT<SP>TO:<forward-path><CRLF>|Chỉ định người nhận thư|Bắt buộc|
|DATA|DATA<CRLF>|Chỉ định phần đầu của thư|Bắt buộc|
|QUIT|QUIT<CRLF>|Đóng kết nối TCP|Bắt buộc|
|RSET|RSET<CRLF>|Huỷ bỏ giao dịch thư hiện tại nhưng kết nối TCP vẫn mở|Rất khuyến khích|
|VRFY|VRFY<SP><string><CRLF>|Xác nhận hoặc xác minh tên người dùng|Rất khuyến khích|
|NOOP|NOOP<CRLF>|Không thi hành|Rất khuyến khích|
|TURN|TURN<CRLF>|Đảo ngược vai trò của người gửi và người nhận|Hiếm sử dụng|
|EXPN|EXPN<SP><string><CRLF>|Chỉ định danh sách gửi thư sẽ được mở rộng|Hiếm sử dụng|
|HELP|HELP<SP><string><CRLF>|Gửi 1 số tài liệu cụ thể đến hệ thống|Hiếm sử dụng|
|SEND|SEND<SP>FROM:<reverse-path><CRLF>|Gửi thư đến thiết bị đầu cuối|Hiếm sử dụng|
|SOML|SOML<SP>FROM:<reverse-path><CRLF>|Gửi thư đến thiết bị đầu cuối nếu có thể, nếu không vào hộp thư|Hiếm sử dụng|
|SAML|SAML<SP>FROM:<reverse-path><CRLF>|Gửi thư đến thiết bị đầu cuối và hộp thư|Hiếm sử dụng|

- SMTP Port: Sử dụng cổng 587 để truyền an toàn qua TLS. Ngoài ra, cổng 25 chủ yếu được sử dụng để chuyển tiếp SMTP, không phải để gửi SMTP. Cổng 2525 có thể phục vụ như 1 giải pháp thay thế tốt, mặc dủ nó không phải là cổng SMTP chính thức
- So sánh SMTP và SMTP Expanded

|SMTP|SMTP Expanded|
|:---|:---|
|Không được xác minh trong SMTP do các email lừa đảo quy mô lớn được gửi|Xác thực người gửi được thực hiện|
|Không thể đính kèm tệp Đa phương tiện trong SMTP trực tiếp mà không có sự trợ giúp của MMIE |Có thể|
|Không thể giảm kích thước của email SMTP|Có thể|
|SMTP Client mở truyền bằng lệnh HELO|Tính năng nhận dạng chính cho các ESMTP client là mở 1 đường truyền bằng lệnh EHLO|

- Ưu điểm:
  - Nếu cần thiết, người dùng có thể có 1 máy chủ chuyên dụng
  - Cho phép gửi thư hàng loạt
  - Chi phí thấp và vùng phủ sóng rộng
  - Cung cấp các lựa chọn để theo dõi email
  - Gửi email đáng tin cậy và nhanh chóng
- Nhược điểmL
  - Cổng chung có thể bị chặn bởi 1 số tường lửa
  - Bảo mật SMTP là 1 vấn đề lớn
  - Sự đơn giản của nó hạn chế mức độ hữu ích của nó
  - Chỉ có thể sử dụng các ký tự ASCII 7 bit
  - Nếu thư dài hơn 1 độ dài nhất định, SMTP server có thể từ chối toàn bộ thư
  - Gửi tin nhắn thường sẽ liên quan đến việc xử lý qua lại bổ sung giữa các máy chủ, điều này sẽ trì hoãn việc gửi và tăng khả năng nó sẽ không được gửi
- So sánh SMTP, POP và IMAP
  
|SMTP|POP|IMAP|
|:---|:---|:---|
|Gửi thư|Truy xuất thư|Truy xuất thư|
|Giao thức đẩy|Giao thức kéo|Giao thức kéo|
|Hoạt động giữa mail server của người gửi đến máy chủ thư của người gửi và người gửi|Hoạt động giữa mail server của người nhận và người nhận|Hoạt động giữa mail server của người nhận và người nhận|
|Không lưu trữ thư trên máy chủ, chỉ gửi thư|Tải xuống tất cả thư khi kết nối với Internet|Lưu trữ tất cả thư trên máy chủ và tải xuống khi nhận được yêu cầu|
|Hoạt động trên cổng TCP 25|TCP 110|TCP 143|
|Giao thức định hướng kết nối|Kết nối|Kết nối|
|Có kết nối TCP bền bỉ|Bền bỉ|Bền bỉ|
|Giao thức không trạng thái|Giao thức trạng thái|Giao thức trạng thái|
|Không được sử dụng ở phía người nhận|Được|Được|
