# Báo cáo thực tập 3
## Networking
### 1. Virtual Private Network (VPN): là 1 công nghệ tạo ra kết nối an toàn và được mã hoá qua 1 mạng kém an toàn hơn, chẳng hạn như Internet. VPN là 1 cách để mở rộng mạng riêng bằng cách sử dụng mạng công cộng như Internet. Người dùng có thể là 1 phần của mạng cục bộ ngồi ở 1 vị trí từ xa. Nó sử dụng giao thức điều chỉnh để thiết lập kết nối an toàn
- Hoạt động: Thiết lập quyền truy cập an toàn vào mạng công ty cho người dùng từ xa. Sau đó, bảo mật dữ liệu trong quá trình truyền và cuối cùng, họ giúp người dùng tránh chặn địa lý và kiểm duyệt. VPN rất hữu ích để bảo vệ dữ liệu trên Wi-Fi mở, cho quyền riêng tư và ngăn ISP của một người điều chỉnh kết nối internet của một người
  - VPN cũng đảm bảo an ninh bằng cách cung cấp một đường hầm được mã hoá giữa client và server VPN
  - VPN được sử dụng để vượt qua nhiều trang web bị chặn
  - VPN tạo điều kiện duyệt web ẩn danh bằng cách ẩn địa chỉ IP
  - Tối ưu hoá công cụ tìm kiếm (SEO) thích hợp nhất được thực hiện bằng cách phân tích dữ liệu từ các nhà cung cấp VPN cung cấp số liệu thống kê theo quốc gia về việc duyệt một sản phẩm cụ thể
  - VPN mã hoá lưu lượng truy cập internet, bảo vệ các hoạt động trực tuyến khỏi các mối đe doạ nghe lén và mạng tiềm ẩn, từ đó tăng cường quyền riêng tư và bảo vệ dữ liệu
- Đặc điểm:
  - Mã hoá: VPN sử dụng 1 số tiêu chuẩn mã hoá để duy trì tính bảo mật của dữ liệu được truyền và ngay cả khi bị chặn cũng không thể hiểu
  - Ẩn danh: VPN ẩn địa chỉ IP của người dùng 1 cách hiệu quả, do đó cung cấp tính ẩn danh và khiến việc theo dõi bởi các trang web hoặc bên thứ 3 là không thể
  - Truy cập từ xa: VPN cung cấp phương tiện để kết nối từ xa an toàn với mạng của doanh nghiệp, do đó thúc đấy năng suất của nhân viên thông qua làm việc từ xa
  - Giả mạo địa lý: người dùng cũng có thể thay đổi địa chỉ IP sang 1 quốc gia khác bằng VPN, do đã phá vỡ các hạn chế khu vực của 1 số trang web
  - Tính toàn vẹn dữ liệu: VPN đảm bảo rằng dữ liệu được truyền trong mạng ở dạng chính xác và không bị thao túng theo bất kỳ cách nào
    
- Các loại VPN:
  - Remote Access VPN: cho phép người dùng kết nối với mạng riêng và truy cập tất cả các dịch vụ và tài nguyên của nó từ xa. Kết nối giữa người dùng và mạng riêng thông qua Internet, kết nối an toàn và riêng tư
  - Site to site VPN: còn được gọi là VPN Router-to-Router, thường được sử dụng trong các công ty lớn. Các công ty hoặc tổ chức, có văn phòng chi nhánh ở các địa điểm khác nhau, sử dụng để kết nối mạng của 1 địa điểm văn phòng với mạng tại 1 điểm văn phòng khác
  - Cloud VPN: là 1 mạng riêng ảo cho phép người dùng kết nối an toàn với cơ sở hạ tầng hoặc dịch vụ dựa trên đám mây. Nó sử dụng internet làm phương tiện truyền tải chính để kết nối người dùng từ xa với các tài nguyên dựa trên cloud. Nó sử dụng các giao thức mã hoá vào bảo mật như IPsec hoặc SSL. Cloud VPN thường được các tổ chức sử dụng để kết nối an toàn tài nguyên tại chỗ với các tài nguyên dựa trên đám mây
  - Mobile VPN: là mạng riêng ảo cho phép người dùng di động kết nối an toàn với mạng riêng, thường thông qua mạng di động. Nó tạo ra 1 kết nối an toàn và được mã hoá giữa thiết bị di động và máy chủ VPN. VPN di động có thể được sử dụng để truy cập các tài nguyên của công ty, chẳng hạn như email hoặc các trang web nội bộ. VPN di động có sẵn dưới dạng ứng dụng độc lập hoặc có thể được tích hợp vào giải pháp MDM
  - SSL VPN: là 1 loại VPN sử dụng giao thức SSL để bảo mật kết nối giữa người dùng và server VPN. SSL VPN thường được truy cập thông qua trình duyệt web. Nó được coi là an toàn hơn VPN IPsec truyền thống vì sử dụng các giao thức mã hoá tương tự HTTPS

