# Linux Bridge
## Khái niệm - ứng dụng 
- Linux bridge là một phần mềm được tích hợp sẵn vào trong nhân Linux để giải quyết vấn đề ảo hóa phần network trong các máy vật lý. Về mặt logic Linux bridge sẽ tạo ra một con switch ảo để cho các VM kết nối được vào và có thể nói chuyện được với nhau cũng như sử dụng để ra mạng ngoài
- Ngoài ra khi tìm hiểu Linux bridge còn có một số thuật ngữ như:
	+ Port: Tương tự như cổng của một con switch thật
	+ Bridge: Ở đây là switch ảo
	+ Tap: Hay còn gọi là tap interface, là giao diện mạng để các VM kết nối với switch do Linux bridge tạo ra (nó hoạt động ở lớp 2 của mô hình OSI)
	+ fd: Forward data có nhiệm vụ chuyển dữ liệu từ VM tới switch

> Switch ảo do Linux bridge tạo ra có chức năng tương tự với 1 con switch vật lý

## Kiến trúc
Kiến trúc của Linux bridge như hình sau

![image](https://github.com/user-attachments/assets/1c8cfcd8-7a19-4d8c-90ed-46e18d6abaad)

- Trong đó:
	+ `Port`: Tương tự như cổng của một con switch thật
	+ `Bridge`: Ở đây là switch ảo
	+ `Tap`: Hay còn gọi là tap interface, là giao diện mạng để các VM kết nối với switch do Linux bridge tạo ra (nó hoạt động ở lớp 2 của mô hình OSI)
	+ `fd`: Forward data có nhiệm vụ chuyển dữ liệu từ VM tới switch

- Switch ảo do Linux bridge tạo ra có chức năng tương tự với 1 con switch vật lý:

![image](https://github.com/user-attachments/assets/a1474a69-f7c1-43ae-a591-991f648b4527)

- Có thể thấy rõ hơn cách kết nối của VM ra ngoài internet. Khi máy vật lý có card mạng kết nối với internet(không phải card wireless). Trên switch ảo sẽ phải có đường để kết nối ra ngoài internet (cụ thể là kết nối với card mạng của máy vật lý). Card mạng trên máy vật lý sẽ được gắn trực tiếp vào switch ảo nên có thể thấy sau khi add switch ảo và card vật lý có cùng địa chỉ MAC. Và trên card vật lý sẽ không còn địa chỉ IP mà nó được gắn cho switch ảo.

## Tạo và quản lý Bridge:
- Tại máy chủ chứa Host KVM: Sử dụng `netplan` để vào tệp cấu hình mạng:
```
sudo nano /etc/netplan/50-cloud-init.yaml
```

- Cấu hình linux-bridge như sau: 

![image](https://github.com/user-attachments/assets/0304aea8-b3a3-462a-9eb1-4e67d78f4c8f)

- Sử dụng `sudo netplan apply` để áp dụng cấu hình vừa thay đổi
- Sử dụng lệnh `ip a` để kiểm tra cấu hình. Bridge đã nhận địa chỉ IP của card mạng vật lý:

![image](https://github.com/user-attachments/assets/df0a4cd2-1039-4908-ba37-2aa29cf6318e)

- Kết nối VM với linux-bridge vừa khởi tạo:

![image](https://github.com/user-attachments/assets/694c0436-c89c-4b05-9df7-b9b295e95b26)

## Kết quả: VM đã nhận IP của dải mạng private. Các VM có thể kết nối với với mạng internet và có thể liên lạc được giữa các VM

![image](https://github.com/user-attachments/assets/94505eae-c455-4c99-80af-1a41798a79be)

![image](https://github.com/user-attachments/assets/cef8ca53-3a35-4bf0-8061-2886fc10af97)

![image](https://github.com/user-attachments/assets/9550569a-9b46-41a3-ba26-cc97e08d2c9d)

