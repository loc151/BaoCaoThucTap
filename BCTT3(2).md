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
  - Lớp vận chuyển (Transport Layer): Trao đổi xác nhận đã nhận dữ liệu và truyền lại các gói bị thiếu để đảm bảo các gói đến thứ tự và không có lỗi. Đó gọi là giao thức end-to-end. Các giao thức được sử dụng:
  - TCP: Các ứng dụng có thể tương tác với nhau bằng TCP như thể chúng được kết nối vật lý bằng 1 mạch điện. TCP truyền dữ liệu theo cách giống với truyền ký tự hơn là các gói riêng biệt. Điểm bắt đầu thiết lập kết nối, toàn bộ quá trình truyền theo thứ tự byte và điểm kết thúc đóng kết nối tạo nên quá trình truyền
  - UDP (User Datagram Protocol): Dịch vụ phân phối
    
