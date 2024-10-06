# Cấu hình Network:
## Flat Network (Mạng phẳng):
### 1. Khái niệm: 
-  Là một kiến trúc mạng trong đó tất cả các thiết bị mạng đều nằm trong cùng một phân đoạn mạng, không có sự phân chia thành các mạng con (subnet) hoặc VLANs.
-  Tất cả các thiết bị có thể giao tiếp trực tiếp với nhau mà không cần thông qua các thiết bị định tuyến (router) hoặc chuyển mạch (switch) phức tạp

### 2. Ưu điểm:
- **Đơn giản hóa quản lý:** Do không có sự phân chia mạng, việc quản lý và cấu hình mạng trở nên đơn giản hơn.
- **Giảm chi phí:** Không cần đầu tư vào các thiết bị định tuyến hoặc chuyển mạch phức tạp.
- **Dễ dàng mở rộng:** Thêm thiết bị mới vào mạng mà không cần cấu hình phức tạp.

### 3. Nhược điểm: 
- **Bảo mật kém:** Do tất cả các thiết bị đều nằm trong cùng một phân đoạn mạng, việc kiểm soát truy cập và bảo mật trở nên khó khăn hơn.
- **Hiệu suất giảm:** Khi số lượng thiết bị tăng lên, lưu lượng mạng có thể trở nên quá tải, dẫn đến giảm hiệu suất.
- **Khó khăn trong việc quản lý lưu lượng:** Không có khả năng phân chia lưu lượng mạng, dẫn đến khó khăn trong việc quản lý và tối ưu hóa lưu lượng.

### 4. Cấu hình:
- Mỗi khi tạo VM mới trên VMware ESXi, sẽ có 1 vSwitch ảo để kết nối với VM (vlan 0)
![image](https://github.com/user-attachments/assets/7a43e151-e7a4-4591-92bb-07e14f797361)


## MultiVLAN:
### 1. Đặc điểm:
- **Phân đoạn mạng:** Multi-VLAN cho phép phân đoạn một mạng vật lý thành nhiều mạng logic độc lập, giúp cải thiện bảo mật và quản lý lưu lượng mạng
- **Tăng cường bảo mật:** Bằng cách tách biệt các thiết bị và lưu lượng mạng vào các VLAN khác nhau, Multi-VLAN giúp ngăn chặn truy cập trái phép và giảm thiểu nguy cơ tấn công mạng
- **Quản lý linh hoạt:** Multi-VLAN cho phép quản trị viên mạng dễ dàng quản lý và cấu hình các mạng con khác nhau, phù hợp với nhu cầu cụ thể của từng bộ phận hoặc ứng dụng
- **Hiệu suất tối ưu:** Việc phân chia mạng thành các VLAN nhỏ hơn giúp giảm thiểu lưu lượng broadcast và cải thiện hiệu suất mạng tổng thể


### 2. Cấu hình: 
### 2.1. Tại switch:
- Cấu hình địa chỉ IP cho `Vlan10` và `Vlan20`:

![image](https://github.com/user-attachments/assets/d0a48c95-7ea7-4465-96c7-4d4fd458af46)

- Cấu hình liên kết trunk để các Vlan có thể liên lạc với nhau: 

![image](https://github.com/user-attachments/assets/2d7cfda6-6312-4048-85af-3666c578ae6e)

- Tại **ESXi Host**, chọn **Networking -> Virtual Switches -> Add standard virtual switch**:

![image](https://github.com/user-attachments/assets/6d55daef-8dfd-4052-a62c-3559cf55e597)

- Tạo vSwitch mới: 
![image](https://github.com/user-attachments/assets/dd7f021c-5532-409c-a258-06cbfeecee46)

### 2.2. Tại ESXi Host: Tạo Port Groups cho VLAN:
- Chọn vSwitch `SW-TRUNK` từ danh sách các Virtual Switches.
- Nhấp vào **Edit Settings**.
- Trong phần **Ports**, chọn **Add** để thêm một Port Group mới.
- Nhập tên cho Port Group là `VLAN 10` và cấu hình VLAN ID là `10`. Nhấp vào **OK** để lưu.
- Lặp lại quy trình để tạo một Port Group khác với tên là `VLAN 11` và VLAN ID là `11`.
![image](https://github.com/user-attachments/assets/f55b76c9-3b5c-4145-ae2a-4ea16f6760c5)

### 2.3. Mô hình MultiVLAN:
- Đây là mô hình khi cấu hình mạng dạng MultiVLAN, yêu cầu là các VM trong cùng 1 VLAN, hoặc khác VLAN nhưng dùng chung một switch có thể liên lạc được với nhau thông qua liên kết trunk. 
![image](https://github.com/user-attachments/assets/afb34af0-5900-4d0c-a1b4-48e6c3fdf476)


### 2.4 Cấu hình VM:
- Với hệ điều hành Ubuntu: Tạo 2 máy ảo, cấu hình IP sao cho cả 2 máy đều cùng trong 1 vlan (VLAN10)
- Sau khi cấu hình, kiểm tra xem 2 máy có liên lạc được với nhau hay không:
- Máy **Ubuntu 22** (`192.168.10.3`) và **Ubuntu 22.1** (`192.168.10.2`)

![image](https://github.com/user-attachments/assets/775ba11a-75b0-412d-b82a-46525183222b)

![image](https://github.com/user-attachments/assets/019802b0-6ac5-48fb-9c3d-3efdb20810e4)

- Với hệ điều hành Windows: Cấu hình địa chỉ IPv4 sao cho phù hợp với địa chỉ mạng của **Vlan20**

![image](https://github.com/user-attachments/assets/addbf555-1772-4bd3-b35a-f0c8b7e0a4ed)

- Kiểm tra xem **VM Windows** với `Vlan20` có thể liên lạc được với các **VM Ubuntu** với `Vlan10` hay không:
![image](https://github.com/user-attachments/assets/e94ae3eb-78f6-4b20-9ad6-7472174993cd)

- Kiểm tra ngược lại: 
![image](https://github.com/user-attachments/assets/ed7dcfc6-6a9c-4fd0-9eca-4d0df28584fe)
![image](https://github.com/user-attachments/assets/d527b5e4-45e5-4409-b54c-93fbb76c2f47)


