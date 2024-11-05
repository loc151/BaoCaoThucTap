#  Thông tin về VM
## Nơi lưu trữ máy ảo:
- Trong KVM (Kernel-based Virtual Machine), các máy ảo thường được lưu trữ trong thư mục `/var/lib/libvirt/images/`.
- Đây là nơi mặc định mà KVM sử dụng để lưu trữ các tệp hình ảnh đĩa của máy ảo
- Sử dụng lệnh sau để xem các file máy ảo đang được lưu trữ
```
cd /var/lib/libvirt/images
sudo ls
```

![image](https://github.com/user-attachments/assets/f790407e-0b63-434e-9834-6e643d68c767)

- Kiểm tra vị trí lưu trữ của máy ảo cụ thể, sử dụng các lệnh sau:
```
virsh list --all
virsh domblklist <tên_máy_ảo>
```

- Lệnh `virsh` dùng để liệt kê các tệp hình ảnh đĩa, vị trí lưu trữ và xem thông tin chi tiết về chúng:

![image](https://github.com/user-attachments/assets/1aab543f-aa05-4310-8723-40daae4b312c)

- Trong đó:
|So sánh|vda|sda|
|:---|:---|:---|
|Khái niệm|Thiết bị lưu trữ ảo (virtual disk) được sử dụng trong các môi trường ảo hóa|Thiết bị lưu trữ vật lý (physical disk) hoặc thiết bị lưu trữ ảo sử dụng giao diện SCSI|
|Giao diện|Sử dụng giao diện Virtio, một giao diện ảo hóa hiệu suất cao được thiết kế để giảm thiểu chi phí ảo hóa và tăng hiệu suất I/O.|Sử dụng giao diện SCSI, một giao diện phổ biến cho các thiết bị lưu trữ như ổ cứng và SSD|
|Hiệu suất|Cao hơn|Thấp hơn|
|Tính tương thích|Thấp hơn|Cao hơn|

## Nội dung của thư mục máy ảo: 
- **Tệp hình ảnh đĩa (Disk Image Files)**: Đây là các tệp `.qcow2` hoặc `.img` chứa hệ điều hành và dữ liệu của máy ảo. Chúng đóng vai trò như ổ cứng ảo của máy ảo.

- **Tệp cấu hình (Configuration Files)**: Các tệp .xml chứa thông tin cấu hình của máy ảo, bao gồm tài nguyên phần cứng, mạng, và các thiết lập khác. Chúng giúp KVM biết cách khởi động và quản lý máy ảo.
  - Để xem các tệp cấu hình của các máy ảo, vào thư mục sau:
```
cd /etc/libvirt/qemu/
ls
```

![image](https://github.com/user-attachments/assets/e4cf1ae9-9308-4730-8019-ef8c3b17b0da)

- **Tệp nhật ký (Log Files)**: Các tệp nhật ký ghi lại hoạt động của máy ảo, giúp theo dõi và khắc phục sự cố. Chúng thường có định dạng .log.
  - Để xem được tệp nhật ký của các máy ảo, vào thư mục sau:
```
cd /var/log/libvirt/qemu
ls
```

![image](https://github.com/user-attachments/assets/4bf57fcb-9ca2-4bba-8a96-80945a5edeef)

## Chi tiết nội dung của các tệp:
### Tệp cấu hình máy ảo trong KVM thường chứa các thông tin sau:
- Tài nguyên phần cứng: Bao gồm số lượng CPU, dung lượng RAM, và các thiết bị lưu trữ.
- Mạng: Cấu hình các giao diện mạng, địa chỉ IP, và các thiết lập liên quan đến mạng.
- Thiết lập khởi động: Thông tin về thứ tự khởi động, thiết bị khởi động, và các tùy chọn khởi động khác.
- Thiết lập lưu trữ: Đường dẫn đến các tệp ảnh đĩa và các thiết lập liên quan đến lưu trữ.
- Thiết lập khác: Các thiết lập bổ sung như thiết bị USB, thiết bị âm thanh, và các thiết bị ngoại vi khác.

### Tệp nhật ký (log files) của máy ảo trong KVM chứa các thông tin sau:
- Sự kiện hệ thống: Ghi lại các sự kiện quan trọng như khởi động, tắt máy, và các thay đổi cấu hình.

- Lỗi và cảnh báo: Ghi lại các lỗi và cảnh báo xảy ra trong quá trình hoạt động của máy ảo.

- Hoạt động của máy ảo: Ghi lại các hoạt động như truy cập đĩa, sử dụng CPU, và các hoạt động mạng.

- Thông tin khắc phục sự cố: Cung cấp thông tin chi tiết để giúp khắc phục sự cố và tối ưu hóa hiệu suất của máy ảo.