- Các giao thức:
  - OpenVPN: là giao thức tương thích cung cấp nhiều lựa chọn thiết lập khác nhau. SSL/TLS dành cho việc trao đổi khoá, nó có thể đi qua tường lửa và NAT
  - PPTP: không được sử dụng vì có nhiều lựa chọn an toàn khác với mã hoá cao hơn và tiên tiến hơn để bảo vệ dữ liệu
  - WireGuard: là 1 lựa chọn tốt cho thấy khả năng về hiệu suất
  - Secure Socket Tunneling Protocol (SSTP): Được phát triển cho người dùng Windows. Không được sử dụng rộng rãi do thiếu tính kết nối
  - Layer 2 Tunneling Protocol (L2TP): kết nối người dùng máy chủ VPN nhưng thiếu mã hoá do đó nó thường được sử dụng với IPsec để cung cấp kết nối, mã hoá và bảo mật đồng thời
 
- Cơ chế xác thực:
  - Pre-Share Key (PSK): là khoá bí mật được sử dụng để xác thực 2 bên, tức là VPN client và server. Nó rất dễ tích hợp nhưng cũng không được coi là an toàn khi không được quản lý đúng cách
  - Digital Certificates: dựa trên các chứng chỉ do cơ quan cấp chứng chỉ đáng tin cậy cấp, nó có hiệu quả trong việc xác định danh tính của người dùng và thiết bị có cảm giác an toàn
  - Username and Password: thường được biết đến trong xác thực người dùng, trong đó người dùng gửi thông tin đăng nhập của họ để họ truy cập VPN. Phương pháp này đôi khi được hỗ trợ bởi các biện pháp bảo mật khác như MFA
  - Two-Factor Authentication (2FA): cung cấp 1 mức độ bảo vệ khác bằng cách bao gồm yếu tố nhận dạng thứ 2 theo cách số nhận được qua điện thoại di động của một người cùng với nhận dạng người dùng và mật khẩu

- Mối quan tâm về bảo mật trong VPN:
  - Rò rỉ dữ liệu: VPN đôi khi cũng không ẩn địa chỉ IP và do đó gây rò rỉ dữ liệu được thu thập. Điều này có thể xảy ra thông qua rò rỉ DNS hoặc khi kết nối VPN bị cắt đứt sớm hoặc khi chuyển đổi giữa các máy chủ
  - Mã hoá yếu: Tính bảo mật của VPN có thể bị ảnh hưởng bởi các tiêu chuẩn mã hoá yếu cũng như các thuật toán mã hoá lỗi thời. Điều cần thiết là phải thực hiện các phương phép mã hoá/giải mã
  - Tin tưởng và nhà cung cấp VPN: họ chỉ có thể đảm bảo rằng họ sẽ bảo mật dữ liệu người dùng và không lạm dụng dữ liệu đó nếu chính người dùng tin tưởng nhà cung cấp dịch vụ. Một số nhà cung cấp có thể lưu giữ hồ sơ về việc sử dụng tài nguyên của người dùng và điều này có thể vi phạm quyền riêng tư của người dùng
  - Man-in-the-Middle Attacks (MitM): nếu cài đặt VPN không an toàn, kẻ tấn công có cơ hội can thiệp và sửa đổi thông tin trao đổi giữa client và server
  - Đánh đổi hiệu suất: Bảo mật VPN thường ảnh hưởng đến kết nối internet vì mã hoá và định tuyến qua các máy chủ VPN gây ra kết nối chậm hơn. Đối với bảo mật và hiệu suất luôn quan trọng như nhau khi cân đo đong đếm.
    
