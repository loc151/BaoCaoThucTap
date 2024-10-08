## 1. Tải cái file ISO lên VMware ESXi:
- Trước khi tạo VM mới, ta cần các file iso của các hệ điều hành cần cài đặt:
- Tại giao diện web của ESXi, chọn **Storage -> Datastores -> Datastore browser**
![image](https://github.com/user-attachments/assets/1bb6e3bc-951c-4794-aebb-7df619f0cb25)

- Tại *Datastore browser*, chọn datastore để chứa file ISO, tạo thư mục mới để chứa các đĩa ISO của các hệ điều hành:
![image](https://github.com/user-attachments/assets/431e5cc2-1772-41f4-8794-23ed3621c1a5)

- Sau khi đã tạo thư mục xong, chọn **Upload** để tải các file ISO lên datastore:
![image](https://github.com/user-attachments/assets/65986743-3e0d-4267-ad10-13095ef75486)

- Một số file ISO sau khi đã cài đặt lên datastore:
![image](https://github.com/user-attachments/assets/2db78e6c-0b4d-46a5-a417-98cf2ac9e5c5)

## 2. Tạo VM mới:
- Tại giao diện của ESXi, chọn **Virtual Machines -> Create / Register VM** để tiến hành các bước tạo VM:
![image](https://github.com/user-attachments/assets/a0e031f8-04b2-4628-8950-75add0db67c1)

- Chọn **Create a new virtual machine**:
![image](https://github.com/user-attachments/assets/76209f06-cbfe-4705-8032-16ffd40ad5a7)

- Đặt tên cho VM mà xác định hệ điều hành:
![image](https://github.com/user-attachments/assets/ee31750f-f113-4570-aa0f-90fd424156ea)

- Chọn datastore để lưu trữ VM:
![image](https://github.com/user-attachments/assets/9953ff27-9609-4c1d-973a-3c901ba0c360)

- Cấu hình các thông số phần cứng:
![image](https://github.com/user-attachments/assets/bcc4fb2f-5acd-4804-9623-4e7894ac0a92)

- Tại **CD/DVD Drive 1**, chọn **Datastore ISO File** và chọn file ISO cần cài đặt:
![image](https://github.com/user-attachments/assets/8d563bbf-e960-42a0-8384-fda67425ee25)

- Xác nhận lại các thông số và nhấn **Finish** để hoàn tất việc cài đặt VM:
![image](https://github.com/user-attachments/assets/1b43c0b0-342e-45bb-a548-895e6b5a3fa6)
