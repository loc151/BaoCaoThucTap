# Chế độ card mạng NAT trong KVM:

## Chuẩn bị: 
- Server có hệ điều hành CentOS 7 hoặc Ubuntu 20.04 trở lên
- Đã cài đặt KVM
- Có card mạng kết nối ra ngoài Internet
- Cài đặt ít nhất 1 VM 
- **Chú ý**: máy vật lý ở đây là máy cài KVM. Máy này có thể là một máy ảo nhưng ở đây ta coi nó như một server vật lý.

## Mô hình:

![image](https://github.com/user-attachments/assets/dc79a683-a161-4b5f-bd70-48d3a8fda200)

- Với mô hình mạng NAT, KVM sẽ tạo ra một thiết bị là virtual router.
- Khi tạo một dải mạng với mô hình NAT thì lúc này virtual router sẽ NAT từ dải mạng mà ta tạo ra ra địa chỉ của card mạng vật lý trên KVM host để đi ra ngoài internet.
- Khi một dải mạng tạo ra ta sẽ thấy trên KVM host xuất hiện một thêm một card mạng. Card mạng này đóng vai trò là gateway cho dải mạng mà ta tạo ra
![image](https://github.com/user-attachments/assets/77dae100-64f8-4b6f-b05c-fc4c02e4ec5d)

## Phân tích đường đi của gói tin:

![image](https://github.com/user-attachments/assets/538b3763-94e4-46bc-aae4-b66f54b5d3f1)

- Sử dụng lệnh `iptables -L -t nat` để xem các rule liên quan đến NAT:

![image](https://github.com/user-attachments/assets/c3f70493-8263-401e-afeb-a7776a792c02)

## Tạo mô hình NAT trên KVM:
1. Tại host KVM, dùng lệnh `virt-manager` để vào giao diện quản lý VM. Chọn **Edit -> Connection Details**

![image](https://github.com/user-attachments/assets/db51f3dd-33c7-4af3-a8b0-33a829277291)

2. Tại **Virtual Network**, tạo mạng ảo mới với `Mode = NAT`, cấu hình dải địa chỉ IP phù hợp:

![image](https://github.com/user-attachments/assets/e8de8efa-d210-424d-ae8a-05817a8c11eb)

3. Kiểm tra lại thông tin của cấu hình mạng vừa khởi tạo qua file XML:

![image](https://github.com/user-attachments/assets/4ed2ee42-4dcd-4d52-ace8-ccbda808f6c8)

4. Tại VM, chọn `Network source = NAT` ở phần **Virtual Network Interface**

![image](https://github.com/user-attachments/assets/36521db3-7b7a-4256-beed-0137e2def676)

5. Khởi động VM và thử xem VM đã kết nối vào mạng được hay chưa:

![image](https://github.com/user-attachments/assets/2b244f1a-082e-433c-873e-dc1289fe7e88)

