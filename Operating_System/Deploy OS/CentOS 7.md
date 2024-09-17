# CentOS 7

## 1. Sau khi Boot từ USB, giao diện GRUB xuất hiện:
![image](https://github.com/user-attachments/assets/06d92e43-28cf-476c-9e93-b3e0c6020552)

## 2. Giao diện cài đặt:
![image](https://github.com/user-attachments/assets/6a63adf4-97ef-4911-bf32-973549e53b1b)

### 2.1. Ở phần System, chọn Installation Destination:
- Vào `Installation Destination` để cấu hình liên quan đến ổ cứng:
![image](https://github.com/user-attachments/assets/75fa9c15-bbc9-4fef-8e2a-338f5ba1ac2e)

- Chọn ổ cứng và ở phần **Other Storage Options**, chọn *I will configure partitioning* để phân vùng ổ cứng:
![image](https://github.com/user-attachments/assets/9bb05c03-3411-4d6c-ac93-76453665372c)

- Ở phần **Manual Partitioning**, tiến hành phân vùng các `mount` với **LVM**
![image](https://github.com/user-attachments/assets/c74c8974-cbf1-4cfb-9452-30d1688232d9)

- Cấu hình mount point `/boot`
![image](https://github.com/user-attachments/assets/e4913da2-50aa-49f8-abde-507b4d81474f)

- Riêng hệ điều hành CentOS, cần thêm mount point **biosboot** để đặc tả phân vùng từ GPT disk 
![image](https://github.com/user-attachments/assets/821bbbe1-a312-457d-801e-fb7975c5317d)

- Phân vùng các *mount* như trong ảnh:
![image](https://github.com/user-attachments/assets/eae4da11-1d6e-46d0-b2ee-22f40de3531f)

## 2.2. Cài đặt mật khẩu và tiến hành cài đặt:
- Cài đặt mật khẩu ở phần **User Settings**, sau đó đợi 1 khoảng thời gian để hoàn tất cài đặt. Chọn **Reboot** để khởi động lại sau khi đã hoàn thành cài đặt.
![image](https://github.com/user-attachments/assets/a07b8198-8ba9-4237-87a4-bd9f91c163c8)

- Khi reboot xong, giao diện GRUB xuất hiện, chọn dòng đầu tiên 
![image](https://github.com/user-attachments/assets/635689dd-2ddc-4da0-8499-c535c3537e5a)

- Khi xuất hiện dòng lệnh, tức là việc cài đặt đã thành công, đăng nhập và kiểm tra các cấu hình
![image](https://github.com/user-attachments/assets/57beff61-041f-4d7e-8e8d-0b7739b8a7fa)

![image](https://github.com/user-attachments/assets/ffd929bd-e8d4-465f-8f6f-307e3fc68dcc)

![image](https://github.com/user-attachments/assets/45a6dc2c-556b-461a-bf34-5f15c8d65654)

![image](https://github.com/user-attachments/assets/c6b2f707-9205-4011-80b8-84408d5a118d)

![image](https://github.com/user-attachments/assets/d6ce97cb-be12-4cad-b31e-40610d783831)

![image](https://github.com/user-attachments/assets/1b6e1f19-29fc-4c8d-b49e-64c65d8a2fd6)


