# Networking
## Mô hình TCP/IP
### Mô hình TCP/IP là giao thức cốt lõi của Internet. Mô hình này xác định cách dữ liệu được truyền qua mạng, đảm bảo liên lạc đáng tin cậy giữa các thiết bị. TCP/IP là mô hình rút gọn của OSI. Công việc chính của TCP/IP là truyền dữ liệu của máy tính từ thiết bị này sang thiết bị khác. Nó chia dữ liệu thành các gói và kết hợp chúng ở đầu kia, giúp duy trì tính chính xác của dữ liệu truyền từ đầu này sang đầu kia. TCP/IP cho phép linh hoạt thích ứng với các triển khai vật lý khác nhau
**Sự khác biệt giữa TCP và IP**
|Tính năng|TCP(Transmission Control Protocol)|IP (Internet Protocol)|
|:---|:---|:---|
|Mục đích|Đảm bảo việc phân phối dữ liệu đáng tin cậy, có trật tự và được kiểm tra lỗi giữa các ứng dụng|Cung cấp địa chỉ và định tuyến các gói trên mạng|
|Kiểu|Định hướng kết nối|Không kết nối|
|Chức năng|Quản lý việc truyền dữ liệu giữa các thiết bị, đảm bảo tính toàn vẹn và trật tự của dữ liệu|Định tuyến các gói dữ liệu từ nguồn tới đích dựa trên địa chỉ IP|
|Xử lý lỗi|Có, bao gồm cơ chế kiểm tra và phục hồi lỗi|Không, bản thân IP không xử lý lỗi; dựa trên các giao thức lớp trên như TCP|
|Kiếm soát dòng chảy|Có|Không|
|Kiếm soát tắc nghẽn|Có|Không|
|Phân đoạn dữ liệu|Chia dữ liệu thành các gói nhỏ và tập hợp chúng tại đích|Chia dữ liệu thành các gói nhưng không xửa lý việc tập hợp lại|
|Kích thước tiêu đề|20-60 byte|20 byte|
|Độ tin cậy|Cung cấp truyền dữ liệu đáng tin cậy|Không đảm bảo giao vận, độ tin cậy hoặc đơn hàng|
|Xác nhận truyền tải|Có|Không|

