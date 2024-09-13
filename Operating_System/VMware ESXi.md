## VMware ESXi:
### 1. Khái niệm:
- VMware ESXi là sản phẩm được phát triển bởi VMware.
- Đây là 1 công cụ giám sát máy ảo (hypervisor) loại 1 dành cho doanh nghiệp.
- Cho phép tạo và quản lý các máy ảo trực tiếp trên phần cứng máy chủ mà không cần hệ điều hành trung gian.
- ESXi chứa các thành phần lõi của 1 hệ điều hành như kernel và có thể chạy trực tiếp trên phần cứng của hệ thống
- ESXi phân chia các tài nguyên CPU, RAM, bộ nhớ ngoài và tài nguyên mạng của server vật lý thành nhiều máy ảo khác nhau. Vì vậy, những ứng dụng chạy trong máy ảo không cần truy cập vào phần cứng bên dưới vẫn có thể trực tiếp 
### 1.1. Hypervisor type 1 (Bare-Metal): Được cài đặt trực tiếp trên phần cứng vật lý của máy chủ mà không cần hệ điều hành trung gian
- Ưu điểm:
  - Hiệu năng cao: Do tương tác trực tiếp với phần cứng
  - Bảo mật tốt hơn: Ít lớp phần mềm hơn, giảm nguy cơ tấn công
  - VD: VMware ESXi, Microsoft Hyper-V
### 1.2. Hypervisor type 2 (Hosted Hypervisor): Chạy trên hệ điều hành của máy chủ và hoạt động như 1 ứng dụng
- Ưu điểm:
  - Dễ cài đặt và dễ sử dụng: Thích hợp cho môi trường phát triển và thử nghiệm
  - Tương thích tốt: Có thể chạy trên nhiều hệ điều hành khác nhau.
  - VD: VMware Workstation, Oracle VirtualBox
