# Quản lý thiết bị lưu trữ 
## Các khải niệm cơ bản:
**1. Logical Volume Manager (LVM):**
- Logical Volume Manager (LVM) là một công cụ quản lý phân vùng logic trong hệ điều hành Linux.
- Nó cho phép tạo mới, thay đổi kích thước hoặc xóa bỏ các phân vùng mà không cần phải dừng hệ thống.
- **LVM** rất hữu ích cho việc quản lý các ổ đĩa lớn và linh hoạt trong việc thay đổi kích thước phân vùng khi cần thiết

**2. Tác dụng của LVM:**
- Tạo 1 hoặc nhiều phân vùng logic hoặc phân vùng với toàn bộ đĩa cứng, cho phép thay đổi kích thước volume
- Quản lý Large hard Disk Farms bằng cách cho phép thêm và thay thế đĩa mà không bị ngừng hoạt động và gián đoạn dịch vụ
- Trên các hệ thống nhỏ (như máy tính để bàn), thay vì phải ước tính thời gian cài đặt, phân vùng, LVM cho phép các hệ thống tệp dễ dàng thay đổi kích thước khi cần
- Thực hiện sao lưu nhất quán bằng cách tạo snapshot nhanh các khối một cách vật lý
- Mã hóa nhiều phân vùng vật lý bằng một mật khẩu

**3. Cấu trúc của LVM:**
![image](https://github.com/user-attachments/assets/61511b98-f73d-4b57-8108-cb422c2ed5ff)

## Quản lý phân vùng:
1. `lsblk`: Hiển thị thông tin về các thiết bị lưu trữ và phân vùng:
![image](https://github.com/user-attachments/assets/9736cdba-71aa-4589-8874-168bab33ca7a)

2. `df -h`: Hiển thị dung lượng đĩa đã sử dụng và còn trống:
![image](https://github.com/user-attachments/assets/04c4e608-00fb-4b4f-a3e8-a5cbfef6e640)

3. `du -sh`: Hiển thị dung lượng sử dụng của các tệp và thư mục:
![image](https://github.com/user-attachments/assets/8a895cd5-cb1a-4767-bf26-954cd02e1ac1)

## Lệnh phân vùng và định dạng:
1. **fdisk**:
- Tạo phân vùng:
![image](https://github.com/user-attachments/assets/cd975240-33d5-467d-a104-ad26ed9bfb32)
![image](https://github.com/user-attachments/assets/d80a394b-fd8f-43ec-9641-4d37a029a3d7)

- Xoá phân vùng:
![image](https://github.com/user-attachments/assets/23a4ab50-3ec0-4f5f-8de7-0c4091e50fb0)

2. **lvreize**: Thay đổi cấu hình phân vùng (dành cho LVM):
- Giảm kích thước:
![image](https://github.com/user-attachments/assets/5f416c81-4fbb-4f82-a497-624923eb355f)

- Tăng kích thước:
![image](https://github.com/user-attachments/assets/9a55a470-85c4-4f9f-8a49-1fed32675864)

- Thay đổi kích thước hệ thống tệp sau khi thay đổi kích thước **Logical Volume**:
```
sudo resize2fs /dev/myvg/mylv
```

blkid
![image](https://github.com/user-attachments/assets/bbc1ab37-5a48-471c-8693-1e9f88add10b)

fsck
![image](https://github.com/user-attachments/assets/e86dde35-4542-4886-aeea-89cfd364d61b)

/etc/fstab
![image](https://github.com/user-attachments/assets/77069d33-ae9a-4ed8-80f8-addaf5c2b491)
