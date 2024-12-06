# LVM Snapshot
---
## Giới thiệu
LVM snapshot cung cấp tính năng cho phép tạo virtual images của thiết bị được chọn lập tức mà không làm gián đoạn các dịch vụ đang chạy.

Khi thay đổi được thực hiện sau khi thiết bị đã được snapshot, tính năng snapshot sẽ tạo bản copy khu vực, cho phép khôi phục khi cần.

Vì Snapshot chỉ sao chép phân vùng dữ liệu thay đổi sau khi snapshot được tạo => yêu cầu khối lượng lưu trữ nhỏ. VD: đối với dữ liệu ít được thay đổi, bản snap chỉ nặng từ 3-5% khi so sánh với phiên bản gốc.

## Phần 1: Tạo LVM Snapshot
### Bước 1: Kiểm tra thông số trước khi cấu hình
```
# vgs
# lvs
# pvs
```

![image](https://github.com/user-attachments/assets/1f37cbfc-4526-4a69-b666-ac4175d42c46)

#### Tạo LV
```
lvcreate -L 1G -n store-1 data-store
```
![image](https://github.com/user-attachments/assets/cbdd40ef-44d9-46dd-bc01-c82d205fcdbc)

### Tạo Snapshot cho LV vừa tạo
```
lvcreate -L 10GB -s -n store-1_snap /dev/data-store/store-1
```
> -s – Tạo Snapshot

> -n – Tên cho snapshot

> Cú pháp: lvcreate -L [Size] -s -n [Tên] [Snapshot cho LV]

![image](https://github.com/user-attachments/assets/32708a51-b1fa-4a6a-85d5-bce6650aa0ca)

### Xoá Snapshot vừa Tạo
```
lvremove /dev/data-store/store-1_snap
```
![image](https://github.com/user-attachments/assets/be0325e1-09a1-48d5-956c-f8da4b58a43f)

### Kiểm tra snapshot vừa tạo
```
lvs
```
![image](https://github.com/user-attachments/assets/094b408a-bf66-4307-b3e9-d1a688d30426)

### Kiểm chứng (Thêm dữ liệu và kiểm tra thông số thay đổi)
__Thêm định dạng, mount vào OS, kiểm tra__
```
mkfs -t ext4 /dev/data-store/store-1
```
![image](https://github.com/user-attachments/assets/d783212d-b5ed-4fe4-962b-6dfde41b00ed)

```
mount /dev/data-store/store-1 /data-store/store-1
```
![image](https://github.com/user-attachments/assets/7036301f-0e70-432a-95a1-29b61a6ff211)

```
df -Th
```
![image](https://github.com/user-attachments/assets/f7211d8f-6d84-4f11-999f-c980fb4d6169)


__Thêm dữ liệu, kiểm tra thay đổi__
```
lvs
df -Th
```
![image](https://github.com/user-attachments/assets/f0db9206-c2df-48b2-b58e-d405f724325a)

> Khi dữ liệu trong thư mục thay đổi, snapshot size sẽ thay đổi theo

__Vấn đề__

> Nếu LVM đầy, snapshot sẽ tự động xóa. Tính năng bảo đảm sẽ luôn có đủ không gian lưu FS.

### Phần 2: Mở rộng LVM
#### Mở rộng Snapshot
```
lvextend -L +100M /dev/data-store/store-1_snap
```

#### Kiểm tra lại thông số
```
# lvs
# lvdisplay
```
![image](https://github.com/user-attachments/assets/2bd7affa-0952-41ba-9d28-2bf3d7ac8720)
![image](https://github.com/user-attachments/assets/83574819-5b06-49ac-9f1b-3e9f577f8268)

### Phần 3: Khôi phục Snapshot (Merging)
#### Umount thư mục
```
umount /data-store/store-1
```
__Kiểm tra__
```
# df -h
```
![image](https://github.com/user-attachments/assets/edd2310d-77d5-43a0-ba73-71b7a1dd7225)

#### Khôi phục theo Snapshot
```
lvconvert --merge /dev/data-store/store-1_snap
```
> Sau câu lệnh trên dữ liệu quay về thời điểm SNAPSHOT

![image](https://github.com/user-attachments/assets/31c41770-ba0a-49ff-9a97-476c92a0228b)

```
# lvs
```

![image](https://github.com/user-attachments/assets/436dbe53-4ccb-43b8-9e8d-c07fa2c2eaa5)

> __Mặc định snapshot volume sẽ tự động removed__

__Kiểm tra__
```
# df -Th
```

![image](https://github.com/user-attachments/assets/1af97e9b-8c19-49b5-ae83-a73fe85ec27a)

### Tự động mở rổng Snapshot (Xem thêm tài liệu gốc)

## Nguồn
https://www.tecmint.com/take-snapshot-of-logical-volume-and-restore-in-lvm/
https://rwmj.wordpress.com/2014/05/22/using-lvms-new-cache-feature/
