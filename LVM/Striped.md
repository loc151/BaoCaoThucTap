# Striped Logical Volumes
---
## Giới thiệu:
Khi dữ liệu được ghi xuống LVM logical volume, File system sẽ đặt data nằm suốt các physical volume.

Có thể kiếm soát cách data được ghi xuống physical volumes băng cách tạo striped logical volume.

Với khối lượng đọc ghi lớn, khi sử dụng phương pháp này hiệu năng data IO sẽ được nâng cao.
Striped Logical nâng cao hiệu năng = ghi data đến 1 số các physical volumes chỉ đinh trước - với striping, IO thực hiện song song.

### Mô hình:
![image](https://github.com/user-attachments/assets/6cabaa69-9598-4f05-8d2c-2ddb02af2172)

### Cách ghi dữ liệu:
![image](https://github.com/user-attachments/assets/1cda8ed2-2a0f-41d2-b305-8e809d5d1dee)

## Cấu hình:
### Tạo volume group:
__Kiểm tra cấu hình hiện tại__
```
pvs
vgs
lvs
```
![image](https://github.com/user-attachments/assets/724c728c-06a0-4e5d-8e72-bf96eb164749)

#### Tạo VG
```
vgcreate vg-strip /dev/sdb1 /dev/sdc1 /dev/sdd1
```
#### Kiểm tra thông tin VG vừa tạo
```
vgdisplay vg-strip -v
```
![image](https://github.com/user-attachments/assets/eb231b93-c1a6-473b-99c0-6c924d2377b6)

### Tạo LV striped
```
lvcreate -L 2G -n lv_strp1 -i3 vg-strip
```
> -L – logical volume size

> -n – logical volume name

> -i – stripes <= số Disk

#### Kiểm tra LV strip vừa tạo
```
lvdisplay vg-strip/lv_strp1 -m
```
![image](https://github.com/user-attachments/assets/397fb3f5-6494-42ad-b5c6-783258910a03)

### Kiểm chứng
#### Định dạng FS cho LV vừa tạo
```
mkfs.ext4 /dev/vg-strip/lv_strp1
```
![image](https://github.com/user-attachments/assets/f6578466-928d-4e28-926a-3b9a92f3e1e8)

#### Mount vào OS
```
mount /dev/vg-strip/lv_strp1 /data-store/
```
> __Đưa dữ liệu test và xem cơ chế phân tán dữ liệu__

#### Kiểm tra đối chiếu
```
pvs
```
![image](https://github.com/user-attachments/assets/7dc87c1f-cf95-4235-b6d4-65a0f95163a7)

> Phân vùng 2GB được chia đều đến các PV __sdb1 sdc1 sdd1__
