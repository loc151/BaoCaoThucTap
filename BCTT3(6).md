# Báo cáo thực tập 3
## Networking
### Virtual LAN (VLAN): là 1 khái niệm trong đó ta có thể phân chia các thiết bị 1 cách hợp lý trên DLL. Nói chung, các thiết bị lớp 3 phân chia miền phát sóng nhưng miền phát sóng có thể được chia bằng các thiết bị chuyển mạch sử dụng VLAN
- Boardcast domain: là 1 phân đoạn mạng trong đó nếu 1 thiết bị phát 1 gói thì tất cả các thiết bị trong cùng 1 miền phát sóng sẽ nhận được nó. Các thiết bị trong cùng 1 miền phát sóng sẽ nhận được tất cả các gói phát sóng nhưng nó chỉ bị giới hạn ở các thiết bị chuyển mạch vì các bộ định tuyến không chuyển tiếp gói phát sóng. Để chuyển tiếp các gói tin đến các VLAN khác nhau hoặc các miền phát sóng, cần định tuyến giữa các VLAN. Thông qua VLAN, các mạng con kích thước nhỏ khác nhau được tạo ra tương đối dễ xử lý.
- Phạm vi VLAN:
  - VLAN 0, 4095: Những VLAN dành riêng không thể nhìn thấy hoặc sử dụng
  - VLAN 1: VLAN mặc định của các thiết bị chuyển mạch. Theo mặc định, tất cả các cổng chuyển mạch đều nằm trong VLAN. VLAN này không thể bị xoá hoặc chỉnh sửa nhưng có thể được sử dụng
  - VLAN 2-1001: Một phạm vi VLAN bình thường. Có thể tạo, chỉnh sửa và xoá các VLAN này
  - VLAN 1002-1005: Những mặc định của CISCO cho fddi và token ring. Không thể xoá các VLAN này
  - VLAN 1006-4094: Phạm vi mở rộng của VLAN
- Cấu hình:
  - Tạo VLAN bằng cách gán tên vlan-id và VLAN:
    ```
    #switch1(config)#vlan 2
    #switch1(config-vlan)#vlan accounts
    ```
