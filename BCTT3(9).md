# Báo cáo thực tập 3
## Networking
###  VLAN Trunking Protocol (VTP): là giao thức độc quyền của CISCO được sử dụng để duy trì tính nhất quán trên toàn mạng hoặc người dùng có thể nói rằng đồng bộ hoá thông tin VLAN trong cùng 1 miền VTP. VTP cho phép thêm, xoá và đổi tên các VLAN sau đó được truyền tới các bộ chuyển mạch khác trong miền VTP. Quảng bá VTP có thể được gửi qua đường 802.1Q và ISL
- Yêu cầu: để VTP truyền thông tin VLAN giữa các switch:
  - Phiên bản VTP phải giống nhau trên các thiết bị chuyển mạch mà người dùng muốn định cấu hình
  - Tên miền VTP phải giống nhau trên các thiết bị chuyển mạch
  - Một trong các switch phải là máy chủ
  - Xác thực phải khớp nếu được áp dụng
 
- Chế độ VTP:
  - `Server`: các switch được đặt ở chế độ này theo mặc định. Chế độ này cho phép tạo, thêm hoặc xoá VLAN. Những thay đổi muốn thực hiện phải được thực hiện ở chế độ này. Mọi thay đổi được thực hiện trên chế độ này (trên 1 switch cụ thể) sẽ được quảng bá tới tất cả các switch trong cùng 1 miền VTP. Ở chế độ này, cấu hình được lưu trong NVRAM
  - `Configuration`:
    - Đầu tiên, cần thực hiện chuyển đổi máy chủ VTP:
      ```
      Switch# config terminal
      Switch(config)#vtp mode server
      ```
    - Tiếp theo, người dùng phải tạo miền VTP và gán mật khẩu để xác thực:
      ```
      Switch(config)#vtp domain anhldl
      Switch(config)#vtp password 123456
      ```
    -  Có thể xác minh cấu hình bằng cách:
      ```
      Switch(config)#do should vtp password
      Switch(config)#do show vtp
      ```
    - `Client`: các thiết bị chuyển mạch nhận được các bản cập nhật và cũng có thể chuyển tiếp đến các thiết bị chuyển mạch khác (trong cùng 1 miền VTP). Các bản cập nhật nhận được ở đây không được lưu trong NVRAM nên tất cả cấu hình sẽ bị xoá nếu switch được đặt lại hoặc tải lại, tức là các switch sẽ chỉ học và chuyển các quảng bá tóm tắt VTP tới các switch khác
    - `Configuration`: Vì các switch được đặt ở chế độ máy chủ theo mặc định, do đó người dùng có thể thay đổi nó sang chế độ client bằng cách:
      ```
      Switch(config)#vtp mode client
      ```
    - `Transparent`: Chuyển tiếp các quảng bá tóm tắt VTP thông qua liên kết. Các switch chế độ này có thể tạo cơ sở dữ liệu cục bộ của riêng chúng để giữ bí mật với các switch khác. Mục đích của chế độ này là chuyển tiếp các quảng cáo tóm tắt VTP nhưng không tham gia vào các nhiệm vụ VLAN
    - `Configuration`
      ```
      Switch(config)#vtp mode transparent
      ```
    - `Configuration Revision Number`: Sửa đổi cấu hình số là số 32 bit cho biết mức độ sửa đổi cho gói VTP. Số cấu hình này được theo dõi bởi mọi switch để biết rằng thông tin nhận được mới hơn phiên bản hiện tại. Mỗi khi switch máy chủ thực hiện 1 sửa đổi trên VLAN và số sửa đổi cấu hình sẽ tăng thêm 1. Các thiết bị ở chế độ *client* nhận được nó và kiểm tra xem số sửa đổi cấu hình mà chúng nhận được có phải là mới nhất hay không bằng cách so sánh số cấu hình của chính chúng với số nhận được. Nếu số cấu hình lớn hơn số của chính chúng thì thiết bị sẽ cập nhật cấu hình của chúng và chuyển nó đến các client khác trong cùng miền VTP. Nếu số cấu hình giống nhau thì các thiết bị sẽ chuyển nó cho các máy khách khác trong cùng miền VTP. Kiểm tra số sửa đổi cấu hình bằng cách:
    - ```
      switch(config)#do show vtp status
      ```
- Sử dụng VTP trong 1 tổ chức: tất cả các thiết bị chuyển mạch để được thiết kế để trở thành máy chủ VTP. Thiết kế này phù hợp với các mạng có phạm vi giới hạn, trong đó kích thước của dữ liệu VLAN nhỏ và dữ liệu dễ dàng được lưu trữ trong tất cả các bộ chuyển mạch (trong NVRAM). Trong 1 tổ chức lớn, chủ tịch phải đưa ra quyết định khi việc lưu trữ NVRAM quan trọng không hiệu quả vì nó được sao chép trên mỗi bộ chuyển mạch. Người giám sát tổ chức phải chọn 1 số thiết bị chuyển mạch đặc biệt và giữ chúng làm máy chủ VTP. Tất cả những thứ khác tham gia vào VTP đều có thể chuyển đổi thành máy khách. Số lượng máy chủ VTP phải được chọn để cung cấp mức độ lặp lại công khai cần thiết trong tổ chức
- Tổng quát:
  - Có thể thiết kế VLAN(s) mà không cần sắp xếp tên vùng VTP trên switch chạy Cisco IOS
  - Nếu 1 Impetus khác được nối vào dòng gồm 2 không gian VTP, thì Impetus mới sẽ giữ tên không gian của công tắc chính gửi cho nó 1 quảng bá tóm tắt. Cách tốt nhất để tham gia thay đổi này vào 1 không gian VTP khác là đặt tên vùng VTP thay thế về mặt vật lý
  - Dynamic Trunking Protocol (DTP) gửi tên không gian VTP trong gói DTP. Do đó, nếu có 2 đầu kết nối nằm ở vị trí có nhiều không gian VTP khác nhau, ngăn lưu trữ sẽ không xuất hiện nếu sử dụng DTP. Trong trường hợp đặc biệt, nên thiết kế chế độ khoang lưu trữ như trên hoặc điều chỉnh ở 2 bên để cho phép khoang lưu trữ xuất hiện mà không cần hiểu thảo luận về DTP
  - Nếu không gian chỉ có 1 máy chủ VTP duy nhất và nó gặp sự cố, phương pháp tốt nhất là thay đổi bất kỳ máy khách VTP nào trong khu vực đó thành VTP server. Việc sửa đổi cấu hình vẫn không thay đổi ở các máy khách khác, bất kể máy chủ có gặp sự cố hay không. Do đó, VTP hoạt động phù hợp trong khu vực.
      
