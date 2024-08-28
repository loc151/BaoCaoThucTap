# Hardware system
## RAID (Redundant Arrays of Independent Disks): là hình thức ghép nhiều ổ đĩa cứng vật lý thành 1 hệ thống ổ đĩa cứng có chức năng gia tăng tốc độ đọc/ghi dữ liệu chứa trên hệ thống đĩa hoặc kết hợp cả 2 yếu tố trên
### Tác dụng: 
- Dung lượng: hỗ trợ dung lượng lớn hơn so với ổ đĩa
- Khả năng chịu lỗi: Hầu hết các cấp RAID đều có 1 số mức độ dự phòng và khả năng chịu lỗi được tích hợp giúp ngăn ngừa mất dữ liệu
- Chạy liên tục: Khi các ổ cứng bị lỗi thì các hệ thống tiếp tục hoạt động bình thường
- Tốc độ: Chạy nhanh hơn so với ổ đĩa vì có thể ghi và đọc từ nhiều đĩa cùng 1 lúc
### Các loại RAID:
- RAID 0 (Striping): Ghép ít nhất 2 ổ đĩa cứng để tăng tốc độ đọc/ghi dữ liệu. Dữ liệu được chia thành nhiều phần bằng nhau và lưu trên các ổ đĩa khác nhau. Tuy nhiên, RAID 0 không có tính an toàn dữ liệu, vì nếu 1 ổ đĩa hỏng, toàn bộ dữ liệu có thể mất
- RAID 1 (Mirroring): Sử dụng ít nhất 2 ổ đĩa cứng, trong đó dữ liệu được sao lưu giữa các ổ đĩa. Nếu 1 ổ đĩa hỏng, dữ liệu vẫn an toàn trên ổ đĩa còn lại. Nhược điểm là làm giảm 1 nửa dung lượng có thể sử dụng.
- RAID 5: Kết hợp tốc độ và an toàn dữ liệu. Dữ liệu được chia thành các phần và lưu trên nhiều ổ đĩa. Một ổ đĩa dự phòng (Parity) được sử dụng để phục hồi dữ liệu khi 1 ổ đĩa hỏng. Hạn chế là nó có hiệu suất thấp hơn nên thường được dùng cho việc lưu trữ tập tin và máy chủ ứng dụng
- RAID 6: giống RAID 5, nhưng sử dụng 2 ổ đĩa dự phòng, giúp tăng tính an toàn trên ổ đĩa còn lại
- RAID 10 (1+0): Kết hợp giữa RAID 0 và 1. Ghép nhiều ổ đĩa thành các cặp mirror, sau đó ghép các cặp mirror lại với nhau. Cung cấp tốc độ và an toàn dữ liệu. Hạn chế của nó là khẳ năng sử dụng thấp và chi phí cao, khả năng mở rộng cũng bị hạn chế. RAID 10 được sử dụng nhiều trong các máy chủ cơ sở dữ liệu thực hiện nhiều thao tác ghi

### Cách triển khai:
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
