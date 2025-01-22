
# Liên kết Zabbix với Grafana

Để liên kết Zabbix với Grafana, cần sử dụng một plugin có tên là "Zabbix Plugin for Grafana". Đây là một plugin bổ sung cho Grafana cho phép bạn truy vấn dữ liệu từ máy chủ Zabbix và hiển thị chúng trong biểu đồ và đồ thị trong Grafana.

Trên server cài grafana-server cài đặt plugin zabbix

```sh
grafana-cli plugins install alexanderzobnin-zabbix-app
```
![image](https://github.com/user-attachments/assets/7af8b9a4-8374-459c-9441-2cdce03afe22)


Sau khi cài xong plugin, khởi động lại dịch vụ Grafana

```sh
systemctl restart grafana-server
```

Tiến hành vào Grafana trên trình duyệt để cài đặt. 


Tại `Administrator >> Plugins and data >> Plugins`. Click Zabbix 
![image](https://github.com/user-attachments/assets/77f95347-cbca-4730-8097-57d3efeaafea)


`Enable` plugin zabbix này lên
![image](https://github.com/user-attachments/assets/e7ea3cdf-2d94-43c4-9618-ed2f8492e7e0)




Sau đó, thêm `Data sources`

Trong `Connections >> Data sources`. Click `Add data source`
![image](https://github.com/user-attachments/assets/185ce59a-1afc-489f-a023-67e02019cd5f)


Chọn data source là `zabbix`
![image](https://github.com/user-attachments/assets/ed943ca8-c398-4513-b60e-653e659132c4)



Thiết lập các thông số cần thiết để thêm data source của zabbix vào grafana


Thêm URL của zabbix server
![image](https://github.com/user-attachments/assets/3ff65ceb-4673-4c94-bbcc-d22c053ab40a)


Điền thông tin về zabbix connection, đây là tài khoản và mật khẩu khi bạn đăng nhập vào zabbix-server
![image](https://github.com/user-attachments/assets/4f6a7212-06f7-4da7-960a-0e0e20d3d88b)



Sau đó, click `save & test`
![image](https://github.com/user-attachments/assets/d4146121-ec5e-4fb5-9e1a-01ca00514c5f)



Nếu thành công sẽ hiển thị ra thông báo về phiên bản của zabbix-server
![image](https://github.com/user-attachments/assets/8d1d8df6-ba99-476a-86b4-1bb4ab8ea7f0)



# Thêm thiết bị cần giám sát trong Dashboards
Sau khi thêm `data source` của zabbix-server vào trong grafana, lúc này các thiết bị trong zabbix có thể được giám sát thông qua grafana


Trong `Dashboards >> Create Dashboard`
![image](https://github.com/user-attachments/assets/43a0aab5-e315-414e-aa5c-9f65db0d1392)



Chọn `Add visualization`
![image](https://github.com/user-attachments/assets/389e0048-5cef-46f5-b74f-77a1a0620838)


Chọn `Data source` 
![image](https://github.com/user-attachments/assets/31ecfe1d-957c-470a-9edb-f23dea3e5357)


Thiết lập các thông tin muốn mà bạn muốn hiển thị biểu đồ bao gồm: thiết bị, thông số,...Sau đó chọn save
![image](https://github.com/user-attachments/assets/6b96bc41-fdd3-4f44-a225-4111a8534673)



Sau khi thêm xong biểu đồ sẽ xuất hiện
![image](https://github.com/user-attachments/assets/c825a74d-fc28-4442-b686-ab4485c21c4a)


Nếu bạn muốn hiển thị thêm các thông số khác thì làm tương tự như trên
![image](https://github.com/user-attachments/assets/92ed3f6e-51ba-4edf-9c6d-13b17f5470f6)


## Thêm thiết bị cần giám sát

Tại `Dashboards >> New dashboard`
![image](https://github.com/user-attachments/assets/cbca653b-9e07-499a-a544-3ddd6c72d370)



Cũng làm tương tự như phần ở trên

![](./images/Screenshot_26.png)


![](./images/Screenshot_27.png)
