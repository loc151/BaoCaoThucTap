# UUID (Universally Unique Identifier)
- **UUID** là một chuỗi số được sử dụng để định danh duy nhất một đối tượng hoặc thực thể. Nó được thiết kế để đảm bảo tính duy nhất trên các hệ thống khác nhau mà không cần sự tương tác hay quản lý tập trung.
- Bạn có thể sử dụng uuid để đảm bảo rằng một ổ đĩa được nhận dạng duy nhất trên toàn cầu trong **/etc/fstab**. Tên thiết bị có thể thay đổi tùy thuộc vào thiết bị đĩa có mặt khi khởi động, nhưng uuid không bao giờ thay đổi.

UUID thường được sử dụng trong nhiều ngữ cảnh khác nhau, bao gồm:
- **Hệ thống tệp và hệ thống lưu trữ**: Trong hệ điều hành, UUID thường được sử dụng để định danh duy nhất các phân vùng đĩa, thiết bị lưu trữ hoặc các tệp tin. Điều này giúp tránh xung đột định danh khi di chuyển hoặc sao chép dữ liệu giữa các hệ thống hoặc trong một hệ thống lớn.
- **Mạng và giao thức**: Trong mạng, UUID có thể được sử dụng để định danh các nguồn tài nguyên như máy chủ, dịch vụ hoặc các thiết bị khác nhau.
- **Ứng dụng và phần mềm**: Trong phần mềm, UUID thường được sử dụng như một cách để đảm bảo mỗi đối tượng được tạo ra hoặc được định danh (ví dụ: ID của một bản ghi trong cơ sở dữ liệu).

## 1. blkid:
Lệnh `blkid` hiển thị thông tin về các thiết bị khối, bao gồm UUID: `sudo blkid`
![image](https://github.com/user-attachments/assets/6f516d5c-4bf1-4654-a287-193a6fb16d90)

## 2. lsblk: 
- Lệnh `lsblk` với tùy chọn `-f` sẽ hiển thị thông tin về hệ thống tệp và UUID của các phân vùng: `lsblk -f`
![image](https://github.com/user-attachments/assets/ec4fe0dc-ddfe-40ed-ac89-ecd8617ff58d)

## 3. tune2fs:
- Lệnh `tune2fs` có thể được sử dụng để hiển thị UUID của các phân vùng ext2/ext3/ext4:
![Uploading image.png…]()
