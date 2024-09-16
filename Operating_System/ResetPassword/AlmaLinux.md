## 1. Khởi động lại hệ thống và vào chế độ GRUB:

![image](https://github.com/user-attachments/assets/3b834eb2-adfa-4704-b7a3-8f8fae421d9b)

## 2. Khi màn hình GRUB xuất hiện, chọn mục khởi động và nhấn phím "e" để chỉnh sửa:

![image](https://github.com/user-attachments/assets/5a3edbec-9831-4231-8d85-bc408cb74641)

## 3. Chỉnh sửa dòng khởi động:
- Tìm dòng bắt đầu bằng `linux`
- Sửa `ro` thành `rw` và thêm rd.break vào cuối dòng.

![image](https://github.com/user-attachments/assets/880f3edd-5ea2-4eca-81a1-73ad19f7264d)

## 4. Khởi động vào Emergency Mode:
- Nhấn `Ctrl + X` hoặc `F10` để khởi động với các thông số đã sửa đổi.
- Hệ thống sẽ khởi động vào chế độ khẩn cấp và ta sẽ nhận được dấu nhắc shell.

![image](https://github.com/user-attachments/assets/bd25143a-6d9f-49a4-9039-687481dfd08a)

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

![image](https://github.com/user-attachments/assets/80b301e1-7615-4bb7-909f-e39c531e8b54)

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

![image](https://github.com/user-attachments/assets/ca259788-7d26-4654-8756-dd6b080ca05e)

## 9. Sau khi hệ thống được khởi động lại, ta cần phải đăng nhập root với mật khẩu mới 
![image](https://github.com/user-attachments/assets/fe20bbe7-cad0-459f-ab9a-1b83d2dfd2c0)

## 10. Dùng MobaXstrem để truy cập từ xa SSH:
![image](https://github.com/user-attachments/assets/a00dc83e-0a97-4073-8e3e-ec3d18c3cba7)


