# Networking
## Mô hình OSI, TCP/IP
### OSI
- Mô hình OSI (Open Systems Interconnection Reference Model) - mô hình tham chiếu kết nối các hệ thống mở,
hoặc mô hình 7 tầng của OSI. Mô hình OSI mô tả 7 tầng một hệ thống máy tính sử dụng để giao tiếp qua mạng. <p>
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
- Lớp vật lý: là lớp thấp nhất của mô hình tham chiếu OSI. Nó chịu trách nhiệm về kết nối vật lý thực tế giữa các thiết bị. Lớp vật lý chưa thông tin dưới dạng bit. Nó chịu trách nhiệm truyền các bit riêng lẻ từ nút này sang nút tiếp theo. Khi nhận dữ liệu, lớp này sẽ nhận được tín hiệu và chuyển đổi nó thành 0s & 1s và gửi chúng đến lớp Data Link, lớp này sẽ đặt khung trở lại với nhau.
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
