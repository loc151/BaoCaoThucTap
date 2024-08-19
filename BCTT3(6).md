# Báo cáo thực tập 3
## Networking
### Virtual LAN (VLAN): là 1 khái niệm trong đó ta có thể phân chia các thiết bị 1 cách hợp lý trên DLL. Nói chung, các thiết bị lớp 3 phân chia miền phát sóng nhưng miền phát sóng có thể được chia bằng các thiết bị chuyển mạch sử dụng VLAN
- Boardcast domain: là 1 phân đoạn mạng trong đó nếu 1 thiết bị phát 1 gói thì tất cả các thiết bị trong cùng 1 miền phát sóng sẽ nhận được nó. Các thiết bị trong cùng 1 miền phát sóng sẽ nhận được tất cả các gói phát sóng nhưng nó chỉ bị giới hạn ở các thiết bị chuyển mạch vì các bộ định tuyến không chuyển tiếp gói phát sóng. Để chuyển tiếp các gói tin đến các VLAN khác nhau hoặc các miền phát sóng, cần định tuyến giữa các VLAN. Thông qua VLAN, các mạng con kích thước nhỏ khác nhau được tạo ra tương đối dễ xử lý.
- Phạm vi VLAN:
  - VLAN 0, 4095: Những VLAN dành riêng không thể nhìn thấy hoặc sử dụng
  - VLAN 1: VLAN mặc định của các thiết bị chuyển mạch. Theo mặc định, tất cả các cổng chuyển mạch đều nằm trong VLAN. VLAN này không thể bị xoá hoặc chỉnh sửa nhưng có thể được sử dụng
  - VLAN 2-1001: Một phạm vi VLAN bình thường. Có thể tạo, chỉnh sửa và xoá các VLAN này
  - VLAN 1002-1005: Những mặc định của CISCO cho fddi và token ring. Không thể xoá các VLAN này
  - VLAN 1006-4094: Phạm vi mở rộng của VLAN
- Cấu hình:
  - Tạo VLAN bằng cách gán tên vlan-id và VLAN:
    ```
    #switch1(config)#vlan 2
    #switch1(config-vlan)#vlan accounts
    ```
  - Gán VLAN cho các cổng chuyển đổi:
    ```
    Switch(config)#int fa0/0
    Switch(config-if)#switchport mode access
    Switch(config-if)#switchport access Vlan 2
    ```
  - Ngoài ra, phạm vi cổng chuyển mạch có thể được gán cho các VLAN cần thiết
    ```
    Switch(config)#int fa0/0-2
    Switch(config-if)#switchport mode access
    Switch(config-if)#switchport access Vlan 2
    ```
- Tính năng và lợi ích:
  - Cải thiện an ninh mạng: VLAN có thể được sử dụng để tách lưu lượng mạng và giới hạn quyền truy cập vào các tài nguyên mạng cụ thể. Điều này cải thiện bảo mật bằng cách ngăn chặn truy cập trái phép vào dữ liệu nhạy cảm và tài nguyên mạng
  - Hiệu suất mạng tốt hơn: Bằng cách tách lưu lượng mạng thành các mạng logic nhỏ hơn, VLAN có thể giảm lưu lượng phát sóng và cải thiện hiệu suất mạng
  - Quản lý mạng đơn giản: VLAN cho phép quản trị viên mạng nhóm các thiết bị lại với nhau một cách hợp lý, thay vì vật lý, điều này có thể đơn giản hoá các tác vụ quản lý mạng như cấu hình, khắc phục sự cố và bảo trì
  - Linh hoạt: VLAN có thể được cấu hình động, cho phép quản trị viên mạng nhanh chóng và dễ dàng điều chỉnh cấu hình mạng khi cần thiết
  - Tiết kiếm chi phí: VLAN có thể giúp giảm chi phí phần cứng bằng cách cho phép nhiều mạng ảo chia sẻ 1 cơ sở hạ tầng mạng vật lý duy nhất
  - Khả năng mở rộng: VLAN có thể được sử dụng để phân đoạn mạng thành các nhóm nhỏ hơn, dễ quản lý hơn khi mạng phát triển về kích thước và độ phức tạp
- Tính năng chính:
  - VLAN tagging: là 1 cách để xác định và phân biệt lưu lượng VLAN với lưu lượng mạng khác. Điều này thường được thực hiện bằng cách thêm thẻ VLAN vào tiêu đề khung Ethernet
  - VLAN membership: xác định thiết bị nào được gán cho VLAN nào. Các thiết bị có thể được gán cho VLAN dựa trên cổng, địa chỉ MAC hoặc các tiêu chí khác
  - VLAN trunking: cho phép nhiều VLAN được thực hiện trên 1 liên kết vật lý duy nhất. Điều này thường được thực hiện bằng cách sử dụng 1 giao thức như IEEE 802.1Q
  - VLAN management: liên quan đến việc cấu hình và quản lý VLAN, bao gồm gán thiết bị cho VLAN, định cấu hình thẻ VLAN và định cấu hình đường VLAN