- Cách hoạt động: chia dữ liệu thành các gói ở đầu người gửi và các gói tương tự phải được kết hợp lại ở đầu người nhận để tạo thành cùng 1 dữ liệu để duy trì tính chính xác của dữ liệu. Mô hình này chia dữ liệu thành quy trình 4 lớp, trong đó dữ liệu đầu tiên đi vào lớp này theo 1 thứ tự và lặp lại theo thứ tự ngược lại để được sắp xếp theo cách tương tự ở đầu người nhận
- Các lớp trong mô hình:
  - Lớp truy cập mạng (Network Access Layer):
    - Một nhóm các ứng dụng yêu cầu truyền thông mạng. Chịu trách nhiệm tạo dữ liệu và yêu cầu kết nối. Nó hoạt động thay mặt cho người gửi và lớp Truy cập mạng thay mặt cho người nhận.
    - Loại giao thức mạng của gói, được xác định bởi lớp truy cập mạng. Ngăn ngừa lỗi và "đóng khung" cũng được cung cấp bởi lớp này. Định khung PPP và định khung Ethernet IEEE 802.2
  - Tầng Internet hoặc Mạng (Network Layer or Internet):
    - Tương đương với các chức năng của lớp Mạng trong OSI. Nó xác định giao thức chịu trách nhiệm truyền dữ liệu logic trên toàn bộ mạng. Các giao thức chính:
      - IP: chịu trách nhiệm phân phối các gói từ máy chủ nguồn đến máy chủ đích bằng cách xem địa chỉ IP trong tiêu đề gói. IP có 2 phiên bản: IPv4 và IPv6. IPv4 được sử dụng hầu hết cho các web hiện này
      - ICMP (Internet Control Message Protocol): Được gói gọn trong các gói dữ liệu IP và chịu trách nhiệm cung cấp cho máy chủ thông tin về các sự cố mạng
      - ARP (Address Resolution Protocol): Tìm địa chỉ phần cứng từ máy chủ từ 1 địa chỉ IP đã biết. ARP có 1 số loại: đảo ngược, proxy, miễn phí và nghịch đảo
    - Lớp Internet là 1 lớp trong bộ IP, là tập hợp các giao thức xác định Internet. Nó chịu trách nhiệm định tuyến các gói dữ liệu từ thiết bị này sang thiết bị khác qua mạng. Nó thực hiện bằng cách gán cho mỗi thiết bị 1 địa chỉ IP duy nhất, địa chỉ này được sử dụng để nhận dạng thiết bị và xác định tuyến đường mà các gói sẽ đi để đến được thiết bị đó.
  - Lớp vận chuyển: Trao đổi xác nhận đã nhận dữ liệu và truyền lại các gói bị thiếu để đảm bảo các gói đến thứ tự và không có lỗi. Đó gọi là giao thức end-to-end. Các giao thức được sử dụng:
    - TCP: Các ứng dụng có thể tương tác với nhau bằng TCP như thể chúng được kết nối vật lý bằng 1 mạch điện. TCP truyền dữ liệu theo cách giống với truyền ký tự hơn là các gói riêng biệt. Điểm bắt đầu thiết lập kết nối, toàn bộ quá trình truyền theo thứ tự byte và điểm kết thúc đóng kết nối tạo nên quá trình truyền
    - UDP (User Datagram Protocol): Dịch vụ phân phối datagram được cung cấp bởi UDP, giao thức lớp vận chuyển khác. Kết nối giữa máy nhận và máy gửi không được UDP xác minh. Các ứng dụng truyền tải lượng dữ liệu nhỏ sử dụng UDP thay vì TCP vì nó loại bỏ quá trình thiết lập và xác thực kết nối
  - Lớp ứng dụng: tương tự lớp vận chuyển của OSI. Chịu trách nhiệm liên lạc từ đầu đến cuối và cung cấp dữ liệu không có lỗi. Nó bảo vệ các ứng dụng lớp trên khỏi sự phức tạp của dữ liệu. Các giao thức trong lớp này:
    - HTTP và HTTPS: được WWW sử dụng để quản lý thông tin liên lạc giữa trình duyệt web và máy chủ. HTTPS là viết tắt của HTTP-Secure. Nó là sự kết hợp giữa HTTP với SSL. Nó hiệu quả trong trường hợp trình duyệt cần điền vào biểu mẫu, đăng nhập, xác thực và thực hiện các giao dịch ngân hàng.
    - SSH (Secure Shell): phần mềm mô phỏng thiết bị đầu cuối tương tự Telnet. SSH được ưa chuồng vì khả năng duy trì kết nối được mã hoá. Nó thiết lập 1 phiên an toàn thông qua kết nối TCP/IP
    - NTP (Network Time Protocol): Đồng bộ hoá trên máy tính với 1 nguồn thời gian tiêu chuẩn. Nó rất hữu ích trong các tình huống như giao dịch ngân hàng
- Lớp server-to-server là 1 lớp trong mô hình OSI chịu trách nhiệm cung cấp liên lạc giữa các máy chủ trên mạng. Một số trường hợp sử dụng phổ biến:
  - Reliable Data Transfer: lớp host-to-host đảm bảo rằng dữ liệu được truyền 1 cách đáng tin cậy giữa các máy chủ bằng cách sử dụng các kỹ thuật như sửa lỗi và kiếm soát luồng
  - Segmentation and Reassembly: lớp host-to-host chịu trách nhiệm chia các khối dữ liệu lớn thành cách phân đoạn nhỏ hơn có thể truyền qua mạng và sau đó tập hợp lại dữ liệu tại đích. Điều này cho phép nhiều thiết bị chia sẻ cùng 1 kết nối mạng và giúp cải thiện việc sử dụng mạng
  - Multiplexing and Demultiplexing: lớp server-to-server chịu trách nhiệm ghép kênh dữ liệu từ nhiều nguồn vào 1 kết nối mạng duy nhất, sau đó phân kênh dữ liệu tại đích, Điều này cho phép nhiều thiết bị chia sẻ cùng 1 kết nối mạng và giúp cải thiện việc sử dụng mạng
  - End-to-end Communication: Lớp server-to-server đến máy chủ cung cấp dịch vụ hướng kết nối cho phép các máy chủ giao tiếp với nhau từ đầu đến cuối mà không cần các thiết bị trung gian tham gia vào quá trình liên lạc
