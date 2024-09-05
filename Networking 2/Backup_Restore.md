# Backup và Restore cấu hình
## **1.1. Khái Niệm Backup và Restore**
- **Backup cấu hình:** Là quá trình sao lưu lại file cấu hình hiện tại của thiết bị mạng (switch Cisco) để có thể khôi phục lại khi cần thiết.
- **Restore cấu hình:** Là quá trình khôi phục lại file cấu hình đã sao lưu trước đó lên thiết bị mạng để đảm bảo thiết bị hoạt động đúng như cấu hình đã định sẵn.
  
## **1.2. Tại Sao Cần Backup/Restore Cấu Hình?**
- **Phòng tránh sự cố:** Trong trường hợp switch gặp sự cố hoặc bị cấu hình sai, việc khôi phục cấu hình từ file sao lưu giúp giảm thiểu thời gian ngừng hoạt động của hệ thống.
- **Thử nghiệm và cấu hình mới:** Sau khi thử nghiệm hoặc cập nhật cấu hình mới, bạn có thể khôi phục lại cấu hình cũ nếu có vấn đề xảy ra.
- **Bảo mật và tuân thủ quy định:** Sao lưu cấu hình giúp tuân thủ quy định bảo mật và quản lý hệ thống, đảm bảo rằng các cấu hình quan trọng luôn có bản sao dự phòng.

## **2. Các Phương Pháp Backup và Restore Cấu Hình trên Switch Cisco**

### **2.1. Phương Pháp Sao Lưu Cấu Hình**

1. **Sao lưu thủ công qua CLI (Command Line Interface):** Sử dụng các lệnh cơ bản trên CLI để sao lưu cấu hình trực tiếp trên switch.
2. **Sao lưu qua TFTP, FTP, SCP:** Sử dụng giao thức TFTP (Trivial File Transfer Protocol), FTP (File Transfer Protocol), hoặc SCP (Secure Copy Protocol) để truyền file cấu hình tới máy chủ từ xa.
3. **Sao lưu định kỳ với Kron:** Sử dụng tính năng Kron trên Cisco để lên lịch sao lưu tự động.
- Trivial File Transfer Protocol (TFTP): là 1 giao thức truyền file đơn giản, cho phép client có thể upload hoặc download các tệp tin trên các remote host như switch, router, ... TFTP được thiết kế nhỏ và dễ thực hiện nên nó thiếu hầu hết các tính năng nâng cao của các giao thức truyền tệp. TFTP chỉ đọc và ghi tệp từ các máy chủ từ xa. 
  - TFTP thường được ứng dụng trong mạng LAN để backup, import config IOS trên các thiết bị switch, router, hoặc cài đặt lisence
  - TFTP sử dụng giao thức UDP làm giao thức truyền tải và sử dụng cổng 69 làm cổng mặc định
  - Cài đặt TFTP64 để thực hiện lab.
