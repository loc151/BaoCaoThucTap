## Di chuyển VM giữa các Datastore trên cùng 1 Host tại VMware vCenter (Không Shutdown máy)

1. Chọn 1 VM đang chạy để tiến hành chuyển sang Datastore khác. Lúc này Datastore2 đang lưu trữ VM này: 

![image](https://github.com/user-attachments/assets/515ce5f0-422b-44a4-9d33-bbbef3a4562d)

2. Chọn **`Migrate`** để bắt đầu chuyển datastore 

![image](https://github.com/user-attachments/assets/5dc87478-79f6-4fea-9bd7-eaf04616bd70)

3. Ở bước `Select a migration type`, chọn **Change storage only**:

![image](https://github.com/user-attachments/assets/51d69ab3-22f6-4344-848f-20c668f3381f)

4. Ở bước `Select storage`, chọn storage phù hợp để di chuyển (máy VM đang dùng đang được lưu trữ tại `datastore 2` nên chọn `datastore 1`)

![image](https://github.com/user-attachments/assets/97b622c7-2ca2-43cc-b00d-f577523cd121)

5. Xác nhận lại các thông tin và nhấn **Finish** để hoàn tất việc di chuyển: 

![image](https://github.com/user-attachments/assets/a7cb0dd5-c585-4e44-b4fb-3911d842899e)

6. Kết quả: VM đã được chuyển sang `datastore1` trong tình trạng VM vẫn đang hoạt động: 

![image](https://github.com/user-attachments/assets/a7fe6b2b-c852-42f2-b6bc-d03fd3b613cb)
