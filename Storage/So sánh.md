# So sánh phương pháp lưu trữ dữ liệu:

|Đặc điểm|NAS|SAN|DAS|
|--|-----|-----|-----|
|Cấu trúc|Kết nối qua mạng|Mạng lưu trữ chuyên biệt|Kết nối trực tiếp|
|Giao thức|NFS, FTP|Fibre Channel, iSCSI, FCoE|SATA, SAS|
|Ưu điểm|Dễ cài đặt, chi phí thấp|Hiệu suất cao, độ tin cậy cao|Hiệu suất cao, chi phí thấp|
|Nhược điểm|Hiệu suất giới hạn bởi mạng|Chi phí cao, phức tạp|Khả năng mở rồng hạn chế|

---

# So sánh các interface trong ổ cứng:

|Đặc điểm|PATA|SATA|SCSI|NVMe|
|---|-----|-----|-----|-----|
|Cấu trúc|Truyền tín hiệu song song|Truyền tín hiệu nối tiếp|Truyền tín hiệu song song/nối tiếp|Giao diện PCIe|
|Tốc độ|Tối đa 133 MB/s|Tối đa 600 MB/s|Tối đa 320 MB/s|Tối đa 32 Gbps (3.9 GB/s)|
|Ứng dụng|Máy tính đời cũ|Máy tính cá nhân và máy chủ|Hệ thống máy chủ và lưu trữ doanh nghiệp|Hệ thống máy tính và máy chủ hiện đại|
|Ưu điểm|Chi phí thấp|Tốc độ nhanh hơn PATA, cáp nhỏ gọn|Độ tin cậy cao, hỗ trợ nhiều thiết bị|Tốc độ cực nhanh, độ trễ thấp, hiệu suất cao|
|Nhược điểm|Tốc độ chậm, cáp lớn|Tốc độ chậm hơn NVMe|Chi phí cao, phức tạp|Chi phí cao hơn SATA và SCSI|
