# Hardware System
## 1. Ổ cứng HDD:
- HDD (Hard Disk Drive) là 1 ổ đĩa lưu trữ dữ liệu bên trong máy tính.
- Nó có các đĩa quay bên trong và dữ liệu được lưu trữ từ tính.
- Ổ HDD có 1 đầu dò, dùng để ghi và đọc dữ liệu từ mặt đĩa phủ vật liệu từ tính.
- Nó hoạt động tương tự như đầu ghi đĩa CD.
- Đầu dò di chuyển giữa các vị trí khác nhau trên bề mặt đĩa để truy xuất dữ liệu khác nhau
### 1.1. Các loại ổ cứng HDD:
- HDD 2.5 inch: thường thấy trên laptop
- HDD 3.5 inch: thường thấy trên máy tính để bàn

### 1.2. Ưu điểm:
- **Dung lượng lớn:** Có thể lưu trữ 1 lượng lớn dữ liệu với chi phí thấp
- **Giá thành rẻ:** Thường rẻ hơn so với các loại ổ cứng khác

### 1.3. Nhược điểm:
- **Tốc độ chậm hơn:** Tốc độ truy xuất dữ liệu thấp hơn so với SSD
- **Tiêu thụ điện năng cao hơn:** Sử dụng nhiều điện năng hơn và có thể phát ra tiếng ồn khi hoạt động

## 2. Ổ cứng SSD:
- SSD (Solid State Drive) là loại ổ cứng thể rắn sử dụng bộ nhớ lưu trữ flash.
- Tất cả dữ liệu được lưu trữ trong các mạch tích hợp.
### 2.1. Các loại ổ cứng SSD:
- SSD 2.5 inch SATA: Phổ biến nhất, dễ dàng nâng cấp cho laptop và PC
- SSD mSATA: Kích thước nhỏ, phù hợp cho các dòng laptop mỏng nhẹ
- SSD M.2 SATA: Phiên bản nâng cấp của SSD SATA, phù hợp với laptop mỏng nhẹ
- SSD M.2 PCIe: Tốc độ cao, chỉ hỗ trợ trên các dòng laptop cao cấp
### 2.2. Ưu điểm:
- Tốc độ truy xuất dữ liệu nhanh: Giúp tăng tốc độ khởi động hệ thống và load ứng dụng
- Độ bền cao: Không có bộ phận cơ học nên ít bị hỏng hóc do va đập
- Tiêu thụ điện năng thấp: Tiết kiệm năng lượng hơn so với HDD
- Hoạt động yên lặng: Không tạo ra tiếng ồn khi hoạt động

### 2.3. Nhược điểm:
- Giá thành cao: Thường đắt hơn HDD khi so cùng 1 dung lượng
- Dung lượng lưu trữ hạn chế: so với HDD, SDD có dung lượng thấp hơn với cùng mức giá

## 3. Ổ cứng NVME:
- NVMe (Non-Volatile Memory Express) là 1 loại ổ đĩa rắn (SSD) sử dụng giao diện NVMe để kết nối với máy tính.
- Là công nghệ mới so với giao diện truyền thống SATA, cung cấp hiệu suất cao hơn và thời gian đáp ứng nhanh hơn
### 3.1. Các loại ổ cứng:
- NVMe PCIe 3.0: Phổ biến và có giá thành hợp lý, phù hợp với nhiều loại máy tính
- NVMe PCIe 4.0: Cung cấp tốc độ truyền dữ liệu cao hơn, phù hợp với các hệ thống yêu cầu hiệu suất cao

### 3.2. Ưu điểm:
- Tốc độ truyền dữ liệu cao: NVMe tận dụng băng thông cao của PCIe, cho phép truyền dữ liệu nhanh hơn nhiều so với SATA. Tốc độ truyền dữ liệu của NVMe có thể lên đến 32000 MB/s, trong khi SATA III chỉ đạt tối đa 600 MB/s
- Độ trễ thấp: NVMe được thiết kế để giảm độ trễ, giúp tăng tốc độ truy xuất dữ liệu và cải thiện hiệu xuất tổng thể của hệ thống
- Hỗ trợ nhiều hàng đợi I/O: NVMe có thể hỗ trợ 64K hàng đợi I/O, mỗi hàng đợi có thể chứa 64K lệnh, giúp tăng khả năng xử lý nhiều tác vụ đồng thời.

