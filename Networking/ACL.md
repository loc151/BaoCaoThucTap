# Báo cáo thực tập 3
## Networking
### Access-Lists (ACL): là 1 bộ quy tắc được xác định để kiểm soát lưu lượng mạng và giảm các cuộc tấn công mạng. ACL được sử dụng để lọc lưu lượng truy cập dựa trên bộ quy tắc được xác định cho mạng đến hoặc đi
- Tính năng:
  - Tập hợp các quy tắc được xác định khớp nối tiếp lối hành động, tức là khớp bắt đầu với dòng đầu tiên, sau đó là dòng 2, dòng 3,...
  - Các gói chỉ được khớp cho đến khi nó khớpp với các quy tắc. Khi một quy tắc được khớp thì không có so sánh nào khác diễn ra và quy tắc đó sẽ được thực hiện
  - Có 1 số sự từ chối ngầm ở cuối mỗi ACL, tức là, nếu không có điều kiện hoặc quy tắc phù hợp thì gói sẽ bị loại bỏ
- Khi danh sách truy cập được xây dựng, thì nó sẽ được áp dụng cho giao diện đến hoặc đi:
  - `Inbound access lists`: Khi 1 danh sách truy cập được áp dụng trên các gói tin đến giao diện thì trước tiên các gói sẽ được xử lý theo danh sách truy cập và sau đó được định tuyến đến giao diện gửi đi
  - `Outbound access lists`: Khi 1 danh sách truy cập được áp dụng trên cái gói tin đi của giao diện thì trước tiên gói sẽ được định tuyến và sau đó được xử lý tại giao diện gửi đi
- Các loại ACL:
  - `Standard Access-list`: Danh sách truy cập chỉ được tạo bằng địa chỉ IP nguồn. Các ACL này cho phép hoặc từ chối toàn bộ giao thức. Họ không phân biết giữa các lưu lượng IP như TCP, UDP, HTTPS, ... Bằng cách sử dụng các số 1-99 hoặc 1300-1999, bộ định tuyến sẽ hiểu nó là ACL tiêu chuẩn và địa chỉ được chỉ định làm địa chỉ IP nguồn.
  - `Extended Access-list`: Những ACL sử dụng IP nguồn, IP đích, cổng nguồn và cổng đích. Những loại ACL này cũng có thể đề cập đến lưu lượng IP nào được phép hoặc bị từ chối. Chúng sử dụng phạm vi 100-199 và 2000-2699
- Ngoài ra, có 2 loại danh sách truy cập:
  -  `Numbered access-list`: Danh sách truy cập không thể xoá cụ thể sau khi được khởi tạo, tức là nếu muốn xoá bất kỳ quy tắc nào khỏi danh sách truy cập thì điều này không được phép trong trường hợp danh sách truy cập được đánh số. Nếu cố gắng xoá 1 quy tắc khỏi danh sách thì toàn bộ danh sách truy cập sẽ bị xoá. Danh sách truy cập được đánh số có thể được sử dụng với cả danh sách truy cập tiêu chuẩn và mở rộng
  -  `Named access-list`: Trong loại này, 1 tên được gán để xác định danh sách truy cập. Nó được phép xoá 1 danh sách truy cập được đặt tên, không giống như Numbered access-list. Giống như Numbered access-list, chúng có thể được sử dụng với cả tiêu chuẩn và danh sách truy cập mở rộng 
- Quy tắc:
  - SAL thường được áp dụng gần đích 
  - EAL thường được áp dụng gần nguồn
  - Chỉ có thể gán 1 ACL cho mỗi giao diện và cho mỗi giao thức trên mỗi hướng, tức là, chỉ 1 ACL đến và đi được phép cho mỗi giao diện
  - Không thể xoá quy tắc khỏi ACL nếu đang sử dụng Numbered access-list. Nếu cố gắng xoá 1 quy tắc thì toàn bộ ACL sẽ bị xoá. Nếu đang sử dụng Named access-list thì có thể xoá 1 quy tắc cụ thể
  - Mỗi quy tắc mới được thêm vào danh sách truy cập sẽ được đặt ở cuối danh sách truy cập, do đó trước khi triển khai danh sách truy cập, hãy phân tích toàn bộ kịch bản 1 cách cẩn thận
  - Vì có 1 từ chối ngầm ở cuối mỗi ACL, nên có ít nhất 1 tuyên bố cho phép ACL nếu không tất cả lưu lượng truy cập sẽ bị từ chối
  - SAL và EAL không được có cùng tên
- Ưu điểm:
  - Cải thiện hiệu suất mạng
  - Cung cấp bảo mật vì quản trị viên có thể định cấu hình danh sách truy cập theo nhu cầu và từ chối các gói không mong muốn xâm nhập vào mạng
  - Cung cấp quyền kiểm soát lưu lượng truy cập vì nó có thể cho phép hoặc từ chối theo nhu cầu của mạng
