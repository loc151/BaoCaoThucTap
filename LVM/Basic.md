# Những câu lệnh cơ bản cấu hình LVM

## Phần 1: Tạo Logical Volume:
### Bước 1: Kiểm tra các ổ cứng hiện tại: `lsblk`
![image](https://github.com/user-attachments/assets/a1a6518f-d39d-4c85-ab2d-0339a609f811)

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

### Bước 3: Tạo Physical Volume:
- Tạo Physical Volume là /dev/sdb1 với lệnh sau: `pvcreate /dev/sdb1`
![image](https://github.com/user-attachments/assets/bb736bee-e862-416f-b501-f22241c9611a)
