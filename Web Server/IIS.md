# Cài đặt IIS và triển khai website với IIS trên Windows Server
## Cài đặt IIS
- **Bước 1:** Mở **Server Manager -> Add Roles and Features:**
![image](https://github.com/user-attachments/assets/e0f67d4f-4a0a-4482-b55b-c8c740f9d158)

- **Bước 2:** Đến mục **Server Roles**, chọn **Web Server (IIS)**
![image](https://github.com/user-attachments/assets/463d0c78-53bf-47e6-8492-73cd2dd57966)

- **Bước 3:** Chọn các thành phần cần thiết và tiến hành cài đặt IIS:
![image](https://github.com/user-attachments/assets/b5de2551-6d4b-49c8-8783-8f78abccaee6)
- **Bước 4:** Chờ 1 khoảng thời gian và cài đặt thành công:
![image](https://github.com/user-attachments/assets/e466f407-e0eb-4fb6-8372-4bdc84babe5d)

## Kết quả
- **Kiểm tra cài đặt**: Mở trình duyệt web và truy cập `http://localhost` để kiểm tra xem IIS đã được cài đặt thành công chưa
- Nếu hiển thị như ảnh dưới tức là đã cài đặt IIS hoạt động đúng cách:
![image](https://github.com/user-attachments/assets/ae935234-aa5e-4a41-9065-d38dd058800c)
---
### Chỉnh sửa website
- Tạo 1 tệp tin đuôi `.html` tại đường dẫn `/inetpub/wwwroot` để thay đổi nội dung website
![image](https://github.com/user-attachments/assets/ebd0190e-b8ae-4c3d-a7ea-b43c2a50997f)

- Mở tệp `.html`, thêm nội dung và lưu lại
![image](https://github.com/user-attachments/assets/2f432307-5f66-4f6c-9d8e-796c0e34336b)

- Truy cập hoặc reset lại trang `localhost` để kiểm tra kết quả:
![image](https://github.com/user-attachments/assets/d5e2b894-a9ed-48f0-abf1-2cc91b3626ef)

## Tạo thêm website trong IIS:
- **Bước 1:** Thêm thư mục mới để chứa các nội dung của website:
![image](https://github.com/user-attachments/assets/9e965d69-ee4a-404d-91de-57988400f92e)

- **Bước 2:** Vào **Server Manager -> Internet Information Services (IIS) Manager**
![image](https://github.com/user-attachments/assets/c78e3fba-6ac3-438f-bff3-b3e433eb1f81)

- **Bước 3:** Trong **IIS Manager**, nhấp chuột phải vào **Sites** trong bảng điều khiển bên trái và chọn **Add Website**:
![image](https://github.com/user-attachments/assets/4f286a2d-11d5-41f0-8c7c-4ad49b831ac3)

- **Bước 4:** Trong cửa sổ **Add Website**, điền các thông tin như sau:
![image](https://github.com/user-attachments/assets/49c74eae-d918-4ea5-bf9c-6f77341d9760)

- **Bước 5:** Vào tệp tin `hosts` với đường dẫn `C:\Windows\System32\drivers\etc`:
![image](https://github.com/user-attachments/assets/a1df26c6-4627-4148-9f30-2c2920f04f2e)

- **Bước 6:** Thêm địa chỉ *localhost* và tên miền để phân giải DNS:
![image](https://github.com/user-attachments/assets/97187565-c60c-4e97-9383-0d14f06c50e6)

## Kết quả: 
- Truy cập tên miền `anhldl.com` để kiểm tra xem website có hoạt động bình thường hay không:
![image](https://github.com/user-attachments/assets/3b83563a-8deb-442d-b023-5ee794da7cc7)
