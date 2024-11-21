# Sử dụng LVM:

## 1. Kiểm tra thông tin về các thiết bị lưu trữ và phân vùng: `lsblk`
![image](https://github.com/user-attachments/assets/3e10ed18-3706-4e9e-9b8a-f4981a8c8c75)

## 2. Tạo vùng vật lý mới có thể sử dụng trong Volumes: `pvcreate`
![image](https://github.com/user-attachments/assets/f9ce5b80-6a15-4da5-9103-065dec183be4)

## 3. `vgcreate` tạo một nhóm ổ đĩa trên một ổ đĩa. Lưu ý rằng có thể thêm nhiều thiết bị hơn vào nhóm ổ đĩa.
![image](https://github.com/user-attachments/assets/e25d275c-965c-400b-a6d4-473a4c0bdcc8)

## 4. Tạo logical volume: `lvcreate`
![image](https://github.com/user-attachments/assets/36d70054-dd94-442b-89f7-32a8906dc05f)

