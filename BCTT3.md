# Networking
## Mô hình OSI, TCP/IP
### OSI
- Mô hình OSI (Open Systems Interconnection Reference Model) - mô hình tham chiếu kết nối các hệ thống mở,
hoặc mô hình 7 tầng của OSI. Mô hình OSI mô tả 7 tầng một hệ thống máy tính sử dụng để giao tiếp qua mạng.
- Có 2 giao thức được sử dụng trong mô hình:
  - `Giao thức hướng liên kết (Connection Oriented):` các thực thể trong cùng 1 tầng của 2 hệ thống khác nhau
cần phải thiết lập một liên kết logic chung. Chúng tiến hành trao đổi, thương lượng với nhau về tập các tham số
sẽ sử dụng trong quá trình truyền dữ liệu.
  - `Giao thức không liên kết (Connectionless):` Chỉ có giai đoạn duy nhất truyền dữ liệu và dữ liệu khi này được
truyền độc lập trên các tuyến khác nhau  
- Vai trò và chức năng của 7 tầng OSI:
1. Tầng 1 - Tầng vật lý (Physical): Đảm bảo các yêu cầu truyền nhận các chuỗi bit qua các phương tiện vật lý
2. Tầng 2 - Tầng liên kết (Data Link): Tạo/gỡ bỏ khung thông tin (Frames), kiểm soát luồng và kiếm soát lỗi
