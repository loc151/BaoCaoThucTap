# Cài đặt VM trên Ubuntu

## Hướng dẫn thêm file ISO từ USB vào Ubuntu để cài đặt máy ảo

1. **Cắm USB vào máy tính**: Đảm bảo server đã nhận được USB khi cắm USB vào cổng.
2. **Xác định tên thiết bị USB**:
- Dùng lệnh sau để liệt kê các thiết bị USB và xác nhận xem server đã nhận USB:

![image](https://github.com/user-attachments/assets/4679f5b5-1f7c-49a3-b020-4557b77a9d68)

- Trường hợp này đang dùng USB của Kingston, và server đã nhận diện được USB này

3. **Mount USB**
- Xác định tên thiết bị USB: nhập lệnh `lsblk`:

![image](https://github.com/user-attachments/assets/fc5cb1a9-318b-4a43-b012-edc4a264cdec)

Lúc này, thiết bị USB xuất hiện với tên **sda1**

- Tạo 1 thư mục để mount USB:
```
sudo mkdir /mnt/usb
```

- Mount USB và thư mục này:
```
sudo mount /dev/sda1 /mnt/usb
```

- Kiểm tra xem các file ISO đã hiển thị hay chưa:

![image](https://github.com/user-attachments/assets/6b5903d0-a438-4ea3-bec3-d623b2f412d6)

- Sao chép file ISO:
```
cp /mnt/usb/yourfile.iso /home/yourusername/
```

Thay `yourfile.iso` bằng tên file ISO và `yourusername` bằng tên người dùng.

![image](https://github.com/user-attachments/assets/0d2c51fb-eafc-4438-aebe-8db2a6f00195)

- Kiểm tra xem file ISO đã hiển thị trong thư mục đích:

![image](https://github.com/user-attachments/assets/670da93b-a3d2-4999-be10-8ae3b5279fcd)

/var/lib/libvirt/images
