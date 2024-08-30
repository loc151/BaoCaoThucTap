# Kỹ thuật bấm dây mạng 
## Dụng cụ:
- Dây mạng
- Hạt mạng, đầu RJ 45
- Kìm bấm mạng
## Các loại dây cáp mạng
- `Cat 5`: là loại cáp cơ bản nhất với 2 dạng chính là lõi đặc và lõi bện. Nó được chia thành 2 loại là không bọc giáp (UTP) và bọc giáp (FTP), có băng thông đạt mức 100 MHz và tốc độ truyền tải 10/100 Mbps. Lõi đặc thường được sử dụng khi truyền dữ liệu ở khoảng cách xa, trong khi lõi bện thường được dùng làm cáp đầu nối
- `Cat 5E`: nâng cấp của **Cat 5**, được sản xuất với 3 loại tiêu chuẩn: UDP, FTP và SFTP. Cat 5E có phần lõi được làm từ kim loại (đồng) hoặc hợp kim lõi đặc, được bao bọc bởi lớp nhựa và vỏ bọc thường làm bằng nhựa PVC. Nó có khả năng hỗ trợ Ethernet Gigabit tốc độ cao lên đến 1Gb/s
- `Cat 6`: Tốc độ hoạt động của cáp mạng Cat 6 lên tới 10 Gbps ở băng thông 250 MHz với khoảng cách truyền dẫn từ 70-100m
|Tiêu chí|Cat5E|Cat6|Cat7|Cat8|
|:---|:---|:---|:---|:---|
|Tần số hoạt động|100 MHz|250 MHz|600 MHz|2000 MHz|
|Ứng dụng|10/100 Mbps Ethernet và Gigabit Ethernet|Gigabit Ethernet|Gigabit Ethernet|Gigabit Ethernet|
|Tốc độ truyền tải|10/100/1000 Mbps|10/100/1000 Mbps|10 GBps|25-40 GBps|
|Chất lượng đường truyền|Ít bị nhiễu chéo|Chống nhiễu chéo|Chống nhiễu chéo|Chống nhiễu chéo|
|Khoảng cách hoạt động|100m, 150m|70-90m, 150m|100m|30m|
## Các loại chuẩn trong dây mạng
- `Chuẩn A (T568A)`: được thiết kế để tương thích với các dây cũ hơn
  - Cách đấu dây: Trắng xanh lá - Xanh lá - Trắng cam - Xanh dương - Trắng xanh dương - Cam - Trắng nâu - Nâu
- `Chuẩn B`: được thiết kế để cách ly tín hiệu tốt hơn và bảo vệ khỏi nhiễu cho các hệ thống và sản phẩm mạng mới hơn 
  - Cách đấu dây: Trắng cam - Cam - Trắng xanh lá - Xanh dương - Trắng xanh dương - Xanh lá - Trắng nâu - Nâu
- Chuẩn thẳng: 2 đầu đấu theo chuẩn A hoặc chuẩn B), để nối 2 thiết bị khác loại với nhau (máy tính, switch, router
- Chuẩn chéo: 1 đầu chuẩn A, 1 đầu chuẩn B hoặc ngược lại, dùng để kết nối 2 thiết bị cùng loại với nhau
![image](https://github.com/user-attachments/assets/649c7a2e-49db-460a-9c7f-26cb79735b37)

## Các bước bấm dây mạng
- Bước 1: Cắt 1 đoạn dây mạng, dùng kìm bấm mạng cắt 1 đoạn vỏ bên ngoài, khoảng 2-3 cm, để các lõi dây mạng xuất hiện
- Bước 2: Miết các dây cho đều nhau, thẳng. Dùng kìm bấm mạng cắt hết đoạn đầu lõi dây lồi lõm, lấy đầu mạng và tra vào phần lõi sau khi cắt thẳng
- Bước 3: Dùng kìm bấm mạng kẹp lấy phần đầu nhựa của hạt mạng, bấm chặt tay
