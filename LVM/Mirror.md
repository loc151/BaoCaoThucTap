# Mirrored Logical Volume
---
## Giới thiệu
Mirrored Logical Volume duy trì bản sao dữ liệu giống nhau trên thiết bị khác nhau. Khi data được ghi tới 1 device, nó cũng sẽ được ghi tới 1 thiết bị khác (mirroring the data).
Phương pháp cung cấp tính bảo vệ dữ liệu khi thiết bị lỗi.

LVM hỗ trợ mirrored volumes. Khi ta tạo mirrored logical volume, LVM sẽ chắc chắn ghi data tới vị trí mirrored tại thiết bị khác.
Với LVM, ta có thể tạo mirrored logical volume với nhiều mirrors.

LVM mirror duy trì lượng log nhỏ, sử dụng để theo dõi phân vùng được đồng bộ với mirror (1 hoặc nhiều).

### Tính năng
- Chuyển logical volumes từ 1 disk tới 1 disk khác.
- Ta có thể sử dụng bất kỳ loại disk nào như SATA, SSD, SAS, SAN storage iSCSI hoặc FC.
- Migrate disk tránh lỗi, khi xảy ra lỗi sẽ không có downtime.

### Mô hình
![image](https://github.com/user-attachments/assets/8f6a7157-649c-4fa6-a3a6-4cb99e3cbb8e)

## Cấu hình
### Bước 1: Tạo ổ đĩa, định dạng, dữ liệu test tính năng mirrors
__Kiểm tra thông số ban đầu__
```
# pvs
# vgs
# lvs
```
![image](https://github.com/user-attachments/assets/97f7e7ce-a18b-48ec-8f63-7a61026ac009)

> Ta sẽ sử dụng 2 ổ __sdc1 và sdd1__ để xây dựng lab.

> __sdc1__ - ổ chính

> __sdd1__ - ổ mirror

__Tạo ổ đĩa__
```
vgcreate vg-group /dev/sdc1
```
![image](https://github.com/user-attachments/assets/7870326a-220a-4f2d-8f30-233cafd7fc1a)

__Tạo LV, định dạng__
```
lvcreate -L 1G -n lv_target vg-group
mkfs.ext4 /dev/vg-group/lv_target
```
![image](https://github.com/user-attachments/assets/ce55154e-8f78-4ba2-9951-7bae81efc974)


__Mount và tạo dữ liệu test__
```
mount /dev/vg-group/lv_target /data-store/data/
ls /data-store/data/
```
![image](https://github.com/user-attachments/assets/944e3fd9-298d-4cfd-b11e-535c5f508266)

__Kiểm tra lại thông tin lv, vg vừa tạo__
```
lvs
vgs -o+devices
```
> Ở đây __/dev/sdc1__ đang giữ dữ liệu

![image](https://github.com/user-attachments/assets/cfcb2623-8c0f-408d-93d9-bd9b80e2abd7)


### Bước 2: Thêm, tạo ổ đĩa mới (Dùng cho hoạt động mirror)
__Sử dụng ổ /dev/sdd1 làm ổ Mirror__
```
pvs
```
![image](https://github.com/user-attachments/assets/998bf133-9e4b-4425-9711-84a94cc492b8)

__Mở rộng VG bằng ổ mới (Mirror disk)__
```
vgextend vg-group /dev/sdd1
vgdisplay vg-group -v
```
![image](https://github.com/user-attachments/assets/80526928-fdb8-43f8-9f48-c18f58031366)

__Kiểm tra ổ đang map tới LV__
```
lvs -o+devices
dmsetup deps /dev/vg-group/lv_target
```
> `dmsetup deps`: Hiển thị các phụ thuộc của 1 thiết bị mapper cụ thể. Nghĩa là nó sẽ liệt kê các thiết bị vật lý mà thiết bị mapper phụ thuộc vào

> Ở đây (8,33) là ảnh xạ LV tới /dev/sdc1

![image](https://github.com/user-attachments/assets/5656001a-6689-4a06-8cf3-801b714a3cf0)

### Bước 3: Cấu hình LVM Mirroring
__Cấu hình migrate data từ LV cũ tới LV Mirror__
```
lvconvert -m 1 /dev/vg-group/lv_target /dev/sdd1
```
> -m = mirror

> 1 = Thêm single mirror

![image](https://github.com/user-attachments/assets/a4f50600-d472-426d-85b6-68a8ba98c28d)

__Kiểm tra cấu hình sau khi add Mirror__
```
lvs -o+devices
```
![image](https://github.com/user-attachments/assets/03751ae3-c830-4cab-be74-f3455c670140)

__Xóa ổ đĩa cũ (LV old)__
```
lvconvert -m 0 /dev/vg-group/lv_target /dev/sdc1
```
![image](https://github.com/user-attachments/assets/1d069b90-4eea-4549-8113-b74727fac712)

__Kiểm tra thông số hiện tại__
```
lvs -o+devices
dmsetup deps /dev/vg-group/lv_target
```
> Tại thời điểm LV ánh xạ sang ổ Mirror (sdd1)

![image](https://github.com/user-attachments/assets/ba86fef8-79fe-4684-8e06-b5435f31cb89)

__Xóa LV cũ ra khỏi VG__
```
vgreduce /dev/vg-group /dev/sdc1
```
> Dữ liệu đã được bảo đảm dù không có ổ sdc1

> Sau khi xóa ổ sdc1 khỏi VG, dữ liệu vẫn còn vì đã migrated từ sdc1 -> sdd1

![image](https://github.com/user-attachments/assets/1d467be6-b057-43ba-b315-31ecbe26b5b4)

__Kiểm tra lại data ban đầu__
```
ls /data-store/data/
```
![image](https://github.com/user-attachments/assets/4cf14da0-5921-4779-ba68-f8b3ce43e59f)

