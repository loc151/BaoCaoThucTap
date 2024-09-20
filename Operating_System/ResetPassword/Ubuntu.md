## Reset Password
### 1. Khởi động lại hệ thống: 
- Khởi động lại hệ thống Ubuntu bằng cách tắt nguồn máy chủ hoặc dùng lệnh `init 6`
- `init 6`: Lệnh được sử dụng để khởi động lại hệ thống trong các hệ điều hành giống Unix, bao gồm cả Linux. Lệnh này yêu cầu hệ thống chuyển sang runlevel 6, tức là runlevel khởi động lại.

### 2. Truy cập vào GRUB Menu: 
- Trong lúc reboot, nhấn vào giữ phím *Shift* để vào giao diện GRUB
![image](https://github.com/user-attachments/assets/f1a71377-d6ca-4e96-917f-b0d7d2bd5cee)

- Chọn **Advanced options for Ubuntu** 
![image](https://github.com/user-attachments/assets/b0d960e9-b8a7-48aa-8ec1-d21f0162851f)

### 3. Khởi động vào Recovery Mode: 
- Nhấn `Ctrl + X` hoặc `F10` để khởi động với các thông số đã sửa đổi.
- Hệ thống sẽ khởi động vào chế độ khẩn cấp và ta sẽ nhận được dấu nhắc shell.

![image](https://github.com/user-attachments/assets/4b4287ed-c210-4b8f-9c8d-6c6c2b834260)

### 5. Gắn lại hệ thống tập tin gốc dưới dạng read-write:
```
mount -o remount,rw /sysroot
```

### 6. Đổi Root thành Sysroot: Đổi môi trường root thành /sysroot:
```
chroot /sysroot
```

### 7. Đặt lại mật khẩu Root:
```
passwd
```
- Nhấn mật khẩu mới và xác nhận

### 8. Cập nhật SELinux Context:
- Tạo tập tin để đảm bảo rằng SELinux được cập nhật vào lần khởi động tới
```
touch /.autorelabel
```

### 9. Thoát và Khởi động lại:
- Thoát môi trường chroot và khởi động lại hệ thống.
```
exit
reboot 
```
![image](https://github.com/user-attachments/assets/ac6daf20-b446-4506-9fac-0237c42c48d6)

## Sau khi hệ thống được khởi động lại, ta cần phải đăng nhập root với mật khẩu mới 

