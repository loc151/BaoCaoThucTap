# Hardware system
## 1. RAID (Redundant Arrays of Independent Disks): là hình thức ghép nhiều ổ đĩa cứng vật lý thành 1 hệ thống ổ đĩa cứng có chức năng gia tăng tốc độ đọc/ghi dữ liệu chứa trên hệ thống đĩa hoặc kết hợp cả 2 yếu tố trên
- Cách thức hoạt động của RAID: sao chép dữ liệu lên 2 hoặc nhiều ổ cứng vật lý được liên kết với nhau bằng 1 RAID **Controller**. **RAID Controller** có thể dựa trên nền tảng phần cứng hoặc phần mềm
- Hầu hết các loại RAID khác nhau đều sử dụng kỹ thuật hạn chế lỗi gọi là dữ liệu *chẵn lẻ* (parity) để cung cấp khả năng chịu lỗi (fault tolerance) khi dữ liệu được nhân đôi. Nhờ đó có thể giảm tác động của việc mất dữ liệu khi gặp phải lỗi phần cứng.
## 2. Tác dụng: 
- Dung lượng: hỗ trợ dung lượng lớn hơn so với ổ đĩa
- Khả năng chịu lỗi: Hầu hết các cấp RAID đều có 1 số mức độ dự phòng và khả năng chịu lỗi được tích hợp giúp ngăn ngừa mất dữ liệu
- Chạy liên tục: Khi các ổ cứng bị lỗi thì các hệ thống tiếp tục hoạt động bình thường
- Tăng hiệu suất: Chạy nhanh hơn so với ổ đĩa vì có thể ghi và đọc từ nhiều đĩa cùng 1 lúc
## 3. Các loại RAID:
- RAID 0 (Striping): Ghép ít nhất 2 ổ đĩa cứng để tăng tốc độ đọc/ghi dữ liệu. Dữ liệu được chia thành nhiều phần bằng nhau và lưu trên các ổ đĩa khác nhau. Tuy nhiên, RAID 0 không có tính an toàn dữ liệu, vì nếu 1 ổ đĩa hỏng, toàn bộ dữ liệu có thể mất
- RAID 1 (Mirroring): Sử dụng ít nhất 2 ổ đĩa cứng, trong đó dữ liệu được sao lưu giữa các ổ đĩa. Nếu 1 ổ đĩa hỏng, dữ liệu vẫn an toàn trên ổ đĩa còn lại. Nhược điểm là làm giảm 1 nửa dung lượng có thể sử dụng.
- RAID 5: Kết hợp tốc độ và an toàn dữ liệu. Dữ liệu được chia thành các phần và lưu trên nhiều ổ đĩa. Một ổ đĩa dự phòng (Parity) được sử dụng để phục hồi dữ liệu khi 1 ổ đĩa hỏng. Hạn chế là nó có hiệu suất thấp hơn nên thường được dùng cho việc lưu trữ tập tin và máy chủ ứng dụng
- RAID 6: giống RAID 5, nhưng sử dụng 2 ổ đĩa dự phòng, giúp tăng tính an toàn trên ổ đĩa còn lại
- RAID 10 (1+0): Kết hợp giữa RAID 0 và 1. Ghép nhiều ổ đĩa thành các cặp mirror, sau đó ghép các cặp mirror lại với nhau. Cung cấp tốc độ và an toàn dữ liệu. Hạn chế của nó là khẳ năng sử dụng thấp và chi phí cao, khả năng mở rộng cũng bị hạn chế. RAID 10 được sử dụng nhiều trong các máy chủ cơ sở dữ liệu thực hiện nhiều thao tác ghi

