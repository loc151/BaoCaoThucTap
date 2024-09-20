## 1. Remote:
### 1.1. Bật Remote Desktop trong Windows Server (2019):
- Ấn vào biểu tượng **Start**, chọn **Remote Desktop Settings**
![image](https://github.com/user-attachments/assets/a2567217-156a-4507-9a7e-22c5a85b7cac)

- Lúc này, **Enable Remote Desktop** đang bị tắt, nhấn vào để bật chế độ này:
![image](https://github.com/user-attachments/assets/5578d18c-3642-464d-a0bf-7fd4dc5e658f)

![image](https://github.com/user-attachments/assets/3afaf544-d6a6-4db7-a6e7-23fc06d5d850)

- Dùng **Remote Desktop Connection** ở máy khác:
![image](https://github.com/user-attachments/assets/01c1f270-844f-4717-a233-c958b34e78da)

- Nhập địa chỉ IP của *Windows Server*: <p>
![image](https://github.com/user-attachments/assets/cf3927a4-f99e-4e2b-aba7-333632ea184e)

- Nhập *username* (nếu user đăng nhập lần đầu) và *password*:
![image](https://github.com/user-attachments/assets/825d8e95-1745-4138-b63f-09fa5c34d98d)

- Hiển thị như này tức là đã remote vào Windows Server thành công:
![image](https://github.com/user-attachments/assets/c27540a5-54bc-438a-b670-801450b9c101)

## 2. Change port remote:
### 2.1. Mở Registry Editor:
- Nhấn `Win + R`, gõ lệnh `regedit`, nhấn `Enter`:
![image](https://github.com/user-attachments/assets/155f6885-4fe5-4901-b5b7-c2ad236c4184)

- Đi đến khoá registry:
```shell
HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp
```
![image](https://github.com/user-attachments/assets/bf62db3b-3893-470f-9f03-0b7346e49089)

### 2.2. Chỉnh sửa giá trị PortNumber:
- Nhấp chuột phải `PortNumber` và chọn `Modify`
- Chọn `Demical` dưới mục Base
- Nhập số cổng muốn sử dụng (ví dụ cổng 151), nhấn `OK` để xác nhận
![image](https://github.com/user-attachments/assets/855d1999-543f-4a5d-87f9-d191322f8012)

### 2.3. Mở cổng trên Windows Firewall:
- Chạy lệnh sau trong PowerShell:
```shell
netsh advfirewall firewall add rule name="Remote Desktop Service" dir=in action=allow protocol=TCP localport=151
```
![image](https://github.com/user-attachments/assets/e75f18bc-546c-472c-83da-04b9719213aa)

### 2.4. Khởi động lại máy chủ để áp dụng thay đổi
### 2.5. Truy cập Remote Desktop Connection:
- Nhập `IP:Port` (ví dụ: 172.16.2.10:151)
![image](https://github.com/user-attachments/assets/9a720968-03fb-4075-89d6-e6dda261ebdd)

## 3. Nhiều user truy cập từ xa trong cùng 1 phiên:
### 3.1. Cho phép remote connection to this computer:
- Ở Windows Server 2019, vào **Control Panel** -> **System and Security** -> **System**
- Chọn **Remote Settings**
- Chọn *Allow remote connections to this computer*, nhấn `OK` để xác nhận thay đổi:
![image](https://github.com/user-attachments/assets/79a3415d-b4b6-4ebb-90b4-8f18673693bd)

### 3.2. Cấu hình Group Policy:
- Mở **Group Policy Editor**: Nhấn `Windows + R`, gõ `gpedit.msc`, nhấn `Enter`
- Điều hướng đến: **Computer Configuration -> Administrative Templates -> Windows Components -> Remote Desktop Services -> Remote Desktop Session Host -> Connections**
![image](https://github.com/user-attachments/assets/769adaa4-5bcc-4d45-bfed-855f8976c270)

### 3.3. Cấu hình các tuỳ chọn:
- Kích đúp vào **Restrict Remote Desktop Services user to a single Remote Desktop Services session**, đặt thành `Disabled`
![image](https://github.com/user-attachments/assets/13c86d27-61c7-41d7-b645-ab92b17f58d3)

- **Limit number of connections:** Đặt số lượng kết nối tối đa cho phép
![image](https://github.com/user-attachments/assets/8a3beaed-e23f-4c2a-b296-a19a422ce607)

- Vào **Command Prompt**, gõ lệnh sau để áp dụng tất cả các policy vừa cấu hình:
```
gpupdate/force
```

## 4. Enable and configure Firewall:
### 4.1. Cho phép truy cập từ xa qua cổng chỉ định
- Vào **Windows Defender Firewall with Advanced Security**
- Chọn **Inbound Rules**, kích vào **New Rule**
![image](https://github.com/user-attachments/assets/e97a30d9-0295-4219-a229-2d8cab654990)

- Áp dụng rule cho cổng 151:
![image](https://github.com/user-attachments/assets/a336cfe1-9456-4548-9459-33a076dc12e5)

- Đặt tên cho rule và xác nhận:
![image](https://github.com/user-attachments/assets/d0dfe3f5-5c21-4d64-80ae-694238518a4d)

## 5. Allow & Block IP remote:
## 5.1. Chọn Rule vừa cấu hình ở phần 4:
- General -> Action -> Allow the connection
- Scope -> Remote IP Address -> Add
![image](https://github.com/user-attachments/assets/a61ee033-73cf-436d-8ac0-6736bfcc9185)
- Nhấn OK -> Apply để xác nhận rule
- Block IP: Allow the connection -> Block the connection
- Dùng Remote Desktop Connection để truy cập từ xa
- Vì đã áp dụng luật chặn IP nên ta không thể truy cập từ xa
![image](https://github.com/user-attachments/assets/f6beb801-39b3-4ccd-9712-e6f44fcada6b)

## 6. Đặt hostname:
### 6.1. Sử dụng Windows Settings:
- Mở **Settings** bằng cách nhấn *Window I*, chọn `System`:
![image](https://github.com/user-attachments/assets/877a6c98-f69d-4ed3-9d92-c4ab4a8659d8)
- Chọn About và nhấn vào Rename this PC:
![image](https://github.com/user-attachments/assets/3a0fe44d-fa91-4301-bf51-5b246ebe73ea)
- Khởi động lại máy tính để áp dụng các thay đổi

### 6.2. Sử dụng System Properties:
- Nhấn Window + R, gõ sysdm.cpl
- Trong tab Computer Name, chọn Change
![image](https://github.com/user-attachments/assets/eb8e1f3c-b1c1-40e5-8659-5f4b2c61bbe1)

