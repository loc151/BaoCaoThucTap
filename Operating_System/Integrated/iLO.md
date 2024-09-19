## 1. Khái niệm:
- iLO (intergrated Lights Outs) mang đến tính năng quản lý cho server cùng các thông số hardware từ xa, troubleshoot và remote thông qua 1 giao diện
- iLo là 1 cổng riêng biệt trên server HP, sở hữu chương trình cùng phần cứng độc lập.
- iLo giúp ta quản lý phần cứng server 1 cách độc lập, thậm chí là nó còn có chương trình WebGUI để quản lý và command line tương ứng.
- iLO được cấu hình nhờ port riêng, kết nối qua đường RJ45 được cấu hình thông số network

## 2. Cấu hình iLO:
### 2.1. Khởi động server HP, nhấn F8 khi thấy dòng **Config iLO**
### 2.2. Cấu hình Network:
- Tắt chế độ DHCP: Network -> DNS/DHCP -> OFF
- Nhập các thông số địa chỉ IP: Network -> NIC and TCP/IP

### 2.3. Cấu hình password cho user:
- Change pass user administrator: User -> Nhập mật khẩu mới -> F10 để lưu

### 2.4. Đăng nhập vào iLO:
- Sau khi cấu hình cơ bản, thoát ra và reboot
- Đăng nhập vào iLO qua địa chỉ IP và tài khoản đã cấu hình:
![image](https://github.com/user-attachments/assets/7cd4bd6b-368a-41ac-b8a8-ebeaee052e12)

- Giao diện sau khi đăng nhập thành công:
![image](https://github.com/user-attachments/assets/0264f717-5214-4637-a3fd-bf92000df5ab)

## 3. Giám sát các thông tin trên iLO:
### 3.1. Information:
Overview: Hiển thị server firmware cùng trạng thái bật/tắt
- **System Information**: Thể hiện trạng thái và thông tin các bộ phân của HP server
![image](https://github.com/user-attachments/assets/a5fa86d8-3e70-4e87-8e66-504d4657dc6d)

- **iLO event log**: Ghi lại nhật kí việc cài thông tin iLO
![image](https://github.com/user-attachments/assets/23985fb8-d33d-49c2-b157-3b01d90ffc93)

- **Intergrated Management Log**: Thông tin nhật ký về vận hành phần cứng HP server
![image](https://github.com/user-attachments/assets/80122d61-6e93-4072-a491-abc80874ba01)

### 3.2. Virtual Media:
- Tính năng chính: đính kèm file ISO, giúp cài đặt OS từ xa cũng như chỉnh sửa thứ tự boot
![image](https://github.com/user-attachments/assets/ab81bc9f-1071-4652-8824-467a4d364c30)

### 3.3. Power Management:
- Tính năng quản lý bật/tắt server từ xa:
![image](https://github.com/user-attachments/assets/b3c8dea5-f594-4bcd-b5e9-2d76188642c2)

### 3.4. Administration:
Tính năng quản lý thông tin cho iLO
- **iLo Firmware**: thể hiện về firmware iLO
![image](https://github.com/user-attachments/assets/71bcd354-0f67-4825-ae83-701711349cb4)

- **User Administration**: Thiết lập tài khoản login iLO
![image](https://github.com/user-attachments/assets/7888f50a-72db-4adc-8e2b-ab7902bf686c)

- **Access Settings**: Cài đặt kiểm soát truy cập đến các port server
![image](https://github.com/user-attachments/assets/2184d6da-7cb5-4ca5-bfbc-150a56c53eb6)

- **Security**: Thiết lập login đến iLO
![image](https://github.com/user-attachments/assets/df2dafbb-641e-4765-b44c-ffd9aae282ba)

- **Network**: Thiết lập thông tin IP cho port iLO
![image](https://github.com/user-attachments/assets/73d50bea-0e2d-460c-8d41-c6f39d13189a)
