
# Liên kết Zabbix với Grafana

Để liên kết Zabbix với Grafana, cần sử dụng một plugin có tên là "Zabbix Plugin for Grafana". Đây là một plugin bổ sung cho Grafana cho phép bạn truy vấn dữ liệu từ máy chủ Zabbix và hiển thị chúng trong biểu đồ và đồ thị trong Grafana.

Trên server cài grafana-server cài đặt plugin zabbix

```sh
grafana-cli plugins install alexanderzobnin-zabbix-app
```

![](./images/Screenshot_8.png)


Sau khi cài xong plugin, khởi động lại dịch vụ Grafana

```sh
systectl restart Grafana
```

Tiến hành vào Grafana trên trình duyệt để cài đặt. 


Tại `Administrator >> Plugins and data >> Plugins`. Click Zabbix 


![](./images/Screenshot_9.png)



`Enable` plugin zabbix này lên


![](./images/Screenshot_10.png)



Sau đó, thêm `Data sources`

Trong `Connections >> Data sources`. Click `Add data source`


![](./images/Screenshot_11.png)


Chọn data source là `zabbix`


![](./images/Screenshot_12.png)


Thiết lập các thông số cần thiết để thêm data source của zabbix vào grafana


Thêm URL của zabbix server


![](./images/Screenshot_13.png)


Điền thông tin về zabbix connection, đây là tài khoản và mật khẩu khi bạn đăng nhập vào zabbix-server


![](./images/Screenshot_14.png)


Sau đó, click `save & test`


![](./images/Screenshot_15.png)


Nếu thành công sẽ hiển thị ra thông báo về phiên bản của zabbix-server


![](./images/Screenshot_16.png)



# Thêm thiết bị cần giám sát trong Dashboards
Sau khi thêm `data source` của zabbix-server vào trong grafana, lúc này các thiết bị trong zabbix có thể được giám sát thông qua grafana


Trong `Dashboards >> Create Dashboard`

![](./images/Screenshot_17.png)


Chọn `Add visualization`


![](./images/Screenshot_18.png)



Chọn `Data source` 


![](./images/Screenshot_19.png)


Thiết lập các thông tin muốn mà bạn muốn hiển thị biểu đồ bao gồm: thiết bị, thông số,...Sau đó chọn save


![](./images/Screenshot_20.png)


Sau khi thêm xong biểu đồ sẽ xuất hiện


![](./images/Screenshot_21.png)


Nếu bạn muốn hiển thị thêm các thông số khác thì làm tương tự như trên


![](./images/Screenshot_23.png)



## Thêm thiết bị cần giám sát

Tại `Dashboards >> New dashboard`

![](./images/Screenshot_25.png)


Cũng làm tương tự như phần ở trên

![](./images/Screenshot_26.png)


![](./images/Screenshot_27.png)
