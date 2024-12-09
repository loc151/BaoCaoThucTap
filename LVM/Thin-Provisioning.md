# Thin Provisioning Volume
---
## Giới thiệu
Cung cấp LV động. Tính năng cho phép tạo lv lớn hơn cần thiết mà không lập tức tiêu tốn tài nguyên thực.

Sử dụng thin provisioning, ta có thể quản lý dung lượng còn trống của storage pool (thin pool), cho phép cấp phát tùy ý cho thiết bị khi cần. Có thể tạo ra các thiết bị nằm trong thin pool, sẽ được cấp phát thực sự khi ứng dụng ghi dữ liệu vào LV.

Thin pool có thể mở rộng động, tận dụng tối đa tài nguyên và tối ưu chi phí.

__VD:__
- Có 10 user yêu cầu cấp phát 100gb FS cho app của họ.
- Storage administrator có thể tạo 100gb cho từng người ngay cả khi dung lượng thực tế của storage nhỏ hơn.

> Nếu cung cấp Provisioning nhiều hơn dung lượng hiện có, nó gọi là __Over Provisioning.__

## Cấu trúc:
![image](https://github.com/user-attachments/assets/2b226c33-a220-4db2-a697-5d3c5c2cfe96)

## Bắt đầu
### Tạo VG
```
vgcreate -s 1G vg_thin /dev/sdc1
```
#### Kiểm tra thông số hiện có
```
pvs
```
![image](https://github.com/user-attachments/assets/a3ede57b-1528-4e5a-bd3b-374aaebdde6a)

### Tạo __Thin Pool__
```
lvcreate -L 5G --thinpool data_pool vg_thin
```
> -L – Size của volume group

> -–thinpool – Tạo thinpool

> data_pool – Tên Thin pool

> vg_thin – Volume group name sử dụng lưu trữ thinpool

![image](https://github.com/user-attachments/assets/d7611a6f-954e-429c-b16a-9baa9b4725c9)


__Kiểm tra thông số thin Pool__
```
lvs
lvdisplay vg_thin/data_pool
```
![image](https://github.com/user-attachments/assets/b6150783-6e93-4caf-bcba-7a86276a384d)

### Tạo Thin Volumes
- Tạo __thin volume__ nằm trong __thin pool__
```
lvcreate -V 2G --thin -n thin_vol_1 vg_thin/data_pool
```
![image](https://github.com/user-attachments/assets/416fb374-eb4f-48aa-b8de-934f39afa950)

> -V – Dung lượng của Thin Volume

> -–thin – Chỉ định đây là 1 Thin Volume

> -n – Tên Thin Volume

> vg_thin/data_pool – Chỉ định nơi lưu trữ của Thin Volume

- Tạo tương tự 2 thin volume

__Kiểm tra thông số__
```
# lvs
```
![image](https://github.com/user-attachments/assets/797a83a0-5d11-45f3-a9a8-c43828c6f52e)

### Tạo File System
#### Tạo thư mục và mount các thin volume
```
mkdir -p /data-pool/client1 /data-pool/client2
```
#### Định dang FS cho volume
```
mkfs.ext4 /dev/vg_thin/thin_vol_1 && mkfs.ext4 /dev/vg_thin/thin_vol_2
```
![image](https://github.com/user-attachments/assets/aeca9c17-61dd-40fc-a818-7af9b7427f6a)

#### Mount các volume vừa tạo
```
mount /dev/vg_thin/thin_vol_1 /data-pool/client1/ && mount /dev/vg_thin/thin_vol_2 /data-pool/client2/
```

#### Kiểm tra thông số vừa tạo
```
df -h
```
![image](https://github.com/user-attachments/assets/245d3bae-592b-4a0a-b1e4-d64d6a0f9078)

#### Tạo dữ liệu test và kiểm tra
```
# lvs
# lvdisplay vg_thin/data_pool
```
![image](https://github.com/user-attachments/assets/8fd40fe0-0698-4550-ad1b-2e217db4bdbd)

> Mỗi ổ có phần trăm sử dụng và giới hạn, tương tự với thin pool

### Over Provisioning
#### Cấp phát thin volume quá giới hạn
```
# lvcreate -V 2G --thin -n thin_vol_3 vg_thin/data_pool
```
![image](https://github.com/user-attachments/assets/b1478def-7ae5-4fab-8764-fd8c4da9086a)

> Tổng dung lượng đã vướt quá sức chứa thin pool

#### Kiểm tra thông số cấp phát
Dung lượng chưa được cấp phát khi data chưa được ghi xuống
```
# lvs
```
![image](https://github.com/user-attachments/assets/ead6df4d-ad21-4c2a-91b5-d6eb2f546535)

### Mở rộng logical thin-pool
```
lvextend -L +1G /dev/vg_thin/data_pool
```
![image](https://github.com/user-attachments/assets/ba625a8c-fb5b-4dd5-b2a7-aedd3a22e793)

> Sử dụng khi VG còn dung lượng hoặc vừa thêm mới các PV