## 4. Cách triển khai:
- RAID phần cứng:
  - Sử dụng bộ điều khiển phần cứng chuyên dụng mà các đĩa được liên kết
  - Bộ xử lý trên bo mạch quản lý RAID giúp giảm tải công việc từ bộ xử lý máy chủ, giúp đọc và ghi dữ liệu nhanh hơn
  - Bộ điều khiển phần cứng cung cấp thêm bộ pin dự phòng bảo vệ dữ liệu trong trường hợp mất điện của máy chủ
  - Thay thế đĩa khá dễ dàng
  - `Nhược điểm`: Phần cứng khá đắt. Nếu bộ điều khiển bị lỗi, cần 1 bộ tương thích để thay thế nó.
- RAID phần mềm:
  - Được cài đặt trong hệ điều hành và khá dễ thực hiện
  - Không cần thêm phần cứng và phần trung gian
  - Hiệu quả hơn về mặt chi phí
  - Mảng có thể cấu hình lại vì không bị hạn chế bới bộ điều khiển RAID phần cứng
  - `Nhược điểm`: chậm hơn RAID phần cứng. Thay thế đĩa khá phức tạp
## 5. Ứng dụng trong kiến trúc máy tính:
- **Hệ thống máy chủ và dịch vụ trực tuyến:** RAID 1 & 10 thường được sử dụng để đảm bảo khả năng dự phòng và tốc độ truy cập cao cho các dịch vụ web, email và cơ sở dữ liệu
- **Trung tâm dữ liệu và lưu trữ lớn:** RAID 5 & 6 thường được sử dụng để lưu trữ dữ liệu lớn, cung cấp hiệu suất và dự phòng
- **Máy tính cá nhân và trò chơi:** RAID 0 thường được sử dụng để tăng hiệu suất trong máy tính cá nhân và máy chơi game
- **Thiết kế đồ hoạ và biên tập video:** RAID 0 & 10 có thể cải thiện hiệu suất trong việc xử lý tệp hình ảnh và video lớn
- **Máy chủ lưu trữ gia đình:** RAID 1 & 5 có thể được sử dụng để bảo vệ dữ liệu

## 6. Ưu điểm và nhược điểm: 
### 6.1. Ưu điểm:
- **Tăng độ tin cậy của dữ liệu:** RAID cung cấp tính dự phòng, nghĩa là nếu 1 đĩa bị lỗi, dữ liệu có thể được phục hồi từ các đĩa còn lại trong mảng
- **Cải thiện hiệu suất:** RAID có thể cải thiện hiệu suất bằng cách trải rộng dữ liệu trên nhiều đĩa, cho phép nhiều thao tác đọc/ghi cùng xảy ra, tăng tốc độ truy cập dữ liệu
- **Khả năng mở rộng:** RAID có khả năng mở rộng bằng cách thêm nhiều đĩa vào mảng, tăng dung lượng lưu trữ mà không cần thay thế toàn bộ hệ thống lưu trữ
- **Tiết kiệm chi phí:** 1 số cấu hình RAID như RAID 0 có thể được triển khai bằng phần cứng giá rẻ, làm cho RAID trở thành giải pháp tiết kiệm chi phí cho các doanh nghiệp nhỏ hoặc hộ gia đình

### 6.2. Nhược điểm:
- **Chi phí:** RAID 5 & 6 có thể tốn kém do yêu cầu phần cứng hoặc phần mềm bổ sung
- **Hạn chế về hiệu suất:** RAID 1 & 5 có thể có những hạn chế về hiệu suất. RAID 1 chỉ có thể đọc dữ liệu nhanh bằng 1 ổ đĩa đơn, RAID 5 có thể có tốc độ ghi chậm hơn do yêu cầu tính toán chẵn lẻ
- **Độ phức tạp:** Việc thiết lập và bảo trì RAID có thể phức tạp, đặc biệt đối với các cấu hình nâng cao như RAID 5 hoặc 6
- **Tăng nguy cơ mất dữ liệu:** Mặc dù RAID cung cấp khả năng dự phòng, nó không thể thay thế cho các bản sao lưu thích hợp. Nếu nhiều ổ đĩa bị lỗi đồng thời, việc mất dữ liệu vẫn có thể xảy ra

