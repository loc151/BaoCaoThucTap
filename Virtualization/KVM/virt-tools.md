# Virt-tools 

# Tìm hiểu một số lệnh cơ bản với virt-tools
- Cài đặt virt-tool
```sh
yum -y install libguestfs-tools virt-top           // Red Hat
hoặc
sudo apt-get install libguestfs-tools virt-top     // Debian
```

## Một số lệnh cơ bản
### Hiển thị cấu trúc một thư mục nào đó trong một vm
```sh
virt-ls -l -d <tên_máy_ảo> /root 
```

![image](https://github.com/user-attachments/assets/62fbcb75-3375-453a-ad95-0ce91662bbc3)

### Xem nội dung file trong vm
```sh
virt-cat -d <tên_máy_ảo> /etc/passwd 
```

![image](https://github.com/user-attachments/assets/74c141ca-4f43-402b-bcc2-769f332c3b61)

### Edit file trong vm
```sh
virt-edit -d <tên_máy_ảo> /etc/fstab
```

### Hiển thị dung lượng disk vm
```sh
virt-df -d <tên_máy_ảo>
```

![image](https://github.com/user-attachments/assets/1fdff375-5831-4b39-9527-d5833a501eb4)


### Hiển thị trạng thái của các máy ảo
```sh
virt-top
```

![image](https://github.com/user-attachments/assets/3d9f7368-742b-4267-8193-aede4808128e)

- Giải thích:
    - `ID`: ID của máy ảo, được sử dụng để định danh duy nhất mỗi máy ảo đang chạy
    - `S`: Trạng thái của máy ảo: R (Running), P (Paused) 
    - `RDRQ`: Read Requests mà máy ảo đã thực hiện
    - `WRRQ`: Write Requests mà máy ảo đã thực hiện
    - `RXBY`: Số lượng byte dữ liệu nhận được qua mạng (Received Bytes)
    - `TXBY`: Số lượng byte dữ liệu gửi đi qua mạng (Transmitted Bytes)
    - `%CPU`: Tỉ lệ phần trăm CPU mà máy ảo đang sử dụng
    - `%MEM`: Tỉ lệ phần trăm bộ nhớ mà máy ảo đang sử dụng
    - `TIME`: Thời gian CPU đã sử dụng bởi máy ảo
    - `NAME`: Tên của máy ảo

## Giải thích các câu lệnh:
- `virt-ls`: Liệt kê các tệp và thư mục trong máy ảo
- `virt-cat`: Xem nội dung của 1 tệp trong máy ảo mà không cần khởi động máy ảo đó
- `virt-df`: Hiển thị thông tin về dung lượng đĩa của các máy ảo
- `virt-edit`: Chỉnh sửa tệp trong máy ảo. Cần tắt máy ảo trước khi chỉnh sửa để tránh xung đột và lỗi
- `virt-top`: Hiển thị thông tin về trạng thái các máy ảo
- `-l`: Hiển thị thông tin chi tiết về các tệp và thư mục, bao gồm quyền truy cập, kích thước, và thời gian sửa đổi cuối cùng
- `-d`: Chỉ định tên của máy ảo muốn liệt kê các tệp và thư mục
