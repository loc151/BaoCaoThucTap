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

`Tổng quan về các lớp`
1. Lớp vật lý: là lớp thấp nhất của mô hình tham chiếu OSI. Nó chịu trách nhiệm về kết nối vật lý thực tế giữa các thiết bị. Lớp vật lý chứa thông tin dưới dạng bit. Nó chịu trách nhiệm truyền các bit riêng lẻ từ nút này sang nút tiếp theo. Khi nhận dữ liệu, lớp này sẽ nhận được tín hiệu và chuyển đổi nó thành 0s & 1s và gửi chúng đến lớp Data Link, lớp này sẽ đặt khung trở lại với nhau.
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
  - `Simplex mode`: trong số 2 thiết bị, chỉ có 1 thiết bị có thể truyền dữ liệu và thiết bị còn lại chỉ có thể nhận dữ liệu. VD: đầu vào từ bàn phím, màn hình, phát thanh, ...
  - `Half Duplex Mode`: trong số 2 thiết bị, cả 2 đều có thể gửi và nhận dữ liệu nhưng chỉ có 1 thiết bị tại một thời điểm không đồng thời
  - `Full-Duplex mode`: cả 2 thiết bị đều có thể gửi và nhận dữ liệu 1 cách đồng thời.
    
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

3. Lớp mạng: là 1 phần quá trình giao tiếp trong mạng máy tính. Công việc chính là di chuyển các gói dữ liệu giữa các mạng khác nhau. Nó giúp định tuyến các gói này từ người gửi đến người nhận qua nhiều đường dẫn và mạng. Kết nối Network-to-network cho phép Internet hoạt động. Các kết nối này xảy ra ở "lớp mạng", gửi các gói dữ liệu giữa các mạng khác nhau. Giao thức Internet (IP) là giao thức chính được sử dụng ở lớp này, cùng với các giao thức khác để định tuyến, kiểm tra và mã hoã
- Đặc điểm:
  - Mang các gói dữ liệu từ nguồn đến đích mà không thay đổi hoặc sử dụng chúng
  - Nếu các gói quá lớn để phan phối, chúng sẽ bị phân mảnh - chia thành các gói nhỏ hơn
  - Quyết định tuyến đường mà các gói sẽ đi từ nguồn đến đích trong số nhiều tuyến có sẵn trong mạng (định tuyến)
  - Địa chỉ nguồn và đích được thêm vào các gói dữ liệu bên trong lớp mạng.