## 7. Chi tiết các RAID:
### 7.1. RAID 0:
- Cơ chế hoạt động: Dữ liệu được chia nhỏ và ghi lên tất cả các ổ đĩa trong RAID, không có dự phòng
- Hiệu năng đọc: Rất tốt, vì có thể đọc từ nhiều ổ đĩa cùng lúc
- Hiệu năng ghi: Tương tự hiệu năng đọc
- Tỉ lệ sử dụng dung lượng: 100% (Tất cả dung lượng được sử dụng cho dữ liệu)
- Khả năng chịu lỗi: Không có. Mất 1 ổ đĩa sẽ mất tất cả dữ liệu
- Số lượng ổ đĩa tối thiểu: 2
- Ứng dụng phổ biến: Các ứng dụng yêu cầu hiệu năng cao, nhưng không quan trọng về an toàn dữ liệu

### 7.2. RAID 1:
- Cơ chế hoạt động: Dữ liệu được sao chép đồng thời trên 2 ổ đĩa (mirroring)
- Hiệu năng đọc: Khá tốt, có thể đọc từ 2 ổ đĩa song song.
- Hiệu năng ghi: Chậm hơn RAID 0, vì dữ liệu phải được ghi lên cả 2 ổ đĩa
- Tỉ lệ sử dụng dung lượng: 50% (1 nửa dung lượng được sử dụng cho dữ liệu, còn lại để dự phòng)
- Khả năng chịu lỗi: Cao. Mất 1 ổ đĩa không mất tất cả dữ liệu
- Số lượng ổ đĩa tối thiểu: 2
- Ứng dụng phổ biến: Lưu trữ hệ điều hành, dữ liệu quan trọng yêu cầu an toàn cao

### 7.3. RAID 5:
- Cơ chế hoạt động: Dữ liệu và thông tin dự phòng (parity) được phân bổ đồng đều trên tất cả các ổ đĩa
- Hiệu năng đọc: Khá tốt, có thể đọc từ nhiều ổ đĩa cùng lúc
- Hiệu năng ghi: Trung bình, vì phải tính toán và ghi thông tin parity
- Tỉ lệ sử dụng dung lượng: (n-1)/n, n là số lượng ổ đĩa
- Khả năng chịu lỗi: Chịu được mất 1 ổ đĩa
- Số lượng ổ đĩa tối thiểu: 3
- Ứng dụng phổ biến: Lưu trữ dữ liệu, môi trường máy chủ đòi hỏi dung lượng lớn và an toàn dữ liệu

### 7.4. RAID 6:
- Cơ chế hoạt động: Tương tự RAID 5, nhưng sử dụng 2 bộ parity độc lập
- Hiệu năng đọc: Tốt, tương tự RAID 5
- Hiệu năng ghi: Trung bình, vì phải tính toán và ghi thông tin parity
- Tỉ lệ sử dụng dung lượng: (n-2)/n
- Khả năng chịu lỗi: Chịu được mất 2 ổ đĩa
- Số lượng ổ đĩa tối thiểu: 4
- Ứng dụng phổ biến: Lưu trữ dữ liệu quan trọng với yêu cầu chịu lỗi cao

### 7.5. RAID 10 (1+0):
- Cơ chế hoạt động: Kết hợp giữa mirroring (RAID 1) và striping (RAID 0).
- Hiệu năng đọc: Rất tốt, tương tự RAID 0.
- Hiệu năng ghi: Tốt, chậm hơn RAID 0 nhưng tốt hơn RAID 5.
- Tỷ lệ sử dụng dung lượng: 50% (Giống RAID 1).
- Khả năng chịu lỗi: Cao. Mất một ổ đĩa trong một cặp mirror không gây mất dữ liệu.
- Số lượng ổ đĩa tối thiểu: 4.
- Ứng dụng phổ biến: Các ứng dụng đòi hỏi cả hiệu năng cao và an toàn dữ liệu, ví dụ: cơ sở dữ liệu, máy chủ ảo.
