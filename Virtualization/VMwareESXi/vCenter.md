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

## 3. Tải và Mount File ISO:
### 3.1. **Mount File ISO:**
- Trên máy tính cài đặt (Windows/Linux/Mac), sử dụng phần mềm mount file ISO (như Daemon Tools, PowerISO, hoặc sử dụng tính năng tích hợp trong hệ điều hành).

![image](https://github.com/user-attachments/assets/0c138ecf-6561-4a26-9d71-66dd5bb81794)

- Sau khi mount, bạn sẽ thấy một thư mục ảo chứa các file cài đặt của vCenter.

![image](https://github.com/user-attachments/assets/c775c31a-2ae1-415c-9a62-87f5e61dee42)

### 3.2. **Chạy Trình Cài Đặt:**
- Vào thư mục chứa file cài đặt và chạy file **`installer.exe`** (trên Windows) hoặc **`installer`** (trên Linux).
  
![image](https://github.com/user-attachments/assets/41d4da3b-e9da-4ee6-a2e4-a15124ebe223)

## 4. Cài đặt vCenter Server - Stage 1:
- Chọn `Install` để bắt đầu quá trình cài đặt:
  
![image](https://github.com/user-attachments/assets/613c5ef3-e8c7-4039-a2d0-2c3ba45a8cc0)

- Tích vào **I accept the terms of the license agreement**:
  
![image](https://github.com/user-attachments/assets/f8bf7d98-9428-4875-87cf-71d1553da2e4)

- Chọn **Embedded Platform Services Controller**:
  
![image](https://github.com/user-attachments/assets/e15d2df2-d2a3-43d5-b8a3-616caa9be98d)

- Điền địa chỉ của máy chủ ESXi sẽ cài đặt vCenter Server lên. Cung cấp thông tin xác thực của ESXi host để tiếp tục.
  
![image](https://github.com/user-attachments/assets/9791eff6-1e33-4fab-b02e-07f76b64d7f2)

- Thiết lập máy ảo cho thiết bị:
  
![image](https://github.com/user-attachments/assets/63930809-53bf-4497-b4f6-82c4d0c4947c)

- Chọn kích thước triển khai:
  
![image](https://github.com/user-attachments/assets/fbc3597a-8cef-4307-a477-bce9f739e61b)

- Chọn kho dữ liệu:
  
![image](https://github.com/user-attachments/assets/cb2e6e1a-6ca5-436a-b9aa-a1db7c630e22)

- Cấu hình thông tin vCenter:

![image](https://github.com/user-attachments/assets/ec1e212d-2db9-4698-a918-4187b0f7d2dd)

- Xác nhận lại các thông số và tiến hành cài đặt bước 1:
  
![image](https://github.com/user-attachments/assets/5f799075-d2f8-4517-829b-656cf2fbcc55)

- Sau khi cài đặt thành công, chương trình sẽ hiển thị tiến hành **Stage 2**:
![image](https://github.com/user-attachments/assets/6d987d7c-3bdd-422e-9f80-f88caeb5c0e3)

## 5. Cấu hình vCenter Server - Stage 2: 
- Chọn **Continue** để tiếp tục
- Thiết lập và xác nhận các cấu hình:

![image](https://github.com/user-attachments/assets/15e57ea5-b46b-4a47-b63d-de6689071194)
![image](https://github.com/user-attachments/assets/e82f62eb-efbe-4845-96a5-e220c1d9e78a)
![image](https://github.com/user-attachments/assets/59ef5f92-f0f1-4fcc-ad54-e9377ff0b7a9)
![image](https://github.com/user-attachments/assets/df247d75-ecac-4b1d-98de-4d19c7580563)


