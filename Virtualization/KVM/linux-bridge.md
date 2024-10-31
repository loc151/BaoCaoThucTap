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

![](./images/linuxbridge.png)

## Chức năng của một switch ảo do Linux bridge tạo ra
- STP: Là giao thức chống loop gói tin trong switch
- Vlan: Là tính năng rất quan trọng trong một switch
- FDB: Là tính năng chuyển gói tin theo database được xây dựng giúp tăng tốc độ của switch 


![image](https://github.com/user-attachments/assets/df0a4cd2-1039-4908-ba37-2aa29cf6318e)

![image](https://github.com/user-attachments/assets/94505eae-c455-4c99-80af-1a41798a79be)

![image](https://github.com/user-attachments/assets/cef8ca53-3a35-4bf0-8061-2886fc10af97)

![image](https://github.com/user-attachments/assets/9550569a-9b46-41a3-ba26-cc97e08d2c9d)

![image](https://github.com/user-attachments/assets/694c0436-c89c-4b05-9df7-b9b295e95b26)
