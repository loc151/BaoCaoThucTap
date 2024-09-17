## 1. Khởi động lại hệ thống và vào chế độ GRUB:

![image](https://github.com/user-attachments/assets/ab2ba74a-c884-40e1-a268-6a438b30ecee)

## 2. Khi màn hình GRUB xuất hiện, chọn mục khởi động và nhấn phím "e" để chỉnh sửa:

![image](https://github.com/user-attachments/assets/375cc87a-76da-4378-a43e-07c4b2dd00ef)

## 3. Chỉnh sửa dòng khởi động:
- Tìm dòng bắt đầu bằng `linux`
- Sửa `ro` thành `rw` và thêm rd.break vào cuối dòng.

![image](https://github.com/user-attachments/assets/4b362aaf-6e5b-47ce-a6e6-812e28f218f7)


## 4. Khởi động vào Emergency Mode:
- Nhấn `Ctrl + X` hoặc `F10` để khởi động với các thông số đã sửa đổi.
- Hệ thống sẽ khởi động vào chế độ khẩn cấp và ta sẽ nhận được dấu nhắc shell.

![image](https://github.com/user-attachments/assets/ddc29ec8-8d74-4d4e-9e65-19486e9e5d50)


## 5. Chuyển đổi môi trường root:
```
chroot /sysroot
```

- Nếu ở bước 3 không sửa `ro` thành `rw` thì cần remount hệ thống với quyền ghi trước khi thực hiện bước 5:
```
mount -o remount, rw /sysroot
```

## 6. Đặt lại mật khẩu root: 
- Sử dụng lệnh `passwd` để đặt lại mặt khẩu root
```
passwd
```
- Nhập mật khẩu mới và xác nhận:

![image](https://github.com/user-attachments/assets/c853e386-c032-4968-9592-e2db5e053266)

## 7. Cập nhật SELinux: 
- Tạo file để SELinux cập nhật các thông số:
```
touch /.autorelabel
```
## 8. Thoát và khởi động lại hệ thống:
- Thoát khỏi chroot
```
exit
```

- Khởi động lại hệ thống:
```
reboot
```

![image](https://github.com/user-attachments/assets/e3d95e14-9d53-41c1-9f16-f4146e759a90)


## 9. Sau khi hệ thống được khởi động lại, ta cần phải đăng nhập root với mật khẩu mới 
![image](https://github.com/user-attachments/assets/d4b544b1-7418-4d92-819c-f73f4c263caa)