- Các dịch vụ:
  - `Đóng gói (Packetizing)`: Quá trình đóng gói dữ liệu nhận được từ các lớp trên của mạng (tải trọng) trong gói lớp mạng tại nguồn và giải mã tải trọng từ gói lớp mạng tại đích
    ![image](https://github.com/user-attachments/assets/a1e7eaae-a436-420d-b303-fc3b22efca84)
    - Máy chủ nguồn thêm 1 tiêu đề chứa địa chỉ nguồn và đích cũng như 1 số thông tin liên quan khác mà giao thức lớp mạng yêu cầu vào tải trọng nhận được từ giao thức lớp trên và phân phối gói đến lớp liên kết dữ liệu
    - Máy chủ đích nhận gói lớp mạng từ lớp liên kết dữ liệu của nó, giải mã gói và phân phối tải trọng đến giao thức lớp trên tương ứng. Các bộ định tuyến trong đường dẫn không được phép thay đổi địa chỉ nguồn hoặc đích. Các bộ định tuyến trong đường dẫn không được phép giải mã các gói mà chúng nhận được trừ khi chúng cần được phân mảnh.
  - `Định tuyến (Routing)`: là quá trình di chuyển dữ liệu từ thiết bị này sang thiết bị khác. Đây là 2 dịch vụ khác được cung cấp bởi lớp mạng.
    - Trong 1 mạng, có 1 số tuyến đường có sẵn từ nguồn đến đích.
    - Lớp mạng chỉ định 1 số chiến lược tìm ra tuyến đường tốt nhất có thể
    - Có 1 số giao thức định tuyến được sử dụng trong quá trình này và chúng nên được chạy để giúp các bộ định tuyến phối hợp với nhau và giúp thiết lập liên lạc trên toàn mạng
    ![image](https://github.com/user-attachments/assets/cd41f88e-8b1c-4f64-9c38-423b7c3077e9)
  - `Forwarding (Chuyển tiếp)`: Hành động được áp dụng bởi mỗi bộ định tuyến khi gói đến 1 trong các giao diện của nó
    - Khi 1 bộ định tuyến nhận được 1 gói từ 1 trong các mạng được đính kém của nó, nó cần chuyển tiếp gói đó đến một mạng được đính kèm khác (unicast routing) hoặc tới 1 số mạng được đính kèm (multicast)
    - Bộ định tuyến được sử dụng trên mạng để chuyển tiếp gói từ mạng cục bộ sang mạng từ xa.
    - Quá trình định tuyến liên quan đến việc chuyển tiếp gói từ giao diện đầu vào sang giao diện thoát
  ![image](https://github.com/user-attachments/assets/e09fd2a5-7820-4060-846a-cf6122740bad)
<p>
  
**So sánh giữa Routing và Forwarding** <p>
  
|Routing|Forwarding|
|:--|:--|
|Quá trình di chuyển dữ liệu từ thiết bị này sang thiết bị khác|Hành động được áp dụng bởi mỗi bộ định tuyển khi gói đến 1 trong các giao diện của nó|
|Hoạt động trên lớp mạng|Hoạt động trên lớp mạng|
|Công việc dựa trên bảng chuyển tiếp|Kiếm tra bảng chuyển tiếp và làm việc theo đó|
|Hoạt động trên Routing Information Protocol (RIP) |Hoạt động trên Encapsulating Security Payloads (UDP)|

  - Ưu điểm:
    - Dịch vụ đóng gói trong lớp mạng giúp dễ dàng vận chuyển các gói dữ liệu
    - Việc đóng gói cũng loại bỏ các điểm lỗi duy nhất trong hệ thống truyền thông dữ liệu
    - Giảm lưu lượng mạng bằng cách tạo các miền xung đột và quảng bá
    - Các gói dữ liệu được chuyển từ nơi này sang nơi khác trong mạng với sự trợ giúp của Forwarding
  - Nhược điểm:
    - Thiếu sự kiểm soát luồng trong thiết kế của lớp mạng
    - Sự tắc nghẽn đôi khi xảy ra do có quá nhiều datagram vượt quá khả năng của mạng hoặc bộ định tuyến. Do đó, 1 số bộ định tuyến có thể loại bỏ 1 số datagram và 1 số thông tin quan trọng có thể bị mất
    - Thiếu cơ chế kiểm soát lỗi thích hợp do sự hiện diện của các gói dữ liệu bị phân mảnh nên việc kiểm soát lỗi trở nên khó thực hiện 

4. Lớp vận chuyển: Là lớp end-to-end được sử dụng để gửi tin nhắn đến máy chủ. Nó được gọi là lớp end-to-end vì nó cung cấp kết nối point-to-point. Đơn vị đóng gói dữ liệu trong lớp vận chuyển là 1 phân đoạn
- Hoạt động: Nhận các dịch vụ từ lớp Ứng dụng và cung cấp các dịch vụ cho lớp Mạng
  - Ở phía người gửi: Lớp vận chuyển nhận dữ liệu (tin nhắn) từ lớp Ứng dụng và sau đó thực hiện Phân đoạn, chia tin nhắn thực tế thành các phân đoạn, thêm số cổng của nguồn và đích vào tiêu đề của phân đoạn và chuyển tin nhắn đến lớp Mạng
  - Ở phía người nhận: Lớp vận chuyển nhận dữ liệu từ lớp Mạng, tập hợp lại các dữ liệu đã phân đoạn, đọc tiêu đề, xác đinh số cổng và chuyển tiếp tin nhắn đến cổng thích hợp trong lớp Ứng dụng.
- Trách nhiệm:
  - Quy trình xử lý giao vận: yêu cầu số cổng để phân phối chính xác các phân đoạn dữ liệu đến đúng quy trình trong số nhiều quy trình đang chạy trên 1 máy chủ cụ thể. Số cổng là địa chỉ 16 bit được sử dụng để nhận dạng duy nhất bất kỳ chương trình client-server
  ![image](https://github.com/user-attachments/assets/decec4cd-9b79-413f-a273-44452a044039)

  - Kết nối đầu cuối giữa các máy chủ: chủ yếu sử dụng TCP và UDP
  ![image](https://github.com/user-attachments/assets/216e5c07-72b1-4c60-802f-140c630da4e7)

  - Ghép kênh và phân kênh:
    - `Ghép kênh (Multiplexing)`: khi dữ liệu được lấy từ 1 số quy trình từ người gửi và được hợp nhất thành 1 gói cùng với các tiêu đề và được gửi dưới dạng 1 gói duy nhất. Ghép kênh cho phép sử dụng đồng thời các quy trình khác nhau trên mạng đang chạy trên máy chủ. Các tiến trình được phân biệt bằng số cổng của chúng
    - Phân kênh (Demultiplexing): yêu cầu ở phía người nhận khi tin nhắn được phân phối thành các quy trình khác nhau. Transport nhận các phân đoạn dữ liệu từ lớp mạng phân phối và phân phối nó đến quy trình thích hợp chạy trên máy tính của người nhận
    ![image](https://github.com/user-attachments/assets/5fbf6b9a-df0b-46b8-8c86-95296385878f)
  - Kiểm soát tắc nghẽn:
    - Tắc nghẽn (Congestion): là tình huống trong đó có quá nhiều nguồn trên mạng cố gắng gửi dữ liệu và bộ đệm của bộ định tuyến bắt đầu tràn do mất gói. Kết quả là việc truyền lại các gói tin từ các nguồn sẽ làm tăng thêm tình trạng tắc nghẽn.
    - Lớp vận chuyển sử dụng điều khiển tắc nghẽn vòng hở để ngăn ngừa tắc nghẽn và điều khiển tắc nghẽn vòng kín để loại bỏ tắc nghẽn trong mạng khi nó xảy ra
    ![image](https://github.com/user-attachments/assets/b291c66d-1cf3-47d9-88d0-f15430b2bcf8)
  - Tính toán tính toàn vẹn dữ liệu và sửa lỗi: Kiểm tra lỗi trong các tin nhắn đến từ lớp ứng dụng bằng cách sử dụng mã phát hiện lỗi và tính toán tổng kiểm tra. Nó kiếm tra xem dữ liệu nhận được có bị hỏng hay không và sử dụng các dịch ACK và NACK để thông báo cho người gửi nếu dữ liệu đã đến hoặc không và kiểm tra tính toàn vẹn của dữ liệu.
  ![image](https://github.com/user-attachments/assets/d942e34f-738d-47ae-8452-2c9fed494ec9)
  - Kiểm soát dòng chảy
- Các giao thức của tầng vận chuyển:
  - `Transmission Control Protocol (TCP)`: giao thức điều khiển truyền dẫn là giao thức hướng kết nối để liên lạc giúp trao đổi tin nhắn giữa các thiết bị khác nhau qua mạng. Giao thức Internet (IP) thiết lập kỹ thuật gửi gói dữ liệu giữa các máy tính, hoạt động với TCP
    - Internet Protocol (IP): là phương thức hữu ích để gửi dữ liệu từ thiết bị này qua thiết bị khác từ khắp nơi trên internet. Nó là 1 bộ quy tắc quản lý cách gửi và nhận dữ liệu qua internet. Nó chịu trách nhiệm đánh địa chỉ và định tuyến các gói dữ liệu để chúng có thể di chuyển từ người gửi đến đích chính xác trên nhiều mạng. Mỗi thiết bị chỉ có duy nhất 1 địa chỉ IP giúp thiết bị liên lạc vào trao đổi dữ liệu giữa các thiết bị khác có trên Internet
- Cách hoạt động: Chia dữ liệu thành các gói nhỏ và tập hợp các gói đó thành thông báo gốc để đảm bảo rằng mỗi thông báo đều đến được vị trí đích 1 cách nguyên vẹn. Điều này giúp việc duy trì hiệu quả trở lên đơn giản hơn so với việc gửi mọi thứ cùng 1 lúc
  ![image](https://github.com/user-attachments/assets/6e171771-f26f-4180-ae74-8aa5f9e539fc)

  - Ưu điểm:
    - Là giao thức đáng tin cậy
    - Cung cấp cơ chế kiểm tra lỗi cũng như cơ chế phục hồi
    - Cho phép kiểm soát dòng chảy
    - Đảm bảo rằng dữ liệu đến đúng đích theo đúng thứ tự được gửi
    - Được ghi chép đầy đủ và được triển khai rộng rãi, được duy trì bởi các tổ chức tiêu chuẩn
    - Hoạt động cùng IP để thiết lập kết nối giữa các thiết bị trên mạng
  - Nhược điểm:
    - Kích thước lớn có thể trở thành vấn đề đối với các mạng nhỏ có tài nguyên thấp
    - Chạy nhiều lớp nên có thể làm chậm tốc độ mạng
    - Không có tính chất chung, tức là không thể biểu diễn bất kỳ ngăn xếp giao thức nào ngoài TCP/IP
    - Không có cập nhật nào kể từ 30 năm trước
  - User Datagram Protocol (UDP): Giao thức gói dữ liệu người dùng là một trong những giao thức cốt lõi của bộ IP. Nó là một giao thức truyền thông được sử dụng trên Internet như phát video hay tìm kiếm DNS. UDP không kết nối và không đảm bảo phân phối, ưu tiên và kiểm tra lỗi, làm cho nó trở nên nhẹ và hiệu quả cho 1 số loại truyền dữ liệu nhất định.
  ![image](https://github.com/user-attachments/assets/94cd2417-bd23-49f4-976a-17c668dba663)
    - `UDP Header`: là 1 tiêu đề cố định và đơn giản với 8 byte. 8 byte đầu tiên chứa tất cả thông tin cần thiết và phần còn lại bao gồm dữ liệu. Các trường số cổng UDP dài mỗi trường 16 bit, do đó phạm vi cho số cổng được xác định từ 0 -> 65535; cổng số 0 được dành riêng. Số cổng giúp phân biệt các yêu cầu hoặc quy trình khác nhau của người dùng
    ![image](https://github.com/user-attachments/assets/c6d6aacc-ec28-4c79-a851-dca07b00e7c7)
    - Cổng nguồn: dùng để xác định số cổng của nguồn, dài 2 Byte
    - Cổng đích: dùng để xác định cổng của gói tin đích (2 Byte)
    - Độ dài: bao gồm tiêu đề và dữ liệu (2 Byte)
    - Tổng kiểm tra: Phần bổ sung 16 bit của checksum UDP Header, pseudo-header từ IP header và dữ liệu, được đệm bằng 0 octet ở cuối (nếu cần) để tạo bội số của 2 octet
  - Ứng dụng:
    - Sử dụng cho giao tiếp Request-Respond đơn giản
    - Phù hợp để đa hướng vì UDP hỗ trợ chuyển đổi gói
    - Được sử dụng cho 1 số giao thức cập nhật định tuyến như RIP
    - Sử dụng cho các ứng dụng thời gian thực không thể chịu được sự chậm trễ không đồng đều giữa các phần tin nhắn đã nhận
    - Các dịch vụ VoIP (Voice over Internet Protocol)
    - DNS (Domain Name System)
    - DHCP (Dynamic Host Configuration Protocol)
  - Ưu điểm:
    - `Tốc độ`: nhanh hơn TCP do không có thiết lập kết nối và đảm bảo phân phối dữ liệu đáng tin cậy
    - `Độ trễ thấp hơn`: Độ trễ thấp hơn và thời gian phản hồi nhanh hơn
    - `Đơn giản`: thiết kế giao thức đơn giản hơn TCP, giúp thực hiện và quản lý dễ dàng hơn
      
5. Lớp phiên: Cho phép người dùng trên các máy khác nhau thiết lập các phiên liên lạc tích cực giữa chúng. Nó chịu trách nhiệm thiết lập, duy trì, đồng bộ hoá, chấm dứt các phiên giữa các ứng dụng của người dùng cuối.
- Thiết lập kết nối giữa các thực thể phiên
- Xử lý và thao tác dữ liệu mà nó nhận được
- Hoạt động: Để thiết lập kết nối phiên, ta cần:
  - Ánh xạ địa chỉa phiên tới địa chỉ giao vận
  - Lựa chọn các thông số chất lượng dịch vụ truyền tải (Quality of Service) được yêu cầu
  - Quan tâm đến các cuộc đàm phán sẽ xảy ra giữa các tham số phiên
  - Truyền thêm dữ liệu người dùng minh bạch có giới hạn
  - Theo dõi giai đoạn Truyền dữ liệu đúng cách
- Chức năng:
  - Cho phép các hệ thống giao tiếp ở chế độ bán song công hoặc song công hoàn toàn
  - Quản lý mã thông báo, ngăn cản 2 người dùng truy cập đồng thời hoặc thực hiện cùng 1 hoạt động quan trọng
  - Đồng bộ hoá bằng cách cho phép quá trình thêm các điểm kiểm tra, được coi là điểm đồng bộ hoá cho các luồng dữ liệu
  - Kiểm tra và phục hồi phiên
  - Cung cấp cơ chế mở, đóng và quản lý phiên giữa các quy trình ứng dụng của người dùng cuối
  - Các dịch vụ thường được triển khai trong môi trường ứng dụng bằng cách sử dụng cách lệnh gọi thủ tục từ xa (Remote Procedure Calls)
  - Chịu trách nhiệm đồng bộ hoá thông tin từ các nguồn khác nhau
  - Kiểm soát các kết nối đơn hoặc nhiều cho từng ứng dụng của người dùng cuối và giao tiếp trực tiếp với cả 2 lớp Trình bày và Vận chuyển
  - Tạo ra các thủ tục để checkpoint, sau đó là hoãn lại, khởi động hoặc chấm dứt
  - Sử dụng các điểm kiểm tra để kích hoạt các phiên giao tiếp sẽ được nối lại từ điểm kiểm tra, tại nơi xảy ra lỗi giao tiếp
  - Tìm nạp hoặc nhận thông tin dữ liệu từ lớp trước đó và gửi thêm dữ liệu từ lớp đến sau nó
- Các giao thức:
  - AppleTalk Data Stream Protocol (ADSP): được phát triển bởi Apple, nó cho phép kết nối mạng cục bộ mà không cần thiết lập trước
  - Real-time Transport Control Protocol (RTCP): cung cấp thông tin điều khiển và thống kê ngoài băng tần cho phiên RTP. RTCP cung cấp phản hồi về QoS trong phân phối phương tiện bằng cách gửi định kỳ thông tin thống kê như octet được truyển và số lượng gói hoặc mất gói cho những người tham gia phiên truyền phát đa phương tiện
  - Point-to-Point Tunneling Protocol (PPTP): là giao thức cung cấp phương thức triển khai mạng riêng ảo. PPTP sử dụng kênh điều khiển TCP và đường hầm Đóng gói định tuyến chung để đóng gói các gói PPP, cung cấp các cấp độ bảo mật và cấp độ truy cập từ xa tương đương với các sản phẩm VPN thông thường
  - Password Authentication Protocol (PAP): giao thức xác thực dựa trên mật khẩu được sử dụng bởi PPP để xác thực người dùng. Xác thực PAP được thực hiện tại thời điểm thiết lập liên kết ban đầu và xác minh danh tính của khách hàng bằng cách bắt tay 2 chiều
  - Remote Procedure Call Protocol (RPCP): là giao thức được sử dụng khi 1 chương trình máy tính khiến 1 thủ tục (hoặc 1 quy trình con) thực thi trong 1 không gian địa chỉ khác mà không cần lập trình viên mã hoá rõ ràng các chi tiết cho sự tương tác từ xa
  - Sockets Direct Protocol (SDP): giao thức hỗ trợ các luồng ổ cắm qua kết cấu mạng Truy cập bộ nhớ trực tiếp từ xa (Remote Direct Memory Access)
 
6. Lớp trình bày: đóng vai trò là trình dịch dữ liệu cho mạng. Trách nhiệm chính là cung cấp hoặc xác định định dạng dữ liệu và mã hoá, duy trì cú pháp thích hợp của dữ liệu mà nhận hoặc truyền đến các lớp khác
- Chức năng:
  - Định dạng lớp trình bày và mã hoá dữ liệu được gửi qua mạng
  - Đảm bảo dữ liệu được gửi theo cách mà người nhận sẽ hiểu thông tin và có thể sử dụng dữ liệu 1 cách hiệu quả
  - Quản lý các cấu trúc dữ liệu trừu tượng và cho phép các cấu trúc dữ liệu cấp cao được xác định và trao đổi
  - Thực hiện mã hoá tại máy phát và giải mã tại máy thu
  - Thực hiện nén dữ liệu để giảm băng thông của dữ liệu được truyền
  - Chịu trách nhiệm về khả năng tương tác giữa các phương pháp mã hoá
  - Xử lý phần trình bày của dữ liệu
  - Tích hợp tất cả các định dạng thành 1 định dạng chuẩn hoá để giao tiếp hiệu quả
  - Mã hoá thông điệp từ định dạng phụ thuộc vào người dùng sang định dạng chung và ngược lại để giao tiếp giữa các hệ thống khác
  - Xử lý cú pháp và ngữ nghĩa của thông điệp
  - Dịch, định dạng và phân phối thông tin để xử lý hoặc hiển thị
  - Tuần tự hoá
- Tính năng:
  - Áp dụng 1 số kỹ thuật nén phức tạp nhất định, do đó cần ít byte dữ liệu hơn để biểu diễn thông tin khi nó được gửi qua mạng
  - Chịu trách nhiệm thêm mã hoá ở đầu người gửi và giải mã hoá ở đầu người nhận
  - Định dạng và mã hoá dữ liệu được gửi qua mạng, cung cấp sự tự do khỏi các vấn đề tương thích
  - Chịu trách nhiệm nén dữ liệu mà nó nhận được từ lớp ứng dụng trước khi phân phối nó đến lớp phiên
- Các giao thức:
  - Apple Filing Protocol (AFP)
  - Lightweight Presentation Protocol (LPP)
  - NetWare Core Protocol (NCP)
  - Network Data Representation (NDR)
  - External Data Representation (XDR): tiêu chuẩn để mô tả và mã hoá dữ liệu. Nó truyền dữ liệu giữa các kiến trúc máy tính và được sử dụng để giao tiêp giữa các máy rất đa dạng
  - Secure Socker Layer (SSL): Cung cấp bảo mật cho dữ liệu được chuyển giữa trình duyệt web và máy chủ. SSL mã hoá liên kết giữa máy chủ web và trình duyệt, đảm bảo rằng tất cả dữ liệu được truyền giữa chúng vẫn riêng tư và không bị tấn công

  7. Lớp ứng dụng: Cho phép truy cập mạng 1 cách dễ dàng bằng cách cung cấp 1 số cách để thao tác dữ liệu
- Chức năng:
  - Cung cấp phương tiện để người dùng có thể chuyển tiếp 1 số email và nó cũng cung cấp phương tiện lưu trữ
  - Cho phép người dùng truy cập, truy xuất và quản lý các tệp trong máy tính từ xa
  - Cho phép người dùng đăng nhập như 1 máy chủ từ xa
  - Cung cấp quyền truy cập vào thông tin toàn cầu về các dịch vụ khác nhau
  - Cung cấp các dịch vụ: e-mail, truyền tệp, phân phối kết quả cho người dùng, dịch vụ thư mục, tài nguyên mạng
  - Cung cấp các giao thức cho phép phần mềm gửi và nhận thông tin cũng như trình bày dữ liệu có ý nghĩa
  - Xử lý các vấn đề như tính minh bạch của mạng, phân bổ tài nguyên
  - Đóng vai trò như 1 cửa sổ để người dùng và quy trình ứng dụng truy cập các dịch vụ mạng
  - Thực hiện các chức năng
  - Giúp xác định các đối tác liên lạc và đồng bộ hoá liên lạc
  - Cho phép người dùng tương tác với các ứng dụng phần mềm khác
  - Dữ liệu ở dạng trực quan, giúp người dùng hiểu và ghi nhớ
  - Thực hiện khởi tạo máy chủ, sau đó đăng nhập từ xa vào máy chủ
- Hoạt động:
  - Máy client gửi lệnh đến máy chủ và khi máy chủ nhận được lệnh đó, nó sẽ cấp phát số cổng cho máy khách
  - Máy client gửi yêu cầu khởi tạo kết nối đến máy chủ và khi máy chủ nhận được yêu cầu, nó sẽ đưa ra xác nhận cho máy client thông qua máy client đã thiết lập thành công kết nối với server
  - Máy client có quyền truy cập vào máy chủ, qua đó nó có thể yêu cầu máy chủ gửi bất kỳ loại tệp hoặc tài liệu nào khác hoặc nó có thể tải lên 1 số tệp hoặc tài liệu chính trên server
- Tính năng:
  - Xác định quy trình cho cả 2 bên tham gia giao tiếp
  - Xác định loại tin nhắn được gửi hoặc nhận từ bất kỳ phía nào (nguồn hoặc đích)
  - Xác định cú pháp cơ bản của tin nhắn được chuyển tiếp hoặc lấy về
  - Xác định cách gửi tin nhắn và phản hồi mong đợi
  - Xác định sự tương tác với cấp độ tiếp theo
- Dịch vụ:
  - Cung cấp giao diện giữa người dùng và ứng dụng
  - Sử dụng để đăng nhập từ xa
  - Sử dụng để chuyển tập tin
  - Sử dụng cho các dịch vụ thư và chuyển khoản
  - Sử dụng để chuyển các tập tin đa phương tiện
  - Chia sẻ tài nguyên
  - Đồng bộ hoá dữ liệu
  - Dịch vụ xác thực
- Các giao thức:
  - Telnet (Telecommunications Network): sử dụng để quản lý các tập tin qua Internet. Cho phép các máy client truy cập vào tài nguyên của Telnet server. Telnet sử dụng cổng 23
  - DNS: Dịch vụ DNS dịch tên miền thành địa chỉ IP tương ứng. Giao thức DNS sử dụng cổng số 53
  - DHCP (Dynamic Host Configuration Protocol): Cung cấp địa chỉ IP cho máy chủ. Bất cứ khi nào 1 máy chủ cố gắng đăng ký địa chỉ IP với máy chủ DHCP, máy chủ DHCP sẽ cung cấp nhiều thông tin cho máy chủ tương ứng. DHCP sử dụng cổng 67 và 68
  - FTP: Chuyển các tệp tin khác nhau từ thiết bị này sang thiết bị khác. FTP thúc đẩy việc chia sẻ tập tin qua các thiết bị máy tính từ xa với khả năng truyền dữ liệu hiệu quả. FTP sử dụng cổng số 20 để truy cập dữ liệu và cổng số 21 để kiểm soát dữ liệu
  - SMTP: Chuyển thư điện tử từ người dùng này sang người dùng khác. SMTP sử dụng cổng 25 và 587
  - HTTP: là nền tảng của WWW. HTTP hoạt động trên mô hình client-server. HTTP sử dụng để truyền các tài liệu hypermedia như HTML. Giao thức được thiết kế đặc biệt để liên lạc giữa trình duyệt web và máy chủ web. HTTP là 1 giao thức không trạng thái, sử dụng cổng 80
