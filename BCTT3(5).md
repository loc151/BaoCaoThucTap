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
  - Link State Update: Khi bộ định tuyến nhận được LSR, nó sẽ phản hồi bằng thông báo LSU có chứa các chi tiết được yêu cầu
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
 