- Tính hợp pháp: VPN là hợp pháp ở hầu hết các quốc gia. Tính hợp pháp của việc sử dụng dịch vụ VPN phụ thuộc vào quốc gia và mối quan hệ địa chính trị của quốc gia đó với quốc gia khác. 1 VPN đáng tin cậy và an toàn luôn hợp pháp nếu không có ý định sử dụng nó cho bất kỳ hoạt động bất hợp pháp nào
- Lợi ích:
  - Có thể chuyển đổi IP
  - Kết nối internet an toàn và được mã hoá
  - Chia sẻ tệp là bí mật và an toàn
  - Quyền riêng tư được bảo vệ khi sử dụng internet
  - Không còn giới hạn băng thông
  - Tạo điều kiện tiết kiệm chi phí cho việc mua sắm
- Hạn chế:
  - Có thể làm giảm tốc độ internet
  - VPN cao cấp có chi phí không rẻ
  - VPN có thể bị cấm ở 1 số quốc gia

### 2. IP security (IPSec): là 1 bộ giao thức tiêu chuẩn của Internet Engineering Task Force (IETF) giữa 2 điểm giao tiếp trên mạng IP cung cấp tính xác thực, toàn vẹn và bảo mật dữ liệu. Nó cũng xác định gói được mã hoá, giải mã và xác thực. Các giao thức cần thiết để trao đổi khoá an toàn và quản lý khoá được xác định trong đó
- Công dụng:
  - Mã hoá dữ liệu lớp ứng dụng
  - Cung cấp bảo mật cho các bộ định tuyến gửi dữ liệu định tuyến qua internet công cộng
  - Cung cấp xác thực mà không cần mã hoá, hay muốn xác thực dữ liệu bắt nguồn từ 1 người gửi đã biết
  - Bảo vệ dữ liệu bằng cách thiết lập các mạch sử dụng đường hầm IPSec trong đó tất cả dữ liệu được gửi giữa 2 điểm cuối được mã hoã

