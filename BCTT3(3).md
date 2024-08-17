# Báo cáo thực tập 3
## Networking
### IP Address: là 1 địa chỉ duy nhất được sử dụng để nhận dạng các máy tính hoặc nút trên internet. Địa chỉ này chỉ là 1 chuỗi số được viết theo 1 định dạng nhất định. Địa chỉ IP nằm trong khoảng từ 0.0.0.0 đến 255.255.255.255

- Hoạt động của địa chỉ IP:
  - Thiết bị trực tiếp yêu cầu Nhà cung cấp dịch vụ Internet, sau đó cấp cho thiết bị đó quyền truy cập vào web
  - Địa chỉ IP được gán cho thiết bị từ phạm vi nhất định có sẵn
  - Hoạt động Internet đi qua nhà cung cấp dịch vụ và họ định tuyến lại bằng địa chỉ IP
  - Địa chỉ IP có thể thay đổi
  - Khi thay đổi môi trường, địa chỉ IP sẽ không đi cùng. Nó thay đổi khi ta thay đổi mạng của thiết bị
- Các loại địa chỉ IP:
  - IPv4: Giao thức Internet phiên bản 4. Nó bao gồm 4 số cách nhau bằng dấu chấm. Mỗi số có thể từ 0-255 ở dạng số thập phân. Nhưng máy tính sẽ chuyển đổi chúng sang hệ nhị phân (00000000-11111111). Vì mỗi số N có thể được biểu diễn bằng 1 nhóm chữ số nhị phân 8 chữ số. Vì vậy, toàn bộ địa chỉ nhị phân có thể được biểu diễn bằng 32 chữ số nhị phân. Tổng có 2^32 ~ 4 tỷ 3 thiết bị có thể được gán IPv4
  - **0.0.0.0** là địa chỉ không thể định tuyến, cho biết người dùng cuối không hợp lệ hoặc không thể áp dụng
  - **Địa chỉ loopback** là dải địa chỉ IP riêng biệt bắt đầu từ 127.0.0.0 kết thúc ở 127.255.255.255 mặc dù 127.255.255.255 là địa chỉ quảng bá cho 128.0.0.0/8. Các địa chỉ loopback được tích hợp vào hệ thống miền IP, cho phép các thiết bị truyền và nhận các gói dữ liệu. Địa chỉ loopback 127.0.0.1 thường được gọi là localhost <p>
  
**Các loại địa chỉ IPv4**
|Lớp IP|Phạm vi địa chỉ|Số lượng mạng tối đa|
|:---|:---|:---|
|A|1-126|126.(2^7-2)|
|B|128-191|16384|
|C|192-223|2097152|
|D|224-239|Dự trữ cho đa nhiệm|
|E|240-254|Dành cho nghiên cứu và phát triển|

  - IPv6: là địa chỉ IP 128 bit. Ở dạng thân thiện với con người, IPv6 được viết dưới dạng 1 nhóm gồm 8 số thập lục phân được phân tách bằng dấu `:`. Nhưng ở dạng máy tính, nó viết dưới dạng 128 bit 0 và 1. Thông qua IPv6, tổng cộng 2^128 thiết bị có thể được gán các địa chỉ duy nhất
