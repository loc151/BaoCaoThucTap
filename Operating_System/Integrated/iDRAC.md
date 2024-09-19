## 1. Khái niệm:
- iDRAC (Integrated Dell Remote Access Controller) là 1 phần cứng được tích hợp sẵn trên bo mạch chủ (mainboard) của các dòng **Dell Server**.
- iDRAC với bộ xử lý, bộ nhớ và network riêng để truy cập vào bus hệ thống.
- Nó cung cấp quyền truy cập từ xa vào console (bàn phím và màn hình) cho phép truy cập giao diện BIOS hệ thống qua Internet.
- Là 1 tính năng giúp hỗ trợ người quản trị IT hoặc kỹ sư hệ thống có thể quản lý máy chủ 1 cách linh động hơn từ xa mà không cần ngồi cạnh các server.

## 2. Vai trò:
### 2.1. Tình huống:
- Trong quá trình vận hành server đã xảy ra nhiều trường hợp các server được đặt ở Datacenter gặp phải sự cố về phần cứng mà người quản trị không thể giám sát và có cảnh báo kịp thời.
### 2.2. Hậu quả:
- Dẫn tới những sự cố khi các thiết bị ngừng hoạt động trong thời gian dài (downtime) mà không được khắc phục nhanh chóng
### 2.3. Giải pháp:
- iDRAC được ra đời nhằm mang đến giải pháp cho các kỹ sư hệ thống trong việc nhận biết các sự cố server từ xa
- Giúp người quản trị quản lý được các thông số hardware, troubleshoot từ xa và remote thông qua 1 giao diện web
- Giúp vận hành hệ thống kịp thời, nhanh chóng, giúp các cá nhân, tổ chức hay doanh nghiệp tránh được thiệt hại lớn trong quá trình vận hành máy chủ 

## 3. Cài đặt:
### 3.1. Khởi động máy chủ Dell của bạn và nhấn phím F2 để vào **System Setup**:
![image](https://github.com/user-attachments/assets/61a0565c-dd5b-40b7-b3db-024989cbb938)

### 3.2. Chọn phần **iDRAC Settings**:
![image](https://github.com/user-attachments/assets/ba9097e2-80c7-4fac-abea-f7a71d1d2f4c)

### 3.3. Trong phần iDRAC Settings tuỳ chỉnh cấu hình địa chỉ IP cho iDRAC:
![image](https://github.com/user-attachments/assets/cd3a56d3-bad9-4e38-8bb8-934edf222b7d)

### 3.4. Setup user login vào iDRAC:
- Quay trở lại tab Setup chọn **User Configuration**:
![image](https://github.com/user-attachments/assets/62951cfa-a07e-4a7d-aafe-8947afde490f)

- Thiết lập password cho user root:
![image](https://github.com/user-attachments/assets/9746ae49-cedf-4974-b968-492fbb07a885)

### 3.5. Chọn Yes để chấp nhận các thay đổi và khởi động lại server:
![image](https://github.com/user-attachments/assets/80f87923-ac78-44c2-b88c-a25e2fd431db)

## 4. Cách sử dụng:
- Đăng nhập vào iDRAC thông qua địa chỉ ip và username/password đã thiết lập:
![image](https://github.com/user-attachments/assets/8f41a8e2-e01f-4668-aa80-c2e14c076e05)

- Giao diện iDRAC khi đăng nhập thành công
![image](https://github.com/user-attachments/assets/a5551bee-736d-48c9-991c-8d0505045c36)

### 4.1. Tab Server:
- Ở trong phần Properties sẽ cung cấp các thông tin chung về server và đường link truy cập nhanh tới các mục khác, cửa sổ console để remote desktop, thao tác nhanh đối với như Power ON/ OFF. Xem thông tin về về server như BIOS, IP, Firmware OS.
![image](https://github.com/user-attachments/assets/44c38203-c79c-44eb-ac34-2747d2f50727)

- Phần **Attached Media** cho biết cấu hình cho phép việc đính kèm file ISO của OS, cho bạn biết nên chia sẻ file hay không.
![image](https://github.com/user-attachments/assets/eff3c17d-ff42-4453-8c21-b5e5eedbfe2a)

- **Log** để hiển thị thông tin log đối với server và có sắp xếp theo mức độ, time/ date
![image](https://github.com/user-attachments/assets/8c6270a0-bc0f-44a7-a3e8-b3e5ca97c714)

- **Power / Thermal**: Hiển thị các thông tin về nguồn và nhiệt độ của server
![image](https://github.com/user-attachments/assets/3c5e3dd2-90a0-4c16-ada3-21317063ff69)

- **Virtual Console**: Thiết lập về các thông số cho việc console tới server từ xa.
![image](https://github.com/user-attachments/assets/902f5994-41bc-49ac-b83a-662938aad11a)

- **Setup**: Thiết lập thứ tự boot cho server khi khởi động:
![image](https://github.com/user-attachments/assets/b7123f66-3421-4520-8a62-f994dbd3b4e3)

### 4.2. iDRAC Settings:
- **Properties**: Cung cấp thông tin về các thông số setup cho iDRAC như IP network, user
![image](https://github.com/user-attachments/assets/1a3e1ec9-03a3-4db6-8f75-999353695591)

- **Network**: Thông tin cấu hình network cho iDRAC
![image](https://github.com/user-attachments/assets/d24e8eb3-bc31-48f1-a37e-e21c8a60b7fa)

- **User Authentication**: Thông tin liên quan đến setup user login iDRAC
![image](https://github.com/user-attachments/assets/c820e000-b5be-401e-b22b-c30eadaafa14)

- **Update and Rollback**: Update firmware cho iDRAC
![image](https://github.com/user-attachments/assets/6f29136e-af92-4378-a82b-caf22c470cc1)

- **Sessions**: Hiển thị phiên kết nối vào trình iDRAC
![image](https://github.com/user-attachments/assets/e6060f28-298d-429c-a66b-3b31d6d14d4d)

### 4.3. Hardware:
- Có thể xem đầy đủ các thông tin về phần cứng của server:
![image](https://github.com/user-attachments/assets/030379e3-01db-42b5-9a96-a2feee4611d6)

### 4.4. Storage:
- Theo dõi được các thông tin về storage của server:
![image](https://github.com/user-attachments/assets/953ec4f1-b6de-4639-b793-ca47027c20f0)
