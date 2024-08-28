# Hardware system:
## Server: là 1 máy tính được kết nối với mạng máy tính hoặc internet, có IP tĩnh, có năng lực xử lý cao. Trong server ta cài đặt các phần mềm để phục vụ cho các máy tính khác truy cập để yêu cầu cung cấp các dịch vụ và tài nguyên
### Cấu tạo:
1. Dedicated Server: (*)
- Mainboard server: main server, là mạch điện chính của 1 hệ thống thông tin. Nhiệm vụ của nó là kết nối và truyền dẫn giữa các thiết bị khác nhau trong máy chủ vật lý. Chúng bao gồm các bộ xử lý, các kênh truyền dữ liệu, khe chứa bộ nhớ, khe sockets, ...
- CPU (Central Processing Unit): là trung tâm điều hành cả hệ thống. Nó là 1 mạch tích hợp phức tạp bao gồm các transistor trên 1 bảng mạch nhỏ
- RAM: là bộ phận ảnh hưởng đến khả năng xử lý của máy chủ tại 1 thời điểm lượng dữ liệu có thể được xử lý ngay tức thời
-  HDD Server: thực hiện chức năng lưu trữ hệ điều hành, các phần mềm ứng dụng, lưu trữ dữ liệu dưới hình thức bộ nhớ ngoài và các dữ liệu khác. HDD dành cho máy chủ vật lý thường hoạt động trên chuẩn giao tiếp SCSI
-  Card RAID: là bộ phận có khả năng kết hợp các ổ cứng trong 1 máy chủ vật lý thành 1 thể thống nhất với những cơ chế chống lỗi và sao lưu giúp dữ liệu luôn được an toàn khi có các trục trặc vật lý xảy ra
-  Khe PCI (Peripheral Component Interconnect): là chuẩn giao tiếp giữa các linh kiện phần cứng máy tính với nhau. Nó quyết định tính tương thích giữa các bộ phận khác nhau của hệ thống máy tính. Có các loại khe cắm: PCI x1, x4, x8, x16 và x32. Ngoài ra còn có PCIe
2. Máy chủ ảo (VPS): là dạng máy chủ được tạo thành bằng phương pháp sử dụng công nghệ ảo hoá để chia tách từ 1 máy chủ vật lý riêng thành nhiều máy chủ ảo khác nhau. Các máy chủ ảo có tính năng tương tự như máy chủ vật lý
3. Máy chủ đám mây: là máy chủ được kết hợp từ nhiều máy chủ vật lý khác nhau với hệ thống lưu trữ SAN. Nó được dùng để phục vụ website có lượng truy cập lớn mà không hề làm mất tính ổn định
4. Máy chủ cơ sở dữ liệu (Database servers): Duy trì và chia sẻ 1 vài hình thức của dữ liệu trên một hệ thống
5. Máy chủ lưu trữ file (File servers): Chia sẻ file và folder
6. Máy chủ mail (mail servers) 
7. Máy chủ in (Print servers)
8. Máy chủ web (Web server): Nơi lưu trữ các trang web, 1 web server có thể làm nên WWW, mỗi website có thể có 1 hoặc nhiều web server
9. Game servers
10. Máy chủ ứng dụng (Application servers): Ứng dụng máy chủ trên web (chương trình máy tính chạy trên trình duyệt web) cho phép người dùng trong hệ thống sử dụng nó mà không cần phải cài đặt thêm 1 bản sao trên máy tính

## Nguyên lí hoạt động:
- Hoạt động theo mô hình client-server.
- Cung cấp các dịch vụ thiết yếu

## Vai trò:
- Cung cấp, lưu trữ và xử lý thông tin rồi chuyển đến các máy trạm liên tục 24/7 cho người dùng thông qua mạng Internet và LAN
- Có khả năng chạy liên tục trong thời gian dài và chỉ tắt khi cần được bảo trì
- Góp phần quan trọng trong việc lưu trữ và vận hành hệ thống server

## Mô hình hoạt động: 
1. Client - Server:
- Server: Có khả năng cung cấp dịch vụ và các tài nguyên đến các máy trạm khác trong cùng 1 hệ thống mạng. Server có nhiệm vụ hỗ trợ cho các hoạt động trên máy trạm client diễn ra nhanh chóng và hiệu quả hơn
- Máy trạm: Không cung cấp tài nguyên đến các thiết bị ngoại vi hay các máy tính mà chỉ sử dụng tài nguyên được cung cấp từ máy chủ
- Ưu điểm:
  - Có thể vận hành trên bất kỳ máy tính nào có hỗ trợ giao thức truyền thông
  - Mang đặc điểm của 1 phần mềm mà không hề liên quan đến phần cứng. Yêu cầu duy nhất là máy chủ phải mạnh hơn máy trạm
  - Mang lại nhiều sự tiện dụng và hỗ trợ nhiều dịch vụ đa dạng
- Nhược điểm:
  - Tính bảo mật kém
  - Luôn phải có 1 máy chủ hoạt động 24/7
  - Chi phí lắp đặt khá cao
    
2. Peer-to-Peer: Mỗi máy tính đóng vai trò vừa là máy trạm, vừa là máy chủ. Mô hình này được tạo ra khi 2 hoặc n máy tính được kết nối và chia sẻ dữ liệu với nhau mà không cần phải thông qua máy chủ riêng biệt
- Ưu điểm:
  - Tất cả các máy tính đều có khả năng lưu trữ, tính toán và đóng góp băng thông
  - Hệ thóng vẫn sẽ hoạt động tốt vì không phụ thuộc và máy chủ khi xảy ra sự cố
  - Cho phép người dùng tìm kiếm tài liệu trên máy tính người khác và ngược lại
  - Dễ cài đặt và chi phí lắp đặt thấp
- Nhược điểm:
  - Độ bảo mật và an toàn kém
  - Không cho phép lưu trữ tập trung và quản lý

3. Hybrid: được kết hợp từ 2 loại trên: trong mô hình mạng có máy chủ thì phần lớn, không phải mọi máy chủ đều hoạt động như nhau mà chúng sẽ thực hiện những nhiệm vụ chuyên biệt nhằm hỗ trợ cho các máy trạm trên mạng. 1 máy chủ vật lý sẽ thực hiện 1 nhiệm vụ riêng biệt nào đó hoặc cũng có thể thực hiện toàn bộ các nhiệm vụ này
4. 