- Lớp vật lý không được bao phủ bởi mô hình TCP/IP vì nó được thiết kế độc lập với phương tiện vật lý cơ bản. Điều này cho phép TCP/IP linh hoạt và thích ứng với các loại kết nối vật lý khác nhau. Lớp vật lý thường được xử lý bởi các thành phần phần cứng và tiêu chuẩn dành riêng cho phương tiện vật lý đang được sử dụng, như cáp Ethernet hoặc Wi-Fi
- Các giao thức Internet phố biến khác:
  - HTTP: chăm sóc trình duyệt web và trang web
  - FTP: đảm nhiệm việc gửi tệp qua Internet
  - SMTP: được sử dụng để gửi và nhận dữ liệu

 **So sánh giữa mô hình TCP/IP và OSI**
 
 |TCP|IP|
 |:---|:---|
 |Sử dụng cả lớp phiên và lớp trình bày trong lớp ứng dụng|Sử dụng các lớp phiên và trình bày khác nhau|
 |Cách tiếp cận không kết nối theo chiều ngang|Cách tiếp nhận theo chiều dọc|
 |Lớp Transport không cung cấp sự đảm bảo cho việc phân phối các gói tin|Cung cấp sự đảm bảo cho việc phân phối các gói tin|
 |Các giao thức không thể thay thế dễ dàng|Các giao thức được bao phủ tốt hơn và dễ dàng thay thế hơn khi thay đổi công nghệ|
 |Lớp mạng chỉ cung cấp các dịch vụ không kết nối (IP). Lớp vận chuyển (TCP) cung cấp các kết nối|Các dịch vụ hướng kết nối và không được cung cấp bởi lớp mạng|

 - Ưu điểm:
   - Khả năng tương tác: cho phép các loại máy tính và mạng khác nhau giao tiếp với nhau, thúc đẩy khả năng tương thích và hợp tác giữa các hệ thống khác nhau
   - Khả năng mở rộng: Có khả năng mở rộng cao, khiến nó phù hợp cho cả mạng nhỏ và lớn, từ LAN đến WAN
   - Tiêu chuẩn hoá: Dựa trên các tiêu chuẩn và giao thức mở, đảm bảo rằng các thiết bị và phần mềm khác nhau có thể hoạt động cùng nhau mà không gặp vấn đề về tương thích
   - Tính linh hoạt: Hỗ trợ nhiều giao thức định tuyến, loại dữ liệu và phương thức liên lạc khác nhau, giúp nó có thể thích ứng với các nhu cầu mạng khác nhau
   - Độ tin cậy: Tính năng kiểm tra lỗi và truyền lại để đảm bảo truyền dữ liệu đáng tin cậy, thậm chí trẻn khoảng cách xa và qua các điều kiện mạng khác nhau
- Nhược điểm:
  - Cấu hình phức tạp: Việc thiết lập và quản lý có thể phức tạp, đặc biệt đối với các mạng lớn có nhiều thiết bị. Sự phức tạp có thể dẫn đến lỗi cấu hình
  - Những lo ngại về bảo mật: TCP/IP ban đầu không được thiết kế nhằm mục đích bảo mật. Mặc dù hiện nay có nhiều giao thức bảo mật như SSL/TLS, nhưng chúng đã được thêm vào bên trên mô hình cơ bản, điều này có thể dẫn đến các lỗ hổng
  - Tính kém hiệu quả đối với các mạng nhỏ: Chi phí và độ phức tạp của mô hình TCP/IP có thể không cần thiết và không hiệu quả so với các giao thức mạng đơn giản hơn
  - Bị giới hạn bởi không gian địa chỉ: Mặc du IPv6 giải quyết được vấn đề này nhưng hệ thống IPv4 cũ hơn có không gian địa chỉ hạn chế, điều này có thể dẫn đến sự cố cạn kiệt địa chỉ trong các mạng lớn hơn
  - Chi phí dữ liệu: TCP, giao thức truyền tải, bao gồm 1 lượng chi phí đáng kể để đảm bảo việc truyền tải đáng tin cậy. Điều này có thể làm giảm hiệu quả, đặc biệt đối với các gói dữ liệu nhỏ hoặc trong các mạng nơi tốc độ là rất quan trọng
