# Tổng quan về DAS
## 1. Khái niệm:
- DAS (Direct Attached Storage) là một phương pháp lưu trữ dữ liệu trong đó các thiết bị lưu trữ như ổ cứng (HDD) hoặc ổ thể rắn (SSD) được kết nối trực tiếp với máy tính hoặc máy chủ thông qua các cổng kết nối như SATA, SAS, hoặc NVMe.
- DAS không yêu cầu một mạng riêng biệt để truyền dữ liệu
---
## 2. Các thành phần chính: 
- Máy tính hoặc máy chủ: Đây là thiết bị chính, nơi dữ liệu được tạo ra, xử lý và truy xuất.
- Thiết bị lưu trữ: Có thể là ổ cứng (HDD), ổ thể rắn (SSD) hoặc một tập hợp các ổ đĩa được cấu hình theo các chế độ như RAID hoặc JBOD.
- Bộ điều khiển RAID: Một thiết bị phần cứng hoặc phần mềm chịu trách nhiệm quản lý và điều phối hoạt động của các ổ đĩa trong cấu hình RAID, đảm bảo tính toàn vẹn và hiệu suất của dữ liệu.
- Cáp kết nối: Các loại cáp như SATA, SAS hoặc USB được sử dụng để kết nối thiết bị lưu trữ với máy tính hoặc máy chủ.
---
## 3. Các loại DAS:
- DAS sử dụng ổ cứng (HDD): Đây là loại DAS phổ biến và rẻ tiền nhất, sử dụng các ổ đĩa cứng truyền thống để lưu trữ dữ liệu. Ưu điểm của DAS HDD là dung lượng lớn và chi phí thấp, tuy nhiên tốc độ truy xuất và độ tin cậy kém hơn so với các loại ổ đĩa khác.
- DAS sử dụng ổ thể rắn (SSD): DAS SSD sử dụng các ổ đĩa thể rắn để lưu trữ dữ liệu, mang lại tốc độ đọc/ghi cao, độ trễ thấp và khả năng chịu lỗi tốt hơn so với HDD. Tuy nhiên, chi phí của DAS SSD cũng cao hơn đáng kể.
- DAS lai (Hybrid) kết hợp HDD và SSD: Loại DAS này kết hợp cả ổ cứng và ổ thể rắn trong cùng một hệ thống, trong đó SSD đóng vai trò là bộ nhớ đệm để tăng tốc độ truy xuất dữ liệu thường xuyên sử dụng, trong khi HDD đảm nhận vai trò lưu trữ dữ liệu dung lượng lớn. DAS lai cung cấp một sự cân bằng tốt giữa hiệu suất và chi phí.
---
## 4. Hướng dẫn cài đặt và sử dụng DAS
### Kết nối DAS với máy tính hoặc máy chủ
- Đảm bảo DAS và máy tính/máy chủ đều đã được tắt nguồn.
- Kết nối cáp từ cổng tương ứng (SATA, SAS, USB, Thunderbolt) của DAS với máy tính/máy chủ.
- Bật nguồn cho DAS và máy tính/máy chủ.
- Hệ điều hành sẽ tự động nhận diện DAS như một ổ đĩa mới.
### Định dạng và phân vùng DAS (nếu cần)
- Mở công cụ quản lý đĩa (Disk Management) trên Windows hoặc Disk Utility trên macOS.
- Chọn ổ đĩa DAS và thực hiện định dạng (format) với hệ thống tập tin phù hợp (NTFS, exFAT, HFS+, vv.).
- Nếu cần, chia ổ đĩa thành nhiều phân vùng (partition) để quản lý dữ liệu hiệu quả hơn.
### Cài đặt phần mềm quản lý DAS (nếu có)
- Một số DAS đi kèm với phần mềm quản lý riêng, giúp giám sát tình trạng phần cứng, cấu hình RAID, hoặc sao lưu dữ liệu.
- Tải và cài đặt phần mềm quản lý từ trang web của nhà sản xuất DAS.
- Thực hiện các thiết lập ban đầu như tạo tài khoản người dùng, cấu hình cảnh báo, lên lịch sao lưu, vv.
### Tổ chức và quản lý dữ liệu trên DAS
- Tạo các thư mục (folder) để phân loại và lưu trữ dữ liệu một cách có hệ thống, tránh lưu trữ tất cả trong một thư mục gốc.
- Đặt tên tập tin và thư mục rõ ràng, ngắn gọn, bao gồm ngày tháng để dễ dàng tìm kiếm và sắp xếp.
- Thực hiện sao lưu (backup) định kỳ dữ liệu quan trọng sang một thiết bị lưu trữ khác hoặc dịch vụ lưu trữ đám mây để tránh mất mát do hỏng hóc phần cứng.
---
## 5. Tối ưu hóa hiệu suất và bảo vệ dữ liệu trên DAS
### Cấu hình RAID để tăng tốc độ và độ tin cậy (RAID)
- Sử dụng các cấp RAID 0 (striping) để tăng tốc độ đọc/ghi, hoặc RAID 1 (mirroring), RAID 5, RAID 6 để tăng độ an toàn dữ liệu.
- Lựa chọn cấu hình RAID phù hợp dựa trên nhu cầu về hiệu suất, dung lượng, và mức độ bảo vệ dữ liệu.
- Sử dụng bộ điều khiển RAID phần cứng (hardware RAID controller) để giảm tải cho CPU và đạt hiệu suất cao hơn so với RAID phần mềm.
### Sử dụng phần mềm sao lưu để bảo vệ dữ liệu
- Chọn phần mềm sao lưu tin cậy và dễ sử dụng, tương thích với hệ điều hành và DAS đang dùng.
- Thiết lập lịch sao lưu tự động (incremental hoặc differential backup) để đảm bảo dữ liệu luôn được cập nhật mới nhất.
- Thử nghiệm khôi phục (restore) dữ liệu định kỳ để đảm bảo tính toàn vẹn của bản sao lưu.
### Giám sát tình trạng hoạt động của DAS
- Sử dụng phần mềm giám sát để theo dõi các thông số như nhiệt độ, tình trạng ổ đĩa, lỗi đọc/ghi, vv.
- Thiết lập cảnh báo qua email hoặc SMS khi có dấu hiệu bất thường hoặc lỗi xảy ra.
- Thực hiện bảo trì phần cứng định kỳ như vệ sinh, kiểm tra kết nối cáp, thay thế ổ đĩa hỏng.