- Các loại kết nối:
  - Trunk Link: tất cả các thiết bị được kết nối với liên kết trung kế phải nhân biết VLAN. Tất cả các khung trên này phải có 1 tiêu đề đặc biệt gắn liền với nó được gọi là khung được gắn thẻ
  - Access Link: kết nối các thiết bị VLAN-unaware với cầu VLAN-aware. Tất cả các khung trên liên kết truy cập phải được bỏ gắn thẻ
  - Hybrid Link: là sự kết hợp của Trunk Link và Access Link. Cả 2 thiết bị VLAN-unaware và VLAN-aware đều được đính kèm và nó có thể có cả khung được gắn hoặc không gắn thẻ
- Lợi thế:
  - Hiệu suất: Lưu lượng mạng đầy đủ các chương trình phát sóng và đa hướng. VLAN làm giảm nhu cầu gửi lưu lượng truy cập như vậy đến các điểm đến không cần thiết
  - Hình thành các nhóm ảo: Vì có các bộ phận khác nhau trong mỗi tổ chức, VLAN có thể rất hữu ích để nhóm các thiết bị một cách hợp lý theo bộ phận của chúng
  - Bảo mật: Trong cùng 1 mạng, dữ liệu nhảy cảm có thể được phát sóng mà người ngoài có thể truy cập nhưng bằng cách tạo VLAN, chúng ta có thể kiểm soát các miền phát sóng, thiết lập tường lửa, hạn chế quyền truy cập. Ngoài ra, VLAN có thể được sử dụng để thông báo cho người quản lý mạng về sự xâm nhập. Do đó, VLAN tăng cường đáng kể an ninh mạng
  - Tính linh hoạt: VLAN cung cấp sự linh hoạt để thêm, xoá số lượng máy chủ chúng ta muốn
  - Giảm chi phí: VLAN có thể được sử dụng để tạo các miền phát sóng giúp loại bỏ sự cần thiết của các bộ định tuyến đắt tiền. Bằng cách sử dụng VLAN, số lượng miền phát sóng kích thước nhỏ có thể được tăng lên, dễ xử lý so với miền phát sóng lớn hơn
- Nhược điểm:
  - Phức tạp: VLAN có thể phức tạp để cấu hình và quản lý, đặc biệt là trong môi trường điện toán đám mây lớn hoặc động
  - Khả năng mở rộng hạn chế: VLAN bị giới hạn bởi số lượng ID VLAN có sẵn, đây có thể là 1 hạn chế trong môi trường điện toán đám mây lớn hơn
  - Bảo mật hạn chế: VLAN không cung cấp bảo mật hoàn toàn mà có thể bị xâm phạm bởi các tác nhân độc hại có thể truy cập vào mạng
  - Khả năng tương tác hạn chế: VLAN có thể không hoàn toàn tương thích với tất cả các loại thiết bị và giao thức mạng, điều này có thể hạn chế tính hữu ích của chúng trong môi trường điện toán đám mây
  - Tính di động hạn chế: VLAN có thể không hỗ trợ sự di chuyển của thiết bị hoặc người dùng giữa các phân đoạn mạng khác nhau, điều này có thể hạn chế tính hữu ích của chúng trong môi trường điện toán đám mây di động hoặc từ xa
  - Chi phí: việc triển khai và duy trì VLAN có thể tốn kém, đặc biệt nếu cần phần cứng hoặc phần mềm chuyên dụng
  - Tầm nhìn hạn chế: VLAN có thể gây khó khăn hơn cho việc giám sát và khắc phục sự cố mạng, vì lưu lượng truy cập bị cô lập trong các phân đoạn khác nhau
- Các ứng dụng thời gian thực của VLAN:
  - Voice over IP (VoIP): {VLAN có thể được sử dụng để} cách ly lưu lượng thoại khỏi lưu lượng dữ liệu, giúp cải thiện chất lượng cuộc gọi VoIP và giảm nguy cơ tắc nghẽn mạng
  - Video Conferencing: {...} ưu tiên lưu lượng video và đảm bảo rằng nó nhận được băng thông và tài nguyên cần thiết cho hội nghị truyền hình chất lượng cao
  - Remote Access: {...} cung cấp quyền truy cập từ xa an toàn vào các ứng dụng và tài nguyên dựa trên Cloud, bằng cách cách ly người dùng từ xa khỏi phần còn lại của mạng
  - Cloud Backup and Recovery: {...} cô lập lưu lượng sao lưu và phục hồi, giúp giảm nguy cơ tắc nghẽn mạng và cải thiện hiệu suất của các hoạt động sao lưu và khôi phục
  - Gaming: {...} ưu tiên lưu lượng truy cập trò chơi, đảm bảo rằng game thủ nhận được băng thông và tài nguyên họ cần để có trải nghiệm chơi game mượt mà
  - IoT: {...} cách ly các thiết bị IoT khỏi phần còn lại của mạng, giúp cải thiện bảo mật và giảm nguy cơ tắc nghẽn mạng
