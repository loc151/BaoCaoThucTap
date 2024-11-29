# Network File System (NFS)
Trong Linux, **NFS** là một phần mềm cung cấp khả năng chia sẻ tệp tin và thư mục giữa các máy tính trong một mạng. Đây là cách tuyệt vời để chia sẻ tài nguyên lưu trữ giữa các máy chủ và các máy khách trong mạng nội bộ hoặc qua Internet. NFS cho phép các máy khách truy cập và làm việc trên tệp tin từ xa như chúng được lưu trữ trên máy local.

Lợi ích của NFS:
- **Chia sẻ tập tin và dữ liệu**: NFS cho phép chia sẻ tệp tin và thư mục trên mạng, giúp các máy tính trong mạng truy cập và sử dụng dữ liệu từ máy chủ NFS một cách dễ dàng.

- **Truy cập từ xa và đồng nhất**: Cho phép người dùng truy cập dữ liệu từ xa một cách thuận tiện và đồng nhất. Người dùng có thể truy cập tệp tin từ bất kỳ máy tính nào trong mạng mà không cần phải lưu trữ cục bộ.

- **Tối ưu hiệu suất**: NFS có thể cải thiện hiệu suất truy cập tệp tin trong mạng nội bộ, giúp giảm thời gian truy cập và truyền dữ liệu so với việc sử dụng các phương thức khác như FTP.

- **Quản lý dữ liệu tập trung**: Cho phép quản lý và duy trì tập tin, thư mục tập trung trên máy chủ NFS, giúp dễ dàng thực hiện sao lưu, phục hồi và quản lý dữ liệu.

- **Bảo mật và kiểm soát truy cập**: NFS cung cấp cơ chế kiểm soát truy cập dựa trên quyền hạn, cho phép người quản trị xác định ai có quyền truy cập vào những dữ liệu cụ thể.

- **Tính linh hoạt và mở rộng**: Dễ dàng mở rộng hệ thống bằng cách thêm các máy chủ NFS mới hoặc mở rộng dung lượng lưu trữ mà không gây ảnh hưởng đến sự liên tục của dịch vụ.

## Chuẩn bị: 
- Hai máy ảo cài đặt Ubuntu Server 22.04 kết nối thông qua mạng nội bộ
- Máy ảo cài NFS Server sẽ được gọi là máy chủ.
- Máy ảo cài NFS Client sẽ được gọi là máy trạm.

### Các cài đặt dịch vụ NFS trên server**
- **Bước 1**: Cài đặt NFS Server:
```
sudo apt update
sudo apt install nfs-kernel-server
```

- **Bước 2**:
  - Tạo thư mục chia sẻ: `sudo mkdir /mnt/nfs -p`
  - Loại bỏ tất cả phân quyền cho thư mục này để các máy trạm có thể truy cập và tạo file:
  ```
  sudo chown nobody:nogroup /mnt/nfs/
  sudo chmod 777 /mnt/nfs/
  ```
  
- **Bước 3**: Cấu hình NFS Server
- Mở file `/etc/exports` bằng trình soạn thảo văn bản như nano hoặc vi: `nano /etc/exports`
- Thêm dòng sau vào cuối file **exports** (thay thế địa chỉ IP hoặc dải IP của client cụ thể và cấp quyền truy cập): `/path/to/your/folder client_IP(rw,sync,no_root_squash)`
- Trong đó:
  - **/path/to/your/folder** là đường dẫn đến thư mục bạn muốn chia sẻ.
  - **client_IP** là địa chỉ IP hoặc dải IP của máy client được phép truy cập.
  - **rw** cho phép ghi và đọc
  - **ro** cho phép đọc nhưng không cho chỉnh sửa
  - **sync** đồng bộ dữ liệu
  - **no_root_squash** cho phép người dùng root trên client có quyền root trên server
  - **no_subtree_check** tắt tính năng subtree checking.

![image](https://github.com/user-attachments/assets/d49738f9-753b-449d-837d-1ac1a23d07cd)

- **Bước 4**: Khởi động dịch vụ NFS và Firewall
```sh
sudo exportfs -a
sudo systemctl restart nfs-kernel-server
```

### Kết nối NFS Share trên máy trạm:
- **Bước 1**: Cài đặt NFS client:
```
sudo apt update
sudo apt install nfs-common
```

- **Bước 2**: Tạp thư mục `mount` để kết nối với NFS Share trên máy chủ: `sudo mkdir /mnt/nfs_client`

- **Bước 3**: Kết nối với NFS Share trên máy chủ và mount vào thư mục vừa tạo trên máy trạm:
`sudo mount server_ip:/mnt/nfs  /mnt/nfs_client`

### Kết quả:
- Tại máy trạm: Tạo thử 1 tệp tin tại thư mục `/mnt/nfs_client`:
```
cd /mnt/nfs_client
touch anhldl.txt
```
![image](https://github.com/user-attachments/assets/42ecbce8-21ad-477a-8748-97e7eecb2ec9)

- Tại máy chủ: Kiểm tra thư mục `/mnt/nfs` có xuất hiện tệp tin vừa tạo không:
![image](https://github.com/user-attachments/assets/ca90f71e-35ef-4c68-a483-0971353d772a)

- Nếu tệp tin vừa tạo đã có tại máy chủ tức là kết nối NFS hoạt động thành công.

### Tuỳ chọn: Tự động kết nối khi khởi động:
- Để máy trạm tự động kết nối vào ổ đĩa mạng NFS mỗi khi khởi động, chỉnh sửa file `/etc/fstab`
- Tại file `/etc/fstab`, thêm câu lệnh sau và lưu lại: `server_ip:/mnt/nfs/  /mnt/nfs_client   nfs auto,nofail,noatime,nolock,intr,tcp,actimeo=1800 0 0`
- Giải thích:
  - `auto`: Tự động mount khi hệ thống khởi động
  - `nofail`: Không gây lỗi nếu không thể mount tại thời điểm khởi động.
  - `noatime`: Không cập nhật thời gian truy cập tệp, giúp cải thiện hiệu suất.
  - `nolock`: Không sử dụng khoá NFS
  - `intr`: Cho phép ngắt kết nối khi có tín hiệu ngắt
  - `tcp`: Sử dụng giao thức TCP để truyền dữ liệu
  - `actimeo=1800`: Thiết lập thời gian cache thuộc tính tệp là 1800 giây
- Khởi động lại máy trạm, ổ đĩa mạng sẽ được tự động kết nối vào thư mục `/mnt/nfs_client`