- IPSec Encryption: là 1 chức năng phần mềm mã hoá dữ liệu để bảo vệ dữ liệu khỏi bị truy cập trái phép. Khoá đó mã hoá dữ liệu mà giải được mã. IPSec hỗ trợ nhiều thuật toán mã hoá, bao gồm AES, Blowfish, Triple DES, ... IPSec kết hợp mã hoá bất đối xứng và đối xứng để cung cấp cả tốc độ và bảo mật trong quá trình truyền dữ liệu. Trong mã hoá bất đối xứng, khoá mã hoá được công khai, trong khi khoá giải mã vẫn ở chế độ riêng tư. Mã hoá đối xứng sử dụng cùng 1 khoá công khai để mã hoá và giải mã dữ liệu. IPSec xây dựng 1 kết nối an toàn bằng cách sử dụng mã hoá bất đối xứng và sau đó chuyển sang mã hoá đối xứng để tăng tốc độ truyền dữ liệu

 - Các thành phần:
   - Encapsulating Security Payload (ESP): Cung cấp tính toàn vẹn dữ liệu, mã hoá, xác thực và chống phát lại. Nó cũng cung cấp xác thực cho tải trọng
   - Authentication Header (AH): Cung cấp tính toàn vẹn dữ liệu, xác thực, chống phát lại và nó không cung cấp mã hoá. Bảo vệ chống phát lại chống lại việc truyển trái phép các gói. Nó không bảo vệ tính bảo mật dữ liệu
     |IP HDR|AH|TCP|DATA|
     |:---|:---|:---|:---|
   - Internet Key Exchange (IKE): là 1 giao thức bảo mật mạng được thiết kế để trao đổi động các khoá mã hoá và tìm cách vượt qua Security Association (SA) giữa 2 thiết bị. SA thiết lập các thuộc tính bảo mật được chia sẻ giữa 2 thực thể mạng để hỗ trợ giao tiếp an toàn. Giao thức quản lý khoá (ISAKMP) và SA cung cấp 1 khuôn khổ để xác thực và trao đổi khoá. ISAKMP cho biết cách thiết lập các SA và cách kết nối trực tiếp giữa 2 server đang sử dụng IPSec. IKE cung cấp bảo vệ nội dung tin nhắn và cũng là 1 khung mở để thực hiện các thuật toán tiêu chuẩn như SHA và MD5. Người dùng thuật toán của IPSec tạo ra 1 mã định danh duy nhất cho mỗi gói. Mã định danh này sau đó cho phép 1 thiết bị xác định xem 1 gói đã đúng hay chưa. Các gói không được uỷ quyền sẽ bị loại bỏ và không được trao cho người nhận
     
