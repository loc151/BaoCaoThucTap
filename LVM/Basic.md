# Những câu lệnh cơ bản cấu hình LVM

## Phần 1: Tạo Logical Volume:
### Bước 1: Kiểm tra các ổ cứng hiện tại: `lsblk`
![image](https://github.com/user-attachments/assets/ed7c4b6a-e729-49ea-a098-cdbe8267bd44)

### Bước 2: Tạo Partition: 
```
fdisk /dev/sdb
```
![image](https://github.com/user-attachments/assets/835cbb3a-2077-4048-ba19-3892358d7740)

- Các thao tác:
  - `m`: Mở bảng trợ giúp và xem các tuỳ chọn
  - `n`: Bắt đầu tạo partition
  - `p`: Tạo partition primary
  - Chọn 1 để tạo partition primary 1
  - Tại First sector (2048-20971519, default 2048) để mặc định
  - Tại Last sector, +sectors or +size{K,M,G} (2048-20971519, default 20971519) chọn +10G để partition tạo ra có dung lượng 10 G
  - `w`: Lưu lại cấu hình và thoát
![image](https://github.com/user-attachments/assets/f5e60d5c-853f-4068-852f-f67f705c8e6f)

- Các thao tác:
  - `t`: Thay đổi định dạng partition
  - `8e`: đổi định dạng sang LVM
![image](https://github.com/user-attachments/assets/a15bcf3b-5e6b-47cd-84ae-f414cb958822)

- Tương tự các bước với **sdc**:
![image](https://github.com/user-attachments/assets/98d41d72-d9b0-48b1-8f01-7beb95d0b304)

### Bước 3: Tạo Physical Volume:
- Tạo Physical Volume là /dev/sdb1 với lệnh sau:
```
pvcreate /dev/sdb1
pvcreate /dev/sdc1
```
![image](https://github.com/user-attachments/assets/8feedb31-649b-44da-9a3c-3b01264b6d7a)

### Bước 4: Tạo Volume Group
- Nhóm các Physical Volume thành 1 Volume Group bằng:
```shell
vgcreate vg-test1 /dev/sdb1 /dev/sdc1
```
> vg-test1: tên của Volume Group

- Kiểm tra lại các Volume Group đã tạo:
```
vgs
vgdisplay
```
![image](https://github.com/user-attachments/assets/4add3fb8-1a8b-4809-907e-a96c279346b2)

### Bước 5: Tạo Logical Volume
- Từ 1 Volume Group, tạo ra các **Logical Volume** bằng lệnh sau:
```
# lvcreate -L 10G -n lv-test1 vg-test1
```
> **`-L`**: Chỉ dung lượng của Logical Volume 
> **`-n`**: Chỉ tên của Logical Volume
> **`lv-test1`**: Tên của Logical Volume
> **`vg-test1`**: Volume Group vừa mới tạo

- Kiểm tra cấu hình vừa tạo:
```
lvs
lvdisplay
```
![image](https://github.com/user-attachments/assets/8a86d6f1-628f-425d-ae83-8056b0660d75)

### Bước 6: Định dạng Logical Volume:
```
mkfs -t ext4 /dev/vg-test1/lv-test1
```
![image](https://github.com/user-attachments/assets/68eabb72-f314-48c8-ae6d-9bae8e8612ee)

### Bước 7: Mount và sử dụng
- Tạo thư mục *mount*: `mkdir test1`
- Tiến hành mount Logical Volume  lv-test1 vào thư mục test1: `mount /dev/vg-test1/lv-test1 test1`
- Kiểm tra lại dung lượng: `df -h`
![image](https://github.com/user-attachments/assets/774d28c3-95b6-4d1a-b581-575f25c86e14)

## Phần 2: Thay đổi dung lượng Logical Volume trên LVM:
### Bước 1: Kiểm tra toàn bộ:
```
vgs
lvs
pvs
```

![image](https://github.com/user-attachments/assets/224774c7-f8e0-44ed-8f3e-e12b8f4d00c5)

### Bước 2: Kiểm tra dung lượng Volume Group:
- Trước khi tăng, cần kiểm tra xem Volume Group còn dư dung lượng để kéo dãn: `vgdisplay`

![image](https://github.com/user-attachments/assets/7a3fdaff-73fd-408e-8a78-43cb82538492)

### Bước 3: Tăng kích thước Logical Volume: 
- Để tăng kích thước Logical Volume, sử dụng câu lệnh:
```
lvextend -L +5G /dev/vg-test1/lv-test1
```

- Kiểm tra lại: `lvs`

> Kích thước cho Logical Volume thì Logical Volume đã được tăng nhưng file system trên volume này vẫn chưa thay đổi, sử dụng lệnh:
```
resize2fs /dev/vg-test1/lv-test1
```
![image](https://github.com/user-attachments/assets/8d4a33c1-8a00-4e08-8c9f-a34fb97ce7e0)

### Bước 4: Giảm kích thước Logical Volume:
- Để giảm kích thước Logical Volume, sử dụng câu lệnh:
```
lvreduce -L 5G /dev/vg-test1/lv-test1
```
![image](https://github.com/user-attachments/assets/8f151f25-973e-4012-8f11-b24965d1db0f)

- Tiến hành format lại Logical Volume:
```
mkfs.ext4 /dev/vg-test1/lv-test1
```

## Phần 3: Thay đổi dung lượng Volume Group trên LVM:
> Việc thay đổi kích thước của Volume Group chính là việc nhóm thêm Physical Volume hay thu hồi Physical Volume ra khỏi Volume Group

### Bước 1: Kiểm tra lại các partition và Volume Group:
```
vgs
lsblk
```
![image](https://github.com/user-attachments/assets/27ee0a9c-3fc7-44a3-b1af-8cc1a256a531)

### Bước 2: Nhóm thêm partition vào Volume Group:
```
vgextend /dev/vg-test1 /dev/sdc2
```

![image](https://github.com/user-attachments/assets/cc073430-187d-4e06-9d2c-d5ad3a08e25b)

### Bước 3: Cắt Physical Volume ra khỏi Volume Group:
```
vgreduce /dev/vg-test1 /dev/sdc2
```
![image](https://github.com/user-attachments/assets/424f88ad-bfc7-421d-8107-d9a5f5eac2a8)

## Phần 4: Xóa Logical Volume, Volume Group, Physical Volume:
### Bước 1: Unmount Logical Volume:
```
umount /dev/vg-test1/lv-test1
```

### Bước 2: Xoá Logical Volume:
```
lvremove /dev/vg-test1/lv-test1
```

### Bước 3: Xoá Logical Group:
```
vgremove /dev/vg-test1
```
> Trước khi xóa Volume Group, chúng ta phải xóa hết Logical Volume

### Bước 4: Xoá Physical Volume: 
```
pvremove /dev/sdc2
```

![image](https://github.com/user-attachments/assets/8d4ba348-4ad6-490c-9d3e-bc34c2ab577d)