## 4. So sánh giữa ổ cứng lưu trữ NVMe, SSD và HDD:
- So với NVMe và SSD, HDD là 1 dạng công nghệ ổ cứng sử dụng cách thức lưu trữ hoàn toàn khác và có thể coi là lỗi thời. Bằng việc đọc ghi dữ liệu từ 1 mặt đĩa phủ từ tính, HDD có độ an toàn dữ liệu, tốc độ truy cập, kích thước đều bị giới hạn bởi chất lượng vật liệu từ tính và vòng quay ổ đĩa. Khi muốn phát triển 1 HDD nhanh hơn, ta phải đánh đổi tuổi thọ ổ cứng vì phải tăng tốc độ vòng quay. Kích thước và trọng lượng của HDD gần như không thay đổi kể từ khi nó ra đời.
- SSD và NVMe là 1 loại ổ cứng thể rắn, việc đọc ghi dữ liệu thông qua mạch điện tử
- Sự khác biệt lớn nhất giữa NVMe và SSD là giao diện truyền dữ liệu giữa ổ cứng và bo mạch chủ. "e" trong NVMe là Express, 1 cách thức truyền dữ liệu qua làn PCIe trực tiếp tới CPU. Được thiết kế nâng cao tính song song và độ trễ thấp.
- Lưu trữ SSD: lưu trữ trạng thái rắn được kết nối với máy chủ thông qua giao diện SATA.
- Lưu trữ NVMe: lưu trữ trạng thái rắn được kết nối với máy chủ thông qua giao diện Express thế hệ tiếp theo, nhanh hơn, đáng tin cậy hơn

## 5. Lợi ích của công nghệ NVMe:
### 5.1. Các Input/Output Per Second (IOPS):
- Với bus PCIe thế hệ tiếp theo, ổ NVMe cung cấp tốc độ đọc ghi cao hơn nhiều so với chuẩn giao diện SATA được sử dụng trong các loại ổ cứng thế hệ đầu.
- Các giao diện SATA III cung cấp băng thông 6Gbps trong khi theo lý thuyết PCIe cung cấp băng thông tối đa là 32 Gbps (thậm chí là 256 Gbps) với giao diện PCIe mới nhất.
- Hiện tại không có SSD nào có thể đạt tới tốc độ này, tuy nhiên đây là điều kiện lý tưởng để phát triển và mở rộng
- 1 ổ SSD tốt, nếu được kết nối với giao diện SAS hoặc SATA, có thể đọc/ghi khoảng 550 MB/s dữ liệu và có thể xử lý tới 10000 I/O mỗi giây
- Nhưng 1 ổ NVMe tốt có thể đọc/ghi khoảng 3000-3200 MB/s dữ liệu và xử lý lên đến 640000 I/O mỗi giây
- NVMe mang lại tốc độ truyền dữ liệu nhanh hơn đến 6 lần với hiệu suất IOPS tốt hơn tới 60 lần so với SSD

### 5.2. Khả năng cung cấp hàng đợi dài hơn:
- Khả năng cung cấp hàng đợi của SSD sử dụng giao diện SATA là 32 lệnh, công nghệ SAS có thể cung cấp đến 256 lệnh hàng đợi.
- Với công nghệ ổ cứng NVMe khi sử dụng toàn bộ 12 làn PCIe, nó có khả năng cung cấp 64000 lệnh hàng đợi khổng lồ

### 5.3. Công nghệ có thể mở rộng:
- NVMe sử dụng PCIe chứ không phải Controller Interface nên nó có thể mở rộng
- Hiện tại NVMe chỉ sử dụng 4 trên tổng số 16 làn PCIe. Do đó không gian để mở rộng về mặt tốc độ đọc ghi của ổ cứng sẽ còn rất nhiều

### 5.4. Công nghệ thân thiện hơn với môi trường:
- Chế độ chờ của NVMe được coi là "xanh" với môi trường hơn tất cả những loại ổ cứng khác
- Chế độ chờ NVMe giảm mức tiêu thụ điện xuống 97%

### 5.5. Giảm hiện tượng "Bottleneck":
- Khi sử dụng các loại ổ cứng truyền thống với mức đọc ghi và hàng chờ lệnh bị giới hạn như ổ cứng SSD, HDD sử dụng cổng SATA, khả năng bị tắc nghẽn có thể xảy ra trong trường hợp:
  - Có quá nhiều lượt truy cập, cần truy xuất dữ liệu cùng lúc
  - Có quá nhiều lệnh chờ trích xuất dữ liệu cần cho CPU xử lý của phần mềm
- Điều này chạm đến ngưỡng giới hạn của CPU và sẽ gây ra hiện tượng chậm phản hồi (not responding thường thấy trên HĐH Windows)
- Máy tính sử dụng NVMe có khả năng xử lý vấn đề này tốt hơn vì nó cung cấp hàng đợi dài hơn và tốc độ đọc/ghi cao hơn

## 6. VPS NVMe: Sử dụng loại ổ cứng NVMe cho mục đích lưu trữ và cài đặt hệ điều hành, phần mềm trên đó. Tốc độ VPS NVME là không thể bàn cãi và so sánh ở thời điểm hiện tại.
