## 1. Remote:
### 1.1. Bật Remote Desktop trong Windows Server (2019):
- Ấn vào biểu tượng **Start**, chọn **Remote Desktop Settings**
![image](https://github.com/user-attachments/assets/a2567217-156a-4507-9a7e-22c5a85b7cac)

- Lúc này, **Enable Remote Desktop** đang bị tắt, nhấn vào để bật chế độ này:
![image](https://github.com/user-attachments/assets/5578d18c-3642-464d-a0bf-7fd4dc5e658f)

![image](https://github.com/user-attachments/assets/3afaf544-d6a6-4db7-a6e7-23fc06d5d850)

- Dùng **Remote Desktop Connection** ở máy khác
![image](https://github.com/user-attachments/assets/01c1f270-844f-4717-a233-c958b34e78da)

- Nhập địa chỉ IP của *Windows Server*:
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
