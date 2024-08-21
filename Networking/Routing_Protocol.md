# Báo cáo thực tập 3
## Networking
### Routing protocol: Cơ chế truyền thông quan trọng chi phối cách các gói dữ liệu từ nguồn đến đích. Định tuyến hiệu quả đảm bảo rằng dữ liệu được truyền qua mạng 1 cách hiệu quả, đáng tin cậy và kịp thời

### Định tuyến tĩnh (Static Routing): còn được gọi là định tuyến không thích ứng, không thay đổi bảng định tuyến trừ khi quản trị viên mạng thay đổi hoặc sửa đổi chúng theo cách thủ công. Định tuyến tĩnh không sử dụng các thuật toán định tuyến phức tạp và cung cấp bảo mật cao hơn định tuyến động
![image](https://github.com/user-attachments/assets/1c12bfcb-4f7e-4cf5-a1be-c45f3adde3a8)
- Ưu điểm:
  - Không có chi phí định tuyến CPU bộ định tuyến, có nghĩa là 1 bộ định tuyến rẻ hơn có thể được sử dụng để định tuyến
  - Bổ sung bảo mật vì chỉ quản trị viên mới có thể cho phép định tuyến đến các mạng cụ thể
  - Không sử dụng băng thông giữa các bộ định tuyến
- Nhược điểm:
  - Đối với 1 mạng lớn, đó là 1 nhiệm vụ bận rộn đối với quản trị viên để thêm thủ công từng tuyến đường cho mạng trong bảng định tuyển trên mỗi bộ định tuyến
  - Quản trị viên nên có kiến thức tốt về cấu trúc liên kết.

 ### Open Shortest Path First (OSPF): giao thức định tuyến trạng thái liên kết được sử dụng để tìm đường dẫn tốt nhất giữa nguồn và bộ định tuyến đích bằng cách sử dụng SPF của riêng nó. Giao thức định tuyến trạng thái liên kết là 1 giao thức sử dụng khái niệm cập nhật được kích hoạt, tức là, nếu có sự thay đổi được quan sát thấy trong bảng định tuyến đã học thì các bản cập nhật chỉ được kích hoạt.
- Tiêu chí: để hình thành 1 liên kết trong OSPF, có 1 tiêu chí cho cả 2 bộ định tuyến:
  - Nó nên có mặt trong cùng 1 khu vực
  - Bộ định tuyến ID sẽ là duy nhất
  - Mặt nạ mạng con phải giống nhau
  - Hello và thời gian chết phải giống nhau
  - Cờ sơ khai phải khớp
  - Xác thực phải khớp
- OSPF hỗ trợ NULL, văn bản thuần tuý và xác thực MD5 <p>
**Note:** Cả 2 bộ định tuyến phải bật 1 số loại xác thực
- Thông điệp OSPF: sử dụng 1 số thông điệp nhất định để liên lạc giữa các bộ định tuyến vận hành OSPF
  - Tin nhắn Hello: là những tin nhắn lưu trữ được sử dụng để khám phá/phục hồi lân cận. Chúng được trao đổi cứ sau 10 giây. Điều này bao gồm: Bộ định tuyến I'd, khoảng thời gian hello/dead, Khu vực I'd, ưu tiên bộ định tuyến, địa chỉ IP DR và BRD, dữ liệu xác thực
  - Database Description (DBD): là tuyến OSPF của bộ định tuyến. Điều này chứa cấu trúc liên kết của 1 AS hoặc 1 khu vực (miền định tuyến)
  - Link State Request (LSR): Khi bộ định tuyến nhận DBD, nó sẽ so sánh với DBD của chính nó. Nếu DBD nhận được 1 số cập nhật nhiều hơn DBD của chính nó thì LSR sẽ được gửi đến lân cận của nó
  - Link State Update (LSU): Khi bộ định tuyến nhận được LSR, nó sẽ phản hồi bằng thông báo LSU có chứa các chi tiết được yêu cầu
  - Link State Acknowledgemet: Cung cấp độ tin cậy cho quá trình trao đổi trạng thái liên kết. Nó được gửi như là sự thừa nhận của LSU
  - Link State Advertisement (LSA): là gói dữ liệu OSPF chứa thông tin định tuyến trạng thái liên kết, chỉ được chia sẻ với các bộ định tuyến đã được hình thành <p>
**Note**: LS Advertisement và LS Acknowledgement đều là những thông điệp khác nhau
- Timer:
  -  Hello tỉmer: Khoảng thời gian mà bộ định tuyến OSPF gửi tin nhắn xin chào trên giao diện. Nó được mặc định là 10 giây
  -  Dead timer: Khoảng thời gian mà lân cận sẽ được tuyên bố là đã chết nếu không thể gửi gói xin chào. Nó là 40 giây theo mặc định. Nó thường gấp 4 lần khoảng thời gian xin chào nhưng có thể được cấu hình thủ công theo yêu cầu
- OSPF hỗ trợ/cung cấp/lợi thế:
  - Cả giao thức định tuyến IPv4 và IPv6
  - Cân bằng tải với các tuyến đường có chi phí bằng nhau cho cùng 1 điểm đến
  - VLSM và tóm tắt tuyến đường
  - Số bước nhảy không giới hạn
  - Kích hoạt cập nhật để hội tụ nhanh
  - Cấu trúc liên kết không có vòng lặp sử dụng thuật toán SPF
  - Chạy trên hầu hết các bộ định tuyến
  - Giao thức không phân loại
- Nhược điểm:
  - Đòi hỏi 1 quá trình CPU bổ sung để chạy thuật toán SPF
  - Yêu cầu nhiều RAM hơn để lưu trữ cấu trúc liên kết liền kề và phức tạp hơn để thiết lập
  - Khó khắc phục sự cố.
- Các loại mạng:
  - Point-to-Point: 2 bộ định tuyến được kết nối thông qua 1 liên kết point-to-point duy nhất. OSPF sử dụng thông báo Hello để duy trì kết nối giữa 2 bộ định tuyến
  - Boardcast: Có nhiều bộ định tuyến được kết nối với một phương tiện phát sóng duy nhất, chẳng hạn như Ethernet. OSPF sử dụng Degignated Router (DR) và Backup Designated Router (BDR) để giao tiếp với tất cả các bộ định tuyến khác trong mạng
  - Point-to-Multipoint: 1 bộ định tuyến duy nhất được kết nối với nhiều bộ định tuyến khác. OSPF sử dụng thông báo Hello để duy trì kết nối với tất cả các bộ định tuyến khác trong mạng
  - Non-Broadcast Multiple Access (NBMA): là các mạng không hỗ trợ phát sóng. OSPF có thể được sử dụng trong loại mạng này bằng cách sử dụng thông báo Hello để khám phá và duy trì kết nối với các bộ định tuyến khác trong mạng

- Cấu hình: Đòi hỏi sự hiểu biết cơ bản về các khái niệm OSPF và kiến thức về cấu trúc liên kết mạng. Các bước cơ bản để định cấu hình OSPF:
  - Xác định ID Router (RID) cho bộ định tuyến. Đây là mã định danh duy nhất cho bộ định tuyến trong mạng OSPF
  - Định cấu hình các giao diện sẽ tham gia OSPF. Điều này liên quan đến việc bật OSPF trên giao diện và xác định loại mạng
  - Tạo một quy trình OSPF và xác định khu vực mà quy trình thuộc về
  - Xác định mức độ ưu tiên của bộ định tuyến cho từng giao diện. Điều này được sử dụng để xác định bộ định tuyến nào sẽ là DR và BDR
  - Bật xác thực OSPF, nếu muốn. Điều này được sử dụng để bảo mật giao tiếp OSPF giữa các bộ định tuyến
  - Xác minh cấu hình OSPF và theo dõi trạng thái OSPF. Điều này có thể được thực hiện bằng cách sử dụng các lệnh hiển thị trong CLI của bộ định tuyến

- Điều khoản OSPF:
  - ID Router: địa chỉ loopback cao nhất được xem xét. Nếu không có loopback nào được cấu hình, thì địa chỉ IP hoạt động cao nhất trên giao diện của bộ định tuyến được xem xét
  - Ưu tiên bộ định tuyến: là giá trị 8 bit được gán cho bộ định tuyến vận hành OSPF, được sử dụng để chọn DR và BDR trong mạng broadcast
  - DR: được bầu để giảm thiểu số lượng liền kề được hình thành. DR phân phát LSA cho tất cả các bộ định tuyến khác. DR được bầu trong 1 mạng phát sóng mà tất cả các bộ định tuyến khác chia sẻ DBR của chúng. Trong boardcast, bộ định tuyến yêu cầu cập nhật lên DR và DR sẽ phản hồi yêu cầu đó bằng bản cập nhật
  - BRD: là bản sao lưu cho DR trong boardcast. Khi DR đi xuống, BDR trở thành DR và thực hiện các chức năng của nó
  - Bầu chọn DR và DBR: diễn ra trong boardcast hoặc mạng đa truy cập:
    - Bộ định tuyến có mức độ ưu tiên bộ định tuyến cao nhất sẽ được khai báo là DR
    - Nếu có sự ràng buộc trong mức độ ưu tiên của bộ định tuyến cao nhất I'd sẽ được xem xét. Đầu tiền, địa chỉ loopback cao nhất được xem xét. Nếu không có loopback nào được cấu hình, thì địa chỉ IP hoạt động cao nhất trên giao diện của bộ định tuyến được xem xét
- Các trạng thái:
  - `Down`: Không có gói Hello nào được nhận trên giao diện
    - **Note**: *Downstate* không có nghĩa là bị *down*. Điều đó có nghĩa là quá trình tiếp giáp OSPF vẫn chưa bắt đầu
  - `INIT`: Các gói Hello đã được nhận từ bộ định tuyến khác
  - `2WAY`: Ở trạng thái này, cả 2 bộ định tuyến đã nhận được các gói Hello từ các bộ định tuyến khác. Kết nối 2 chiều đã được thiết lập
    - **Note**: Ở trạng thái 2WAY và Exstart, cuộc bầu cử DR và BDR diễn ra
  - `Exstart`: NULL DBD được trao đổi và cuộc bầu cử *master* và *slave* được diễn ra. Bộ định tuyến nào có mức định tuyến cao hơn, I'd sẽ trở thành *master* trong khi bộ định tuyến kia trở thành *slave*. Cuộc bầu cử này quyết định bộ định tuyến nào sẽ gửi DBD của nó trước (các bộ định tuyến đã hình thành khu lân cận sẽ tham gia cuộc bầu cử này)
  - `Exchange`: Các DBD thực tế được trao đổi
  - `Loading`: LSR, LSU và LSA được trao đổi
    - **Important**: Khi 1 bộ định tuyến nhận DBD từ bộ định tuyến khác, nó sẽ so sánh DBD của chính nó với DBD của bộ định tuyến khác. Nếu DBD nhận được cập nhật nhiều hơn DBD của chinh nó, thì bộ định tuyến sẽ gửi LSR đến bộ định tuyến khác nêu rõ những liên kết nào là cần thiết. Bộ định tuyến khác trả lời với LSU chứa các bản cập nhật cần thiết. Đổi lại, bộ định tuyến trả lời bằng LSA.
  - `Full`: đồng bộ hoá tất cả các thông tin diễn ra. Định tuyến OSPF chỉ có thể bắt đầu trong trạng thái *Full*
 
### Border Gateway Protocol (BGP): Chức năng chính của BGP là trao đổi thông tin khả năng tiếp cận mạng với các hệ thống BGP khác. BGP xây dựng 1 biểu đồ hệ thống tự trị dựa trên thông tin trao đổi giữa các bộ định tuyến BGP
- Đặc điểm:
  - Cấu hình hệ thống liên tự trị: Cung cấp giao tiếp giữa 2 hệ thống tự trị
  - Hỗ trợ mô hình Next-Hop
  - Phối hợp nhiều loa BGP trong AS (Autonomous Systems)
  - Thông tin đường dẫn: Quảng bá BGP cũng bao gồm thông tin đường dẫn, cùng với điểm đến có thể truy cập và cặp điểm đến tiếp theo
  - Hỗ trợ chính sách: BGP có thể thực hiện các chính sách được cấu hình bởi quản trị viên
  - Chạy qua TCP
  - Bảo tồn băng thông mạng
  - Hỗ trợ CIDR
  - Hỗ trợ bảo mật
- Chức năng:
  - Thu thập và xác thực ngang hàng ban đầu, cả 2 đồng nghiệp đã thiết lập kết nối TCP và thực hiện trao đổi tin nhắn đảm bảo cả 2 bên đã đồng ý liên lạc
  - Tập trung vào việc gửi thông tin khả năng tiếp cận tiêu cực hoặc tích cực
  - Xác minh rằng các đồng nghiệp và kết nối mạng giữa chúng đang hoạt động chính xác
- Tầm quan trọng:
  - Bảo mật: Có tính bảo mật cao vì nó xác thực tin nhắn giữa các bộ định tuyến bằng cách sử dụng mật khẩu được định cấu hình sẵn thông qua đó lưu lượng truy cập trái phép được lọc ra
  - Khả năng mở rộng: Có khả năng mở rộng hơn vì nó quản lý 1 số lượng lớn các tuyến và mạng có trên internet
  - Hỗ trợ Multihoming: Một tổ chức có thể kết nối với nhiều mạng cùng 1 lúc
  - Tính toán đường dẫn tốt nhất: Các gói dữ liệu được truyền qua internet từ nguồn đến đích, mọi hệ thống ở giữa nguồn và đích phải quyết định nơi gói dữ liệu sẽ đi tiếp theo
  - Mô hình TCP/IP: dựa trên mô hình này và nó được sử dung để điều khiển lớp mạng bằng cách sử dụng giao thức lớp truyền tải
- Phân loại:
  - External BGP: Được sử dụng để trao đổi thông tin định tuyến giữa các bộ định tuyến trong hệ thống tự trị khác nhau, còn được gọi là eBGP
  ![image](https://github.com/user-attachments/assets/5b48d91a-7648-4d7e-aae4-8210af2b58ec)
  - Internal BGP: Được sử dụng để trao đổi thông tin định tuyến giữa các bộ định tuyến trong cùng 1 hệ thống tự trị, nó còn được gọi là iBGP. Bộ định tuyến nội bộ cũng đảm bảo tính nhất quán giữa các bộ định tuyến để chia sẻ thông tin định tuyến
  ![image](https://github.com/user-attachments/assets/e94d45cc-0372-47b6-b512-5de91ff2c5ab)
- Các yếu tố:
  - Weight: là thuộc tính dành riêng cho Cisco với bộ định tuyến biết đường dẫn nào được ưu tiên. Trọng lượng có giá trị cao hơn được ưu tiên
  - Originate: Cho biết cách bộ định tuyến chọn tuyến đường và thêm vào chính BGP
  - Local Preference: 1 phần tử được sử dụng để chọn đường dẫn định tuyến đi. Địa phương lớn hơn được ưu tiên
  - Autonomous System Path: Yêu cầu bộ định tuyến chọn 1 đường dẫn có độ dài ngắn hơn
  - Next Hop: Để đến đích, có phần tử hop tiếp theo chỉ định địa chỉ IP sẽ được sử dụng làm bước nhảy tiếp theo
- Chức năng quản lý thông tin tuyến BGP:
  - Lưu trữ tuyến đường: Mỗi BGP lưu trữ thông tin về cách truy cập các mạng khác
  - Cập nhật tuyến đường: Các kỹ thuật đặc biệt được sử dụng để xác định thời điểm và cách sử dụng thông tin nhận được từ các đồng nghiệp để cập nhật đúng các tuyến đường
  - Lựa chọn tuyến đường: Mỗi BGP sử dụng thông tin trong cơ sở dữ liệu tuyến đường để chọn các tuyến đường tốt đến từng mạng trên Internet
  - Quảng cáo tuyến đường: Mỗi loa BGP thường xuyên nói với đồng nghiệp của họ những gì đã biết về các mạng và phương pháp khác nhau để tiếp cận họ

- So sánh BGP và OSPF

|BGP|OSPF|
|:---|:---|
|Tuân theo Thuật toán định tuyến vector đường dẫn |Tuân theo Thuật toán định tuyến trạng thái liên kết|
|Tốc độ hội tụ rất chậm trong BGP|Tốc độ hội tụ nhanh trong OSPF|
|Giao thức định tuyến liên miền|Giao thức định tuyến nội bộ miền|
|Hoạt động định tuyến được thực hiện giữa 2 AS|Hoạt động định tuyến được thực hiện bên trong AS|
|Giao thức TCP được sử dụng|Giao thức IP được sử dụng|

