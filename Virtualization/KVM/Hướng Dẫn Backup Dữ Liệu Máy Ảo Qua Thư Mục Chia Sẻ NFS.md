# Hướng Dẫn Backup Dữ Liệu Máy Ảo Qua Thư Mục Chia Sẻ NFS
## Giới Thiệu
**NFS (Network File System)** là một giao thức mạng cho phép chia sẻ thư mục và tệp tin giữa các máy tính trong cùng mạng nội bộ. Trong hướng dẫn này, chúng ta sẽ thiết lập NFS để chia sẻ thư mục `nfs_backup`, nhằm mục đích sao lưu máy ảo và dữ liệu quan trọng từ KVM.

## Cấu Hình NFS Chia Sẻ Thư Mục

### Bước 1: Cài Đặt Dịch Vụ NFS
Trước tiên, cần cài đặt dịch vụ NFS trên máy chủ để chia sẻ thư mục `nfs_backup`.

- **Trên Ubuntu/Debian**: Cài đặt dịch vụ NFS bằng lệnh `apt`.

```bash
sudo apt update
sudo apt install nfs-kernel-server -y
```

- **Trên CentOS/RHEL**: Cài đặt dịch vụ NFS bằng lệnh `yum`.

  ```bash
  sudo yum install nfs-utils -y
  ```

### Bước 2: Cấp quyền truy cập cho thư mục
- Tạo thư mục chia sẻ:

```
sudo mkdir -p /mnt/nfs_backup
```

- Sao chép cấu hình máy ảo vào file `/mnt/nfs_backup`

```
sudo cp /etc/libvirt/qemu/<tên_tệp_ảnh_đĩa> /mnt/nfs_backup/
```

- Cấp quyền truy cập cho thư mục để tất cả các máy trong mạng có thể ghi dữ liệu.

```
sudo chown nobody:nogroup /mnt/nfs_backup
sudo chmod 777 /mnt/nfs_backup
```

### Bước 3: Chia Sẻ Thư Mục Qua NFS
- Chỉnh sửa file `/etc/exports` để chia sẻ thư mục `nfs_backup` qua NFS. Dùng lệnh sau: `sudo nano /etc/exports`

- Thêm dòng sau vào cuối file:

```
/mnt/nfs_backup 172.16.2.0/20(rw,sync,no_subtree_check)
```

![image](https://github.com/user-attachments/assets/9fa96ac7-82c9-413e-88ef-a7f03c52f9e9)

- `*`: Cho phép tất cả các địa chỉ IP trong mạng truy cập.
- `rw`: Cho phép quyền đọc và ghi.
- `sync`: Đảm bảo dữ liệu được ghi ngay lập tức vào đĩa.
- `no_subtree_check`: Tắt kiểm tra cây thư mục để cải thiện hiệu năng.

- Sau đó, áp dụng cấu hình chia sẻ: `sudo exportfs -a`

### Bước 4: Khởi Động Lại Dịch Vụ NFS
Khởi động lại dịch vụ NFS để áp dụng cấu hình mới.

- **Trên Ubuntu**:
```
sudo systemctl restart nfs-kernel-server
```
- **Trên CentOS**:
```
sudo systemctl restart nfs
```

## Cấu Hình Backup Với Veeam
Sau khi thư mục `nfs_backup` được chia sẻ thành công qua NFS , có thể sử dụng **Veeam** để quản lý và thực hiện backup.

### Bước 1: Kết Nối Thư Mục Chia Sẻ NFS Với Veeam
1. Trong giao diện Veeam, chọn **Add Repository**.

![image](https://github.com/user-attachments/assets/68c97d86-7b9c-4c9b-8d34-683b04d9cb0f)

2. Chọn loại **NFS** và điền địa chỉ thư mục chia sẻ, ví dụ: `172.16.2.160:/mnt/nfs_backup`.

![image](https://github.com/user-attachments/assets/fa3e824e-e110-4729-9dea-4e9eb4318246)

3. Tiến hành các bước theo hướng dẫn để hoàn tất việc thêm thư mục NFS vào Veeam như một repository lưu trữ.
![Command Prompt](https://github.com/cuongnvvietis/NhanHoa/blob/main/Docs/Picture/KVM/Screenshot_43.png) 
### Bước 2: Tạo File Backup Job
1. Tạo **File Backup Job** mới.
2. Chọn thư mục `/mnt/nfs_backup` từ repository đã thêm làm đối tượng cần backup.
3. Thiết lập các cấu hình cho job backup (ví dụ: lịch trình backup, proxy backup, và cache repository).
### Bước 3: Xác Nhận và Thực Hiện Backup
1. Nhấn **Apply** và sau đó **Finish** để hoàn tất việc cấu hình job backup.
2. Kiểm tra trạng thái của job trong danh sách các công việc backup để đảm bảo quá trình backup đang chạy đúng.

![image](https://github.com/user-attachments/assets/db9450d9-7bad-4100-bc49-bafc1f518e47)

![image](https://github.com/user-attachments/assets/b6b10e70-d457-4966-b624-986a1fd157ba)

## Kết Luận
Với hướng dẫn trên, bạn đã thiết lập thành công chia sẻ thư mục `backup-veeam` qua NFS và tích hợp với Veeam để thực hiện backup dữ liệu của các máy ảo trên KVM. Việc này giúp đảm bảo tính an toàn dữ liệu và dễ dàng khôi phục khi có sự cố.

### Lưu Ý
- Đảm bảo thư mục `/backup-veeam` có quyền truy cập đầy đủ để tránh lỗi ghi dữ liệu khi backup.
- Cần kiểm tra định kỳ việc mount và cấu hình backup để đảm bảo tính liên tục và không bị gián đoạn trong quá trình sao lưu.


**Lỗi: Backup không thành công**
![image](https://github.com/user-attachments/assets/07cdb99b-bd73-4f55-9a5d-3975663e4a36)
