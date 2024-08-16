# Networking
## Mô hình OSI
### Mô hình OSI (Open Systems Interconnection Reference Model) - mô hình tham chiếu kết nối các hệ thống mở, hoặc mô hình 7 tầng của OSI. Mô hình OSI mô tả 7 tầng một hệ thống máy tính sử dụng để giao tiếp qua mạng. <p>
![image](https://github.com/user-attachments/assets/ac1ec1b5-c1ea-4c25-86e8-35c6fca40102)
- Có 2 giao thức được sử dụng trong mô hình:
  - `Giao thức hướng liên kết (Connection Oriented):` các thực thể trong cùng 1 tầng của 2 hệ thống khác nhau
cần phải thiết lập một liên kết logic chung. Chúng tiến hành trao đổi, thương lượng với nhau về tập các tham số
sẽ sử dụng trong quá trình truyền dữ liệu.
  - `Giao thức không liên kết (Connectionless):` Chỉ có giai đoạn duy nhất truyền dữ liệu và dữ liệu khi này được
truyền độc lập trên các tuyến khác nhau  
- Vai trò và chức năng của 7 tầng OSI:
1. Lớp vật lý (Physical): Các khung được chuyển đổi thành bit và được truyền vật lý
2. Lớp liên kết (Data Link): Các gói được đóng khung và gửi đến thiết bị tiếp theo
3. Lớp mạng (Network): Các phân đoạn được đóng gói thành các gói và được định tuyến 
4. Lớp vận chuyển (Transport): Dữ liệu được chia thành các phân đoạn để phân phối đáng tin cậy
5. Lớp phiên (Session): Các kết nối được thiết lập và quản lý
6. Lớp trình bày (Presentation): Dữ liệu được định dạng và mã hoá
7. Lớp ứng dụng (Application): Ứng dụng tạo dữ liệu
   
1. Lớp vật lý: là lớp thấp nhất của mô hình tham chiếu OSI. Nó chịu trách nhiệm về kết nối vật lý thực tế giữa các thiết bị. Lớp vật lý chưa thông tin dưới dạng bit. Nó chịu trách nhiệm truyền các bit riêng lẻ từ nút này sang nút tiếp theo. Khi nhận dữ liệu, lớp này sẽ nhận được tín hiệu và chuyển đổi nó thành 0s & 1s và gửi chúng đến lớp Data Link, lớp này sẽ đặt khung trở lại với nhau.
- Các chức năng:
  - Duy trì tốc độ dữ liệu (số bit mà người gửi có thể gửi mỗi giây)
  - Đồng bộ hoá các bit
  - Quyết định hướng truyền tải dữ liệu
  - Quyết định Cấu trúc liên kết vật lý (Physical Topologies)(Mesh, Star, Bus, Ring) 
  - Cung cấp các quyết định về Phương tiện vật lý & Giao diện
  - Cung cấp 2 kiểu định cấu hình: Point-to-Point và Multi-Point
  - Cung cấp giao diện giữa các thiết bị và phương tiện truyền dẫn
  - Có đơn vị dữ liệu giao thức tính bằng bit
  - Thiết bị Hubs, Ethernet được sử dụng tại lớp này
  - Thuộc danh mục Lớp phần cứng (chịu trách nhiệm cho tất cả các thiết lập và xử lý kết nối vật lý)
  - Cung cấp khía cách quan trọng được gọi là Modulation: quá trình chuyển đổi dữ liệu thành sóng vô tuyến bằng cách thêm thông tin vào tín hiệu thần kinh điện hoặc quang học
  - Cung cấp cơ chế chuyển mạnh trong đó các gói dữ liệu có thể được chuyển tiếp từ 1 cổng đến cổng đích hàng đầu
- Physical Topologies: Đại diện địa lý của các thiết bị liên kết. Có 4 loại:
  - `Mesh Topology`: Mỗi và mọi thiết bị phải có kết nối Point-to-Point chuyên dụng với mỗi và mọi thiết bị khác trong mạng. Nó bảo mật dữ liệu hơn vì có kết nối Point-to-Point chuyên dụng giữa 2 thiết bị. Rất khó cài đặt vì khá phức tạp.
![image](https://github.com/user-attachments/assets/de2978ee-c4b9-4cc3-a1ed-8aa5748754ec)
  - `Star Topology`: các thiết bị cần phải kết nối Point-to-Point chuyên dụng với bộ điều khiển hoặc hub. Nó dễ cài đặt và tái kết nối hơn so với Mesh Topology. Star Topology không có Fault Tolerance Technique.
    ![image](https://github.com/user-attachments/assets/bf519ff0-2f78-4357-8bdd-1f7677acf132)
  - `Bus Topology`: đa thiết bị được kết nối thông qua 1 cáp duy nhất được gọi là **backbone** với sự trợ giúp của các đường chạm và thả. Chi phí rẻ hơn so với Mesh và Star nhưng tái kết nối và cài đặt lại rất khó khăn
    ![image](https://github.com/user-attachments/assets/f4d8970e-89f9-481e-bb7c-f6759423c623)
  - `Ring Topology`: Mỗi thiết bị được kết nối với các bộ lặp trong 1 vòng giống vòng tròn. Mỗi thiết bị chỉ có thể gửi dữ liệu khi nó có mã thông báo, nếu không có mã thông báo thì không có thiết bị nào có thể gửi dữ liệu và mã thông báo được đặt bởi Màn hình
    ![image](https://github.com/user-attachments/assets/3c084f08-c545-4c0d-8a65-e2be47624f17)
- Line Configuration:
  - `Point-to-Point`: có một đường dẫn (liên kết) hoàn toàn dành riêng để mang dữ liệu giữa 2 thiết bị
  - `Multi-Point`: có 1 đường dẫn (liên kết) thông qua đó nhiều thiết bị được kết nối
- Modes of Transmission Medium (Phương thức truyền dẫn):
  - Simplex mode: trong số 2 thiết bị, chỉ có 1 thiết bị có thể truyền dữ liệu và thiết bị còn lại chỉ có thển nhận dữ liệu. VD: đầu vào từ bàn phím, màn hình, phát thanh, ...
  - Half Duplex Mode: trong số 2 thiết bị, cả 2 đều có thể gửi và nhận dữ liệu nhưng chỉ có 1 thiết bị tại một thời điểm không đồng thời
  - Full-Duplex mode: cả 2 thiết bị đều có thể gửi và nhận dữ liệu 1 cách đồng thời.
    
2. Lớp liên kết dữ liệu: Chịu trách nhiệm phân phối dữ liệu từ nút này đến nút khác, vai trò chính của nó là đảm bảo việc truyền thông thông tin không có lỗi. Nó cũng chịu trách nhiệm mã hoá, giải mã và tổ chức dữ liệu đi và đến
- Các lớp con của DLL:
  - Kiếm soát liên kết logic (Logical Link Control): Lớp con xử lý việc ghép kênh, luồng dữ liệu giữa các ứng dụng và các dịch vụ khác, và LLC cũng chịu trách nhiệm cung cấp giữa các thông báo lỗi và xác nhận
  - Kiểm soát truy cập phương tiện (Media Access Control): Lớp con quản lý sự tương tác của thiết bị, chịu trách nhiêm đánh địa chỉ các khung và kiểm soát việc truy cập phương tiện vật lý. Lớp liên kết dữ liệu nhận thông tin dưới dạng các gói từ lớp Mạng, nó chia các gói thành các khung và gửi các khung bit-by-bit đến lớp vật lý bên dưới
- Chức năng:
  - Đóng khung (Framing): Gói nhận được từ lớp Mạng được gọi là khung trong DLL. Ở phía người gửi, DLL nhận các gói tin từ lớp Mạng và chia chúng thành các khung nhỏ, sau đó gửi từng khung hình bit-by-bit đến lớp vật lý. Nó cũng gắn 1 số bit đặc biệt (để kiểm soát lỗi và đánh địa chỉ) ở đầu và cuối khung.
  - Addressing: đóng gói địa chỉ MAC/vật lý của nguồn và đích trong tiêu đề của mỗi khung để đảm bảo phân phối từ nút này đến nút khác.
  - `MAC address`: số phần cứng 48 bit duy nhất của máy tính được nhúng vào card mạng. Địa chỉ MAC còn được gọi là *Địa chỉ vật lý* của thiết bị mạng. Địa chỉ MAC là số thập lục phân gồm 12 chữ số (số nhị phân 6 bit), phần lớn được biểu thị bằng Colon-Hexademical. 6 chữ số đầu tiền của địa chỉ MAC xác định nhà sản xuất, được gọi là OUI (Organizational Unique Identifier). Các loại địa chỉ MAC:
    - Unicast: 1 khung có địa chỉ Unicast chỉ được gửi tới giao diện dẫn đến một NIC cụ thể. nếu LSB (Least Significant Bit) của octet đầu tiên địa chỉ nhận được đặt thành 0 thì nghĩa là khung chỉ tiếp nhận 1 NIC nhận. Địa chỉ MAC của máy nguồn luôn là Unicast
    - Multicast: cho phép nguồn gửi khung đến 1 nhóm thiết bị, trong địa chỉ Multicast lớp 2 (Ethernet), LSB octet đầu tiên của địa chỉ đặt được thành 1. IEEE đã phân bổ khối địa chỉ 01-80-C2-xx-xx-xx cho các địa chỉ nhóm để sử dụng theo các giao thức tiêu chuẩn
    - Boardcast: các khung Ethernet có tất cả các bit của địa chỉ đích (FF-FF-FF-FF-FF-FF) được gọi là địa chỉ quảng bá. Các khung có địa chỉ MAC FF-FF-FF-FF-FF-FF sẽ đến mọi máy tính thuộc phân đoạn mạng LAN đó
    - DLL sử dụng địa chỉ MAC. Đây là những mã định danh duy nhất được gán cho các giao diện mạng để liên lạc ở DLL. Chức năng chính là quản lý dữ liệu được truyền từ nút mạng này sang nút mạng khác trên cơ sở vật lý, hay còn được gọi là phân phối hop-to-hop
    - Ưu điểm:
      - **Tính duy nhất**: mỗi địa chỉ MAC là duy nhất, có nghĩa là các thiết bị trên mạng có thể dễ dàng được xác định và quản lý
      - **Tính đơn giản**: dễ cấu hình và quản lý, không yêu cầu bất kỳ cơ sở hạ tầng mạng bổ sung nào
      - **Khả năng tương thích**: được sử dụng rộng rãi và hỗ trợ bời nhiều công nghệ và giao thức mạng khác nhau, khiến chúng tương thích với nhiều hệ thống khác nhau
      - **Bảo mật**: có thể được sử dụng để hạn chế quyền truy cập vào mạng bằng cách chỉ cho phép các thiết bị có địa chỉ MAC được uỷ quyền kết nối
      - **Khả năng chịu lỗi**: trong trường hợp lỗi phần cứng hoặc mềm, thiết bị có thể dễ dàng thay thế mà không ảnh hưởng đến mạng, miễn là thiết bị mới có cùng địa chỉ MAC với thiết bị cũ
      - **Multicasting**: cho phép gửi 1 gói đến nhiều thiết bị mạng cùng 1 lúc
      - **Hiệu quả**: cho phép liên lạc hiệu quả trên mạng vì chúng cho phép các thiết bị nhận dạng và liên lạc với nhau 1 cách nhanh chóng và dễ dàng
      - **Chi phí mạng thấp hơn**: cho phép các thiết bị liên lạc trực tiếp với nhau mà không cần định tuyến hoặc đánh địa chỉ bổ sung
      - **Dễ khắc phục sự cố**: có thể sử dụng để khắc phục sự cố bằng cách xác định nguồn gốc của sự cố và theo dõi hoạt động mạng
      - **Tính linh hoạt**: được sử dụng để khắc phục sự cố mạng bằng cách xác định nguồn gốc của sự cố và theo dõi hoạt động mạng
    - Nhược điểm:
      - **Không gian địa chỉ hạn chế**: Địa chỉ MAC là số 48 bit, có thể hữu hạn. Điều này có thể dẫn đến xung đột địa chỉ nếu nhiều thiết bị có cùng địa chỉ MAC
      - **Giả mạo**: có thể dễ dàng bị giả mạo, cho phép các thiết bị trái phép truy cập vào mạng
      - **Tính kém hiệu quả**: địa chỉ MAC không được phân cấp, điều này có thể gây khó khăn cho việc quản lý các mạng lớn
      - **Địa chỉ tĩnh**: địa chỉ MAC thường được chỉ định tại thời điểm sản xuất và không dễ dàng thay đổi. Đây có thể là 1 bất lợi trong trường hợp thiết bị cần được cấu hình lại hoặc thay thế
      - **Phạm vi giới hạn**: chỉ được sử dụng để nhận dạng các thiết bị trong phân đoạn mạng cục bộ và không thể sử dụng để nhận dạng các thiết bị bên ngoài phân đoạn này
      - **Phụ thuộc vào phần cứng**: nếu NIC bị lỗi hoặc được thay thế thì địa chỉ MAC cũng thay đổi
      - **Thiếu mã hoá**: địa chỉ MAC được gửi dưới dạng văn bản thuần tuý, điều này có thể khiến chúng dễ bị chặn và nghe lén
      - **Không có bảo mật vốn có**: Tính năng lọc MAC có thể được sử dụng để hạn chế quyền truy cập vào mạng nhưng địa chỉ MAC không cung cấp bất kỳ tính năng bảo mật nào.
      - **Xung đột địa chỉ MAC**: Trong 1 số trường hợp hiếm gặp, các địa chỉ MAC có thể xung đột, điều này có thể gây gián đoạn mạng và gây khó khăn cho việc xác định và quản lý các thiết bị trên mạng
  - Kiểm soát lỗi: Dữ liệu có thể bị hỏng do nhiều lý do khác nhau như nhiễu, suy giảm, ... Trách nhiệm của DLL là phát hiện lỗi trong dữ liệu được truyền và sửa lỗi bằng cách sử dụng các kỹ thuật phát hiện và sửa lỗi tương ứng. DLL thêm các bit phát hiện lỗi vào tiêu đề của khung để người nhận có thể kiếm tra dữ liệu nhận được có chính xác hay không. Nó tăng thêm độ tin cậy cho lớp vật lý bằng cách thêm các cơ chế để phát hiện và truyền lại các khung bị hỏng hoặc bị mất
  - Kiếm soát dòng chảy: Nếu tốc độ nhận của người nhận thấp hơn tốc độ gửi của người gửi thì điều này có thể dẫn đến tràn bộ đệm của người nhận và 1 số khung có thể bị mất. DDL đồng bộ hoá tốc độ của người gửi và người nhận và thiết lập luồng kiểm soát giữa chúng
  - Kiếm soát truy cập: Khi nhiều thiết bị chia sẻ cùng 1 kênh liên lạc thì có khả năng xảy ra xung đột cao, do đó, DLL kiếm tra xem thiết bị nào có quyền kiểm soát kênh
- Các giao thức trong DLL:
  - Giao thức liên kết dữ liệu đồng bộ (Synchronous Data Link Control): giao thức truyền thông của máy tính. Nó thường hỗ trợ các liên kết đa điểm, thậm chí khôi phục lỗi hoặc sửa lỗi. Nó thường được sử dụng để mang lưu lượng SNA (System Network Architecture) và là tiền thân của HDLC. Nó cũng được sử dụng để kết nối tất cả các thiết bị từ xa với máy tính lớn tại các vị trí trung tâm có thể ở các kết nối Point-to-Point (1-1) hoặc Point-to-Multipoint (1-n). Nó cũng được sử dụng để đảm bảo rằng các đơn vị dữ liệu phải đến chính xác và với luồng phù hợp từ 1 điểm mạng đến điểm mạng tiếp theo
  - Giao thức liên kết dữ liệu cấp cao (High-Level Data Link Control): giao thức thường dựa trên SDLC. Nó cũng cung cấp nỗ lực tốt nhất, dịch vụ không đáng tin cậy và dịch vụ đáng tin cậy. HDLC là 1 giao thức hướng bit có thể áp dụng cho cả giao tiếp Point-to-Point và Multi-Point
  - Giao thức giao diện dòng nối tiếp (Serial Line Interface Protocol): là 1 giao thức cũ hơn chỉ được sử dụng để thêm 1 byte đóng khung ở cuối gói IP. Nó là 1 cơ sở kiếm soát liên kết dữ liệu được yêu cầu để chuyển các gói IP, thường là giữa các Nhà cung cấp dich vụ Internet (ISP) và người dùng gia đình qua liên kết quay số. Nó là 1 gói gọn của TCP/IP được thiết kế đặc biệt để làm việc với các cổng nối tiếp và 1 số kết nối bộ định tuyến chỉ để liên lạc. Đó là 1 số hạn chế như: không cung cấp các cơ chế như sửa lỗi hoặc phát hiện lỗi.
  - Giao thức Điểm-Điểm (Point-to-Point Protocol): là 1 giao thức cơ bản được sử dụng để cung cấp chức năng tương tự như SLIP. Đây là giao thức mạnh mẽ nhất được sử dụng để vận chuyển các loại gói khác cùng với gói IP. Nó cũng có thể được yêu cầu cho các đường dây bộ định tuyến-bộ định tuyến quay số. Về cơ bản, nó cung cấp phương pháp đóng khung để mô tả các khung. Nó là 1 giao thức hướng ký tự và được sử dụng để phát hiện lỗi. Nó cũng được sử dụng để cung cấp 2 giao thức NCP và LCP. LCP được sử dụng để đưa các đường dây lên, đàm phán các tuỳ chọn, đưa chúng xuống trong khi NCP được sử dụng để đàm phán các giao thức lớp mạng. Nó được yêu cầu cho các giao diện nối tiếp giống như HDLC.
  - Giao thức điều khiển liên kết (Link Control Protocol): Được sử dụng để cung cấp các dịch vụ kiểu HDLC trên mạng LAN. LCP cơ bản là 1 giao thức PPP được sử dụng để thiết lập, cấu hình, kiểm tra, bảo trì và kết thúc hoặc chấm dứt các liên kết để truyền các khung dữ liệu
  - Quy trình truy cấp liên kết (Link Access Procedure): là 1 giao thức DLL được yêu cầu để đóng khung và truyền dữ liệu qua các liên kết Point-to-Point. Nó cũng bao gồm 1 số tính năng dịch vụ đáng tin cậy. Có 3 loại LAP, bao gồm: LAPB (Balanced), LAPD (D-Channel) và LAPF (Frame-Mode Bearer Services)
  - Giao thức điều khiển mạng (Network Control Protocol): Cho phép người dùng có quyền truy cập để sử dụng máy tính và 1 số thiết bị tại các điểm từ xa và cũng có thể truyền tệp giữa 2 hoặc nhiều máy tính. Nó thường là 1 tập hợp các giao thức đang tạo thành 1 phần của PPP. NCP luôn có sẵn cho mỗi và mọi giao thức lớp cao hơn được hỗ trợ bởi PPP

3. Lớp mạng: là 1 phần quá trình giao tiếp trong mạng máy tính. Công việc chính là di chuyển các gói dữ liệu giữa các mạng khác nhau. Nó giúp định tuyến các gói này từ người gửi đến người nhận qua nhiều đường dẫn và mạng. Kết nối mạng với mạng cho phép Internet hoạt động. Các kết nối này xảy ra ở "lớp mạng", gửi các gói dữ liệu giữa các mạng khác nhau. Giao thức Internet (IP) là giao thức chính được sử dụng ở lớp này, cùng với các giao thức khác để định tuyến, kiểm tra và mã hoã