- Kiến trúc IPSec: sử dụng 2 giao thức để bảo mật luồng dữ liệu. Các giao thức này là ESP và AH. Kiến trúc IPSec bao gồm các giao thức, thuật toán, DOI và quản lý khoá. Tất cả các thành phần rất quan trọng để cung cấp 3 dịch vụ chính
  - Bảo mật
  - Tính xác thực
  - Tính toàn vẹn
    ![image](https://github.com/user-attachments/assets/10fce8a6-0f1c-45b1-964f-3cea7c57b67e)

- Làm việc trên IPSec:
  - Máy chủ kiểm tra xem gói tin có nên được truyền bằng IPSec hay không. Lưu lượng gói này kích hoạt chính sách bảo mật cho chính nó. Điều này được thực hiện khi hệ thống gửi gói áp dụng mã hoá thích hợp. Các gói tin đến cũng được máy chủ kiểm tra xem chúng có được mã hoá đúng cách hay không
  - Sau đó, IKE giai đoạn 1 bắt đầu, trong đó 2 máy chủ tự xác thực với nhau để bắt đầu 1 kênh an toàn. Nó có 2 chế độ. Chế độ *Main* cung cấp bảo mật cao hơn và chế độ *Aggrressive* cho phép máy chủ thiết lập mạch IPSec nhanh hơn
  - Kênh được tạo ở bước cuối cùng sau đó được sử dụng để thương lượng an toàn cách mạch IP sẽ mã hoá dữ liệu trên mạch IP
  - Bây giờ, IKE giai đoạn 2 được tiến hành qua kênh an toàn, trong đó 2 máy chủ thương lượng loại thuật toán mật mã để sử dụng trong phiên và đồng ý về tài liệu khoá bí mật sẽ được sử dụng với các thuật toán đó
  - Sau đó, dữ liệu được trao đổi qua đường hầm được mã hoá IPSec mới được tạo. Các gói này được mã hoá và giải mã bởi các máy chủ bằng IPSec SA
  - Khi giao tiếp giữa các máy chủ được hoàn thành hoặc phiên hết thời gian chờ thì đường hầm IPSec sẽ bị chấm dứt bằng cách loại bỏ các khoá của cả 2 máy chủ

- Chế độ IPSec:
  - Tunnel: thích hợp để gửi dữ liệu qua mạng công cộng vì nó cải thiện bảo mật dữ liệu chống lại các bên trái phép. Máy tính mã hoá tất cả dữ liệu, bao gồm cả tải trọng và tiêu đề, thêm 1 tiêu đề mới vào nó
  - Transport: chỉ mã hoá tải trọng của gói dữ liệu trong khi giữ nguyên tiêu đề IP. Tiêu đề gói không được mã hoá cho phép các bộ định tuyến xác định địa chỉ đích của mỗi gói dữ liệu. Do đó, truyền tải IPSec được sử dụng trong 1 mạng khép kín và đáng tin cậy, chẳng hạn như để bảo mật liên kết trực tiếp giữa 2 máy tính
 
- Các tính năng:
  - Xác thực: xác thực các gói IP bằng chữ ký số hoặc bí mật được chia sẻ. Điều này giúp đảm bảo rằng các gói không bị giả mạo hoặc giả mạo
  - Bảo mật: Cung cấp tính bảo mật bằng cách mã hoá các gói IP, ngăn chặn việc nghe lén lưu lượng mạng
  - Tính toàn vẹn: đảm bảo rằng các gói IP không bi sửa đổi hoặc bị hỏng trong quá trình truyền
  - Quản lý khoá: cung cấp các dịch vụ quản lý khoá, bao gồm trao đổi khoá và thu hồi khoá, để đảm bảo rằng các khoá mật mã được quản lý an toàn
  - Tunnel: hỗ trợ đường hầm, cho phép các gói IP được đóng gói trong 1 giao thức khác, chẳng hạn như GRE (Generic Routing Encapsulation) hoặc L2TP
  - Tính linh hoạt: Có thể được cấu hình để cung cấp bảo mật cho 1 loạt các cấu trúc liên kết mạng, bao gồm các kết nối point-to-point, site-to-site và truy cập từ xa
  - Khả năng tương tác: IPSec là 1 giao thức tiêu chuẩn mở, có nghĩa là nó được hỗ trợ bởi 1 loạt các nhà cung cấp và có thể được sử dụng trong các môi trường không đồng nhất

- IPSec VPN: là 1 loại phần mềm sử dụng giao thức IPSec để thiết lập các đường hầm được mã hoá qua internet. Nó cung cấp mã hoá đầu cuối, có nghĩa là dữ liệu được chia nhỏ tại máy tính và sau đó được thu thập tại máy chủ nhận

- Ưu điểm:
  - Bảo mật mạnh mẽ: giúp bảo vệ dữ liệu nhạy cảm và đảm bảo quyền riêng tư cùng tính toàn vẹn của mạng
  - Khả năng tương thích rộng: là 1 giao thức tiêu chuẩn mở được hỗ trợ rộng rãi bởi các nhà cung cấp và có thể được sử dụng trong các môi trường không đồng nhất
  - Tính linh hoạt: Có thể được cấu hình để cung cấp bảo mật cho 1 loạt các cấu trúc liên kết mạng, bao gồm các kết nối point-to-point, site-to-site và truy cập từ xa
  - Khả năng mở rộng: được sử dụng để bảo mật các mạng quy mô lớn và có thể được tăng hoặc giảm khi cần thiết
  - Cải thiện hiệu suất mạng: bằng cách giảm tắc nghẽn mạng và cải thiện hiệu quả mạng
 
- Nhược điểm:
  - Cấu hình phức tạp: có thể phức tạp để cấu hình và đòi hỏi kiến thức cũng như kỹ năng chuyên ngành
  - Vấn đề tương thích: Có thể có vấn đề tương thích với 1 số thiết bị và ứng dụng mạng, có thể dẫn đến các vấn đề về khả năng tương tác
  - Tác động đến hiệu suất: do chi phí mã hoá và giải mã các gói IP
  - Quản lý khoá: yêu cầu quản lý khoá hiệu quả để đảm bảo tính bảo mật của các khoá mật mã được sử dụng để mã hoá và xác thực
  - Bảo vệ hạn chế: chỉ cung cấp bảo vệ cho lưu lượng IP và các giao thức khác như ICMP, DNS và các giao thức định tuyến vẫn có thể bị tấn công
