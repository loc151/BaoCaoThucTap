## 1. Yêu Cầu Hệ Thống

Trước khi cài đặt, đảm bảo máy chủ đáp ứng các yêu cầu sau:
- **CPU:** Tối thiểu 2 CPU, 4 cores.
- **RAM:** Tối thiểu 12 GB RAM.
- **Dung Lượng Ổ Đĩa:** Tối thiểu 300 GB dung lượng đĩa trống.
- **ESXi Host:** vCenter yêu cầu một máy chủ ESXi để cài đặt. Cần ESXi 6.5 trở lên.
- **DNS:** Đảm bảo cấu hình DNS chính xác và có thể phân giải tên vCenter Server.

## 2. Chuẩn Bị Cài Đặt

### 2.1. **Download vCenter ISO:**
   - Truy cập trang chủ VMware và tải file ISO của vCenter Server về máy tính của bạn.

### 2.2. **Chuẩn Bị Tên và Địa Chỉ IP:**
   - Đặt trước hostname và địa chỉ IP cho vCenter Server.
   - Cấu hình DNS trên hệ thống của bạn để hostname và IP khớp nhau.

## 3. Tải và Mount File ISO

### 3.1. **Mount File ISO:**
   - Trên máy tính cài đặt (Windows/Linux/Mac), sử dụng phần mềm mount file ISO (như Daemon Tools, PowerISO, hoặc sử dụng tính năng tích hợp trong hệ điều hành).
  
   - Sau khi mount, bạn sẽ thấy một thư mục ảo chứa các file cài đặt của vCenter.

2. **Chạy Trình Cài Đặt:**
   - Vào thư mục chứa file cài đặt và chạy file **`installer.exe`** (trên Windows) hoặc **`installer`** (trên Linux).
