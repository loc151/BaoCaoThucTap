# MultiVLAN: 
## Sử dụng Linux Bridge để cấu hình MultiVLAN:


## Cấu hình tại Cisco Switch:
- Cấu hình VLAN 10 và VLAN 20:

![image](https://github.com/user-attachments/assets/527164ab-f137-43c3-9d20-fd21948afcd1)

- Cấu hình cổng trunk cho GigabitEthernet 2/0/6:

![image](https://github.com/user-attachments/assets/b5a0f85e-196f-4cf2-8d9c-a0259f28f10d)

## Cấu hình tại Host KVM:
- Mở file cấu hình **Netplan** để chỉnh sửa file cấu hình:

```
sudo nano /etc/netplan/50-cloud-init.yaml
```

- Tại file này, cấu hình mạng VLAN bằng cách sử dụng linux-bridge:
```
    eno2:
      dhcp4: no
  vlans:
    vlan10:
      id: 10
      link: eno2
    vlan20:
      id: 20
      link: eno2
  bridges:
    br-vlan10:
      interfaces:
        - vlan10
      dhcp4: no
      addresses:
        - 10.10.10.100/24
      routes:
        - to: 10.10.10.0/24
          via: 10.10.10.1
    br-vlan20:
      interfaces:
        - vlan20
      dhcp4: no
      addresses:
        - 10.10.20.100/24
      routes:
        - to: 10.10.20.0/24
          via: 10.10.20.1
```

![image](https://github.com/user-attachments/assets/49635262-b8f9-4869-bef9-e4aa1dfc9c5c)

- Áp dụng cấu hình: Sau khi cấu hình xong, sử dụng lệnh sau để áp dụng cấu hình:

```
sudo netplan apply
```

- Kiểm tra cấu hình: Sử dụng lệnh `ip a` để kiếm tra xem cấu hình đã được lưu hay chưa:

![image](https://github.com/user-attachments/assets/d5ae9ea8-61e7-47cc-ac86-6ef2acfa1f67)

## Cấu hình tại VM:
- Mở `virt-manager`: Chọn máy ảo dùng để thực hiện cấu hình
- Tại **Virtual Network Interface**, chọn **Bridge devices -> br-vlan10 (VLAN10) hoặc br-vlan20 (VLAN20) -> Apply**

![image](https://github.com/user-attachments/assets/883008e4-1710-4bc9-997c-3d0768a4dc63)

![image](https://github.com/user-attachments/assets/5e87a882-28bd-49ec-8d91-8cbd5226815e)

- Tại máy ảo, vào file sau để cấu hình mạng:

```
sudo nano /etc/netplan/50-cloud-init.yaml  #ubuntu 22.04
```

- Cấu hình IP và các thông số phù hợp với bridge vừa kết nối ở trên:

![image](https://github.com/user-attachments/assets/cd00fc61-fe66-46f8-b229-1d7bab8c6248)

- Sử dụng lệnh `sudo netplan apply` để lưu cấu hình

## Kết quả: 2 VM khác VLAN có thể liên lạc được với nhau.

![image](https://github.com/user-attachments/assets/fb10f193-d6e8-4b38-8fc2-bb89a978cded)

![image](https://github.com/user-attachments/assets/768d484e-fe98-42fd-9177-5165160c5c97)