- Phân loại địa chỉ IP:
  - Public: được cung cấp công khai và được nhà cung cấp mạng gán cho bộ định tuyến, địa chỉ này được phân chia thành 2 loại:
    - `Dynamic`: IP liên tục thay đổi mỗi khi kết nối Internet
    - `Static`: Không bao giờ thay đổi, phục vụ như 1 địa chỉ internet vĩnh viễn. Chúng được sử dụng bới các máy chủ DNS. Địa chỉ IP tĩnh cung cấp thông tin như thiết bị được đặt tại đâu và Nhà cung cấp dịch vụ Internet nào cung cấp kết nối cho thiết bị cụ thể đó. Nó cung cấp ít bảo mật hơn địa chỉ IP động vì chúng dễ theo dõi hơn.
  - Private: Địa chỉ nội bộ của thiết bị không được định tuyến tới internet và không thể trao đổi dữ liệu giữa địa chỉ riêng và internet
  - Shared: Nhiều trang web sử dụng địa chỉ IP dùng chung, nơi lưu lượng truy cập không lớn và rất dễ kiểm soát, họ quyết định cho các trang web tương tự khác thuê địa chỉ đó để tiết kiệm chi phí. 1 số công ty và máy chủ gửi email sử dụng cùng 1 địa chỉ IP (trong mail server) để cắt giảm chi phí và có thể tiết kiệm thời gian máy chủ không hoạt động
  - Delicated: được sử dụng bởi 1 công ty hoặc 1 cá nhân, mang lại cho họ những lợi ích nhất định khi sử dụng SSL riêng tư, không phải trong trường hợp địa chỉ IP dùng chung. Nó cho phép truy cập trang web hoặc đăng nhập thông qua FTP bằng địa chỉ IP thay vì tên miền. Nó làm tăng hiệu suất của trang web khi lưu lượng truy cập cao. Nó cũng bảo vệ khỏi địa chỉ IP dùng chung bị đưa vào danh sách đen do thư rác
- Các mối đe doạ:
  - Mỗi địa chỉ IP được liên kết với các cổng ảo trong máy tính, hoạt động như 1 ô cửa cho phép các ứng dụng web hoặc trang web gửi và nhận dữ liệu, thông tin trên các thiết bị. Nếu cổng vẫn được mở sau khi ngắt kết nối, tin tặc sẽ có thể xâm nhập và truy cập vào thiết bị từ xa thông qua nhiều công cụ và virus khác nhau.
  - Các hoạt động trực tuyến khác nhau có thể tiết lộ địa chỉ IP khi chơi trò chơi hoặc chấp nhận cookie xấu từ trang web bẫy hoặc diễn đàn. Họ có thể sử dụng các trang web truyền thông xã hội để theo dõi sự hiện diện trực tuyến và xác minh chéo mọi thứ họ nhận được từ các trang web này, sử dụng thông tin vì lợi ích của họ.
- Bảo vệ và ẩn địa chỉ IP:
  - Sử dụng máy chủ proxy
  - Sử dụng mạng riêng ảo (VPN) khi sử dụng Wi-Fi công cộng
  - Thay đổi cài đặt quyền riêng tư trên các ứng dụng nhắn tin tức thời
  - Tạo mật khẩu độc đáo, khó bị dò ra
  - Cảnh giác với các email lừa đảo và nội dung độc hại
  - Sử dụng 1 ứng dụng chống virus tốt và luôn cập nhật nó
  - Không nên sử dụng các trang web torrent hoặc vi phạm bản quyền
 
### Subnetting: Chia mạng lớn hơn thành các mạng nhỏ hơn để duy trì bảo mật
- Công dụng:
  - Tổ chức mạng 1 cách hiệu quả, giúp mở rộng công nghệ cho các công ty vừa và lớn
  - Được sử dụng cho các cấu trúc nhân sự cụ thể để giảm lưu lượng truy cập và duy trì trật tự, hiệu quả
  - Mạng con phân chia các miền của chương trình để lưu lượng truy cập được định tuyến hiệu quả, giúp cải thiện hiệu suất mạng
  - Được sử dụng để tăng cường an ninh mạng
- Mạng có thể được chia thành 2 phần: Để chia mạng thành 2 phần, cần chọn 1 bit cho mỗi Mạng con từ phần ID server
- Cách hoạt động: Chia các mạng con thành các mạng con nhỏ hơn. Để giao tiếp giữa các mạng con cần sử dụng bộ định tuyến. Mỗi mạng con cho phép các thiết bị được liên kết giao tiếp với nhau. Mạng con cho 1 mạng nên được thực hiện theo cách mà nó không ảnh hưởng đến các bit mạng
- Ưu điểm: Cung cấp bảo mật cho 1 mạng từ 1 mạng khác
