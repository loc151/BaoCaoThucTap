# Tổng quan về SAN
## 1. Khái niệm:
- **Storage Area Network (SAN)**, một loại mạng lưu trữ chuyên dụng cho việc kết nối các thiết bị lưu trữ như ổ cứng, đĩa quang, băng từ với các máy chủ
- **SAN** cho phép các máy chủ truy cập vào các thiết bị lưu trữ như thể chúng là ổ đĩa cục bộ, nhưng lại có khả năng mở rộng và quản lý tốt hơn
![image](https://github.com/user-attachments/assets/f9a172ff-176e-4e34-9ffa-316d788055bc)
---

## 2. Các thành phần chính:
### 2.1. Server:
- Server (máy chủ): là các máy tính có nhiệm vụ xử lý các yêu cầu của người dùng hoặc các ứng dụng.
- Server có thể sử dụng hệ điều hành Windows, Linux, Unix hoặc các hệ điều hành khác.
- Server cần có một giao diện kết nối với SAN, thường là một card mạng quang (Fibre Channel) hoặc Ethernet.

### 2.2. Storage:
- **Storage (Lưu trữ)** là các thiết bị dùng để lưu trữ dữ liệu, có thể là ổ cứng, đĩa quang, băng từ hoặc các thiết bị khác.
- Storage có thể được tổ chức thành các khối lưu trữ logic (LUN) và được gán cho các máy chủ thông qua SAN.
- Storage có thể được quản lý bằng phần mềm hoặc phần cứng.

### 2.3. Network infrastructure:
- **Network infrastructure (Cơ sở hạ tầng mạng)**: là các thiết bị dùng để kết nối server và storage, có thể là switch, router, hub hoặc các thiết bị khác.
- **Network infrastructure** có thể sử dụng các giao thức khác nhau để truyền tải dữ liệu, như Fibre Channel, iSCSI, FCoE hoặc InfiniBand.
---

## 3. Tính năng:
- **Tăng hiệu suất**: SAN cho phép các máy chủ truy cập vào storage với tốc độ cao và độ trễ thấp, do đó giảm thiểu thời gian xử lý và tăng hiệu suất của các ứng dụng.
- **Tăng khả năng mở rộng**: SAN cho phép thêm hoặc bớt storage một cách linh hoạt và nhanh chóng, do đó đáp ứng được nhu cầu lưu trữ ngày càng tăng của doanh nghiệp.
- **Tăng khả năng an toàn**: SAN cho phép bảo vệ dữ liệu bằng các biện pháp như mã hóa, sao lưu, phục hồi và sao chép. SAN cũng giúp ngăn chặn sự can thiệp của người dùng hoặc máy chủ không được phép vào storage.
- **Tăng khả năng quản lý**: SAN cho phép quản lý storage từ một điểm trung tâm, do đó giảm thiểu chi phí và công sức của nhân viên IT. SAN cũng cho phép theo dõi và giám sát hiệu suất và tình trạng của storage.
---

## 4. Các giao thức:
- **Fibre Channel (FC)**: Là một giao thức truyền tải dữ liệu qua cáp quang, có tốc độ cao (từ 1 Gbps đến 128 Gbps) và độ tin cậy cao. FC là giao thức truyền thống của SAN, được sử dụng rộng rãi trong các môi trường yêu cầu hiệu suất cao, như cơ sở dữ liệu, máy chủ ảo hoặc máy chủ lớn.
- **Internet Small Computer System Interface (iSCSI)**: Là một giao thức truyền tải dữ liệu qua mạng Ethernet, có tốc độ thấp hơn FC (từ 1 Gbps đến 40 Gbps) nhưng chi phí thấp hơn và dễ triển khai hơn. iSCSI là giao thức phù hợp cho các môi trường yêu cầu khả năng mở rộng và linh hoạt, như máy chủ nhỏ hoặc máy chủ đám mây.
- **Fibre Channel over Ethernet (FCoE)**: Là một giao thức kết hợp giữa FC và Ethernet, có tốc độ cao (từ 10 Gbps đến 100 Gbps) và chi phí thấp hơn FC. **FCoE** là giao thức mới của SAN, được sử dụng trong các môi trường yêu cầu hiệu suất cao và tiết kiệm chi phí, như trung tâm dữ liệu.

### 4.1. iSCSI SAN:
- **iSCSI** là Internet SCSI ( Small Computer System Interface ) là một chuẩn công nghiệp phát triển để cho phép truyền tải các lệnh SCSI qua mạng IP hiện có bằng cách sử dụng giao thức TCP/IP.
- Các thiết bị **iSCSI SAN** (hay IP SAN) là các Server (chạy HĐH nào đó, như Win Storage) và có cài tính năng hỗ trợ iSCSI ở phía server (gọi là iSCSI target). Các máy truy cập đến thiết bị IP SAN bằng iSCSI sẽ phải hỗ trợ tính năng iSCSI client (gọi là iSCSI source). iSCSI source (client) được cài sẵn trong Win Vista/7 và 2008. Đối với iSCSI target, có nhiều Soft, ví dụ StarWind trên nền Win, và OpenFiler trên nền Linux.
- **iSCSI** dễ dùng, linh hoạt, dễ mở rộng, vì hoạt động dựa trên nền IP và Ethernet / Internet, không đòi hỏi phần cứng đặc biệt. Đặc biệt hiệu quả khi mạng Ethernet 10G phổ biến.

=> Nếu như giao thức iSCSI hoạt động trên nền IP, và từ lớp Internet trở lên, thì giao thức Fiber Channel (1 loại SAN khác) hoạt động ở mức Physical layer, nên phụ thuộc nhiều vào phần cứng, cần đến phần cứng riêng biệt, bao gồm các Switch, NIC (HBA) và thiết bị lưu trữ/cáp hỗ trợ Fiber channel. Vì không hoạt động trên nền IP nên không linh động và khó mở rộng, so với IP SAN. Dù khó dùng và đắt tiền, Fiber Channel SAN đã và đang là giải pháp SAN chính của nhiều hệ thống lớn.
