# Hướng Dẫn Cài Đặt Veeam Backup & Replication

## Yêu Cầu Hệ Thống

### Phần Cứng
- **CPU:** Tối thiểu 2-core, khuyến nghị 4-core
- **RAM:** Tối thiểu 4 GB, khuyến nghị 8 GB
- **Dung Lượng Ổ Đĩa:** Tối thiểu 500 GB trống cho việc lưu trữ sao lưu
- **Kết Nối Mạng:** 1 Gbps hoặc nhanh hơn

### Phần Mềm
- **Hệ Điều Hành:** Windows Server 2016/2019/2022
- **Phiên Bản SQL Server:** SQL Server Express sẽ được cài đặt tự động nếu chưa có.

## Chuẩn Bị

1. **Máy Chủ Cài Đặt:**
   - Chuẩn bị một máy chủ Windows với hệ điều hành được hỗ trợ.
   - Kiểm tra xem máy chủ có đủ tài nguyên phần cứng để chạy Veeam Backup & Replication.

2. **Tài Khoản Quản Trị:**
   - Đảm bảo có tài khoản với quyền quản trị trên máy chủ Windows nơi Veeam sẽ được cài đặt.

3. **Kết Nối Mạng:**
   - Đảm bảo máy chủ có thể kết nối đến các máy chủ ESXi hoặc hạ tầng ảo hóa khác mà bạn muốn sao lưu.

## Tải Về và Cài Đặt

1. **Tải Về Veeam Backup & Replication:**
   - Truy cập vào [trang chủ Veeam](https://www.veeam.com/backup-replication-download.html) và tải về phiên bản Veeam Backup & Replication.

2. **Chạy Trình Cài Đặt:**
   - Chạy file cài đặt `.exe` và làm theo hướng dẫn trên màn hình.

3. **Chọn Các Thành Phần Cần Cài Đặt:**
   - Chọn các thành phần sau trong quá trình cài đặt:
     - **Veeam Backup Server**
     - **Veeam Backup Console**
     - **Veeam Backup Catalog**
     - **Veeam Backup & Replication PowerShell module** (tuỳ chọn)

  ![Hình ảnh quá trình cài đặt Veeam](https://github.com/cuongnvvietis/NhanHoa/blob/main/Docs/Esxi/Picture/Veem/Screenshot_74.png)

4. **Cài Đặt SQL Server Express (Nếu Cần):**
   - Nếu không có SQL Server trên máy chủ, Veeam sẽ tự động cài đặt SQL Server Express.

  ![Hình ảnh quá trình cài đặt Veeam](https://github.com/cuongnvvietis/NhanHoa/blob/main/Docs/Esxi/Picture/Veem/Screenshot_77.png)

5. **Hoàn Thành Cài Đặt:**
   - Sau khi cài đặt xong, khởi động lại máy chủ nếu được yêu cầu.

## Cấu Hình Ban Đầu

1. **Khởi Động Veeam Backup & Replication:**
   - Sau khi cài đặt, mở **Veeam Backup & Replication Console** từ máy chủ.

2. **Cấu Hình Repository (Kho Lưu Trữ):**
   - Từ giao diện, vào **Backup Infrastructure** > **Backup Repositories**.
   - Thêm hoặc cấu hình một repository mới để lưu trữ bản sao lưu. Bạn có thể chọn ổ đĩa cục bộ hoặc ổ đĩa mạng.

## Thêm Máy Chủ ESXi

1. **Thêm Máy Chủ ESXi:**
  - Trong Veeam Console, vào **Backup Infrastructure** > **Managed Servers**.
  - Chọn **Add Server** và thêm thông tin đăng nhập cho máy chủ ESXi của bạn.
  - Veeam sẽ xác thực và kết nối đến máy chủ ESXi.

![image](https://github.com/user-attachments/assets/53b00e58-09e1-4475-87b2-d33663c1ccea)

2. **Xác Thực Kết Nối:**
  - Veeam sẽ xác thực và thu thập thông tin về các máy ảo trên máy chủ ESXi.
  - Ở mục **Add server**, chọn **VMware Vsphere**:
    
![image](https://github.com/user-attachments/assets/aa75f5d5-099c-42ba-ba3d-51b3eee62700)

  - Chọn **vSphere**:
    
![image](https://github.com/user-attachments/assets/226b946d-ee36-4f73-a6c6-f0123fbb40c6)

  - Điền địa chỉ IP của ESXi Host vào mục **Name**:
    
![image](https://github.com/user-attachments/assets/292ceffd-1e6b-4c5c-86ba-1cd2fbbbd79e)

  - Điền user và pass sử dụng cho ESXi Host:
    
![image](https://github.com/user-attachments/assets/eb972337-b280-4f71-bf82-74c4406b60e7)
![image](https://github.com/user-attachments/assets/f9c5f483-4546-47f1-be1c-5e10dfc55426)

  - Sau khi Veeam xác thực và thu thập thông tin về các máy ảo trên máy chủ ESXi, nhấn **Finish** để hoàn tất việc liên kết:
    
![image](https://github.com/user-attachments/assets/f73e5e16-4775-4cee-bd14-4ef09a5f5bfa)

## Thiết Lập Job Sao Lưu

1. **Tạo Job Sao Lưu:**
   - Trong giao diện **Home**, chọn **Backup Job** và làm theo các bước hướng dẫn để thiết lập job sao lưu cho các máy ảo trên ESXi.

2. **Chọn Máy Ảo:**
   - Chọn các máy ảo mà bạn muốn sao lưu từ danh sách trên máy chủ ESXi.

3. **Chọn Repository:**
   - Chọn repository để lưu trữ bản sao lưu.

4. **Đặt Lịch Trình Sao Lưu:**
   - Đặt lịch trình sao lưu tự động theo ngày hoặc tuần.

![image](https://github.com/user-attachments/assets/2b22e16d-b40d-4a10-aa92-2b11ecb94dce)


5. **Hoàn Thành Job Sao Lưu:**
   - Kiểm tra lại các tùy chọn và hoàn tất việc thiết lập job sao lưu.
![image](https://github.com/user-attachments/assets/2c3350de-7942-4f98-83fd-e1be4621275d)

---

Sau khi hoàn thành, Veeam Backup & Replication sẽ tự động sao lưu các máy ảo theo lịch trình bạn đã cấu hình.
  - Quá trình backup:
![image](https://github.com/user-attachments/assets/5976b51a-7333-49d4-9790-be0d917991bf)

  - Sao lưu thành công:
![image](https://github.com/user-attachments/assets/385616a8-2df4-4c6d-aa26-6f6cc5542073)

   - Vị trí lưu file backup:
![image](https://github.com/user-attachments/assets/83de89a1-5cfc-4e1a-8503-c9df9977d3f4)
