## VMware ESXi:
### 1. Khái niệm:
- VMware ESXi là sản phẩm được phát triển bởi VMware.
- Đây là 1 công cụ giám sát máy ảo (hypervisor) loại 1 dành cho doanh nghiệp.
- Cho phép tạo và quản lý các máy ảo trực tiếp trên phần cứng máy chủ mà không cần hệ điều hành trung gian.
- ESXi chứa các thành phần lõi của 1 hệ điều hành như kernel và có thể chạy trực tiếp trên phần cứng của hệ thống
- ESXi phân chia các tài nguyên CPU, RAM, bộ nhớ ngoài và tài nguyên mạng của server vật lý thành nhiều máy ảo khác nhau. Vì vậy, những ứng dụng chạy trong máy ảo không cần truy cập vào phần cứng bên dưới vẫn có thể trực tiếp sử dụng các tài nguyên này.
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

### 2. Đặc điểm:
- Hiệu năng cao: Do chạy trực tiếp trên phần cứng, ESXi tối ưu hoá việc sử dụng tài nguyên hệ thống
- Bảo mật: ESXi cung cấp các tính năng bảo mật mạnh mẽ, bao gồm kiểm soát truy cập dựa trên vai trò và ghi nhật ký
- Quản lý dễ dàng: Sử dụng giao diện người dùng đồ hoạ (GUI) và các công cụ điều khiển từ xa như vSphere Client

### 3. Lợi ích:
- Tối ưu hoá tài nguyên: Cho phép hợp nhất nhiều máy ảo trên 1 máy chủ vật lý, giúp tiết kiệm chi phí phần cứng
- Tính linh hoạt: Hỗ trợ nhiều hệ điều hành và cấu hình phần cứng khác nhau
- Khả năng mở rộng: Có thể quản lý hàng trăm máy ảo trên 1 máy chủ duy nhất

### 4. Cài đặt VMware ESXi trên iDRAC:
- Đăng nhập vào iDRAC:
![image](https://github.com/user-attachments/assets/184b4cab-4a7a-44bb-b719-fd902ce001f1)

- Vào `Launch` để vào giao diện cài đặt:
![image](https://github.com/user-attachments/assets/9ca2d237-dc45-46c1-b874-1268d88637d1)

- Vào `Virtual Media`, chọn file ISO của ESXi đã tải về và map vào ổ CD/DVD ảo
![image](https://github.com/user-attachments/assets/b1d91a80-128a-4b16-8f07-5afc483a05b6)



