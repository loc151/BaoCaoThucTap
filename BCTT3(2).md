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
