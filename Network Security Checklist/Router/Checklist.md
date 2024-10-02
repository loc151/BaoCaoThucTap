|STT|Guidance|Explain|Making|Demo|
|:---|:---|:---|:---|:---|
|01|Do not use Default password for your router|Không sử dụng mật khẩu mặc định cho bộ định tuyến|||
|02|Check if the router block access to a modem by IP address|Kiểm tra xem bộ định tuyến có chặn quyền truy cập vào modem theo địa chỉ IP không|||
|03|Ensure that router admin gets an alert when a new device joins the network|Đảm bảo rằng người quản trị router nhận được cảnh báo khi có thiết bị mới tham gia mạng|||
|04|Most routers let you disable UPnP on the LAN side|Hầu hết các bộ định tuyến cho phép bạn vô hiệu hóa UPnP ở phía LAN|||
|05|Enable port forwarding and IP filtering for your router|Bật chuyển tiếp cổng và lọc IP cho bộ định tuyến|||
|06|Check if the router supports HTTPs, in some routers it is disabled by default|Kiểm tra xem bộ định tuyến có hỗ trợ HTTPs không, ở một số bộ định tuyến, HTTPs bị vô hiệu hóa theo mặc định|||
|07|If HTTPS is supported, can admin access be limited exclusively to HTTPS?|Nếu HTTPS được hỗ trợ, quyền truy cập của quản trị viên có thể bị giới hạn độc quyền đối với HTTPS không?|||
|08|Check if the TCP/IP port used for the web interface can be changed|Kiểm tra xem cổng TCP/IP được sử dụng cho giao diện web có thể thay đổi được không|||
|09|To really prevent local admin access, limit the LAN IP address to a single IP address that is both outside the DHCP range and not normally assigned|Để thực sự ngăn chặn quyền truy cập quản trị cục bộ, hãy giới hạn địa chỉ IP LAN thành một địa chỉ IP duy nhất nằm ngoài phạm vi DHCP và không được chỉ định bình thường|||
|10|Check if the admin access can be limited to Ethernet only|Kiểm tra xem quyền truy cập quản trị có thể chỉ giới hạn ở Ethernet không|||
|11|Check if the router access can be restricted by SSID and/or by VLAN|Kiểm tra xem quyền truy cập router có thể bị hạn chế bởi SSID và/hoặc VLAN không|||
|12|The router should not allow multiple computers to logon at the same time using the same userid|Bộ định tuyến không nên cho phép nhiều máy tính đăng nhập cùng lúc bằng cùng một ID người dùng|||
|13|Check if there is some type of lockout after too many failed attempts to login to the web interface|Kiểm tra xem có loại khóa nào sau quá nhiều lần đăng nhập không thành công vào giao diện web không|||
|14|Make sure the remote administration settings are turned off by default|Đảm bảo cài đặt quản trị từ xa được tắt theo mặc định|||
|15|Check if the port number can be changed remotely|Kiểm tra xem số cổng có thể được thay đổi từ xa không|||
|16|If you forget to logout from the router, eventually your session should time out, and, you should be able to set the time limit, the shorter, the more secure|Nếu quên đăng xuất khỏi bộ định tuyến, cuối cùng phiên sẽ hết thời gian và có thể đặt giới hạn thời gian, càng ngắn thì càng an toàn.|||
|17|Inbound WAN|Những cổng nào đang mở ở phía WAN/Internet? Câu trả lời an toàn nhất là không có và nên mong đợi bất kỳ bộ định tuyến nào không do ISP cung cấp đều không có cổng mở nào ở phía Internet. Một ngoại lệ là Remote Administration, yêu cầu phải có cổng mở. Mọi cổng mở ở phía WAN đều cần được tính đến, đặc biệt nếu bộ định tuyến do ISP cung cấp; chúng thường để lại một cửa sau. **The Test your Router** liên kết đến nhiều trang web cung cấp các bài kiểm tra tường lửa. Tuy nhiên, không có trang nào trong số chúng sẽ quét tất cả 65.535 cổng TCP hoặc tất cả 65.535 cổng UDP. Thời điểm tốt nhất để kiểm tra điều này là trước khi đưa bộ định tuyến mới vào sử dụng|||
|18|Inbound LAN|Những cổng nào đang mở ở phía LAN? Mong đợi cổng 53 được mở cho DNS (có thể là UDP, hoặc TCP). Nếu bộ định tuyến có giao diện web, thì điều đó yêu cầu một cổng mở. Tiện ích cổ điển/tiêu chuẩn để kiểm tra tường lửa phía LAN là nmap. Cũng như phía WAN, mọi cổng đang mở đều cần được tính đến.|||
|19|Outbound|Bộ định tuyến có thể tạo quy tắc tường lửa gửi đi không? Có đủ loại tấn công có thể bị chặn bằng quy tắc tường lửa gửi đi. Nhìn chung, bộ định tuyến dành cho người tiêu dùng không cung cấp quy tắc tường lửa gửi đi trong khi bộ định tuyến hạng doanh nghiệp thì có. Ngoài việc chặn, sẽ rất tuyệt nếu các khối được ghi lại cho mục đích kiểm tra. Tuy nhiên, lưu ý rằng các thiết bị được kết nối với Tor hoặc VPN sẽ không tuân thủ quy tắc tường lửa gửi đi|||

