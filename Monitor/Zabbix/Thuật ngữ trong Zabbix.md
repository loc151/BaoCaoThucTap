## Các thuật ngữ cơ bản trong Zabbix

### 1.host
Một thiết bị vật lý hoặc ảo, ứng dụng, dịch vụ hoặc bất kỳ bộ sưu tập các thông số được giám sát nào khác có mối liên hệ logic.

### 2. host group
Một nhóm logic của các host; nó có thể chứa các host và các mẫu. Các host và các mẫu trong một nhóm host không có bất kỳ liên kết nào với nhau. Nhóm host được sử dụng khi gán quyền truy cập cho các host cho các nhóm người dùng khác nhau.

### 3. item
Một mảnh dữ liệu cụ thể mà bạn muốn nhận từ một host, một số liệu dữ liệu.

### 4. value preprocessing
Một quá trình biến đổi giá trị số liệu đã nhận trước khi lưu vào cơ sở dữ liệu.

### 5. trigger
Một biểu thức logic xác định một ngưỡng vấn đề và được sử dụng để "đánh giá" dữ liệu nhận được từ các item. Khi dữ liệu nhận được vượt qua ngưỡng, các trigger chuyển từ trạng thái 'Ok' sang trạng thái 'Problem'. Khi dữ liệu nhận được dưới ngưỡng, các trigger ở trạng thái 'Ok' hoặc quay trở lại trạng thái 'Ok'.

### 6. event
Một sự kiện duy nhất của một điều gì đó đáng chú ý như một trigger thay đổi trạng thái hoặc một sự kiện phát hiện/đăng ký tự động của agent.

### 7. event tag
Một đánh dấu được định nghĩa trước cho sự kiện. Nó có thể được sử dụng trong việc liên kết sự kiện, phân chia quyền hạn, vv.

### 8. event correlation
Một phương pháp của việc tương quan hóa vấn đề với việc giải quyết chúng một cách linh hoạt và chính xác.

### 9. problem
Một trigger đang ở trạng thái "Problem".

### 10. problem update
Các tùy chọn quản lý vấn đề được cung cấp bởi Zabbix, như thêm bình luận, xác nhận, thay đổi mức nghiêm trọng hoặc đóng thủ công.

### 11. action
Một phương tiện được xác định trước để phản ứng với một sự kiện.

### 12. escalation
Một kịch bản tùy chỉnh cho việc thực hiện các hoạt động trong một action; một chuỗi gửi thông báo/thực thi lệnh từ xa.

### 13. media
Một phương tiện giao tiếp thông báo; kênh giao tiếp.

### 14. notification
Một tin nhắn về một sự kiện gì đó được gửi đến người dùng qua kênh truyền thông được chọn.

### 15. remote command
Một lệnh được xác định trước sẽ tự động thực thi trên một host được giám sát khi một số điều kiện nào đó xảy ra.

### 16. template
Một tập hợp các thực thể (item, trigger, graph, low-level discovery rule, web scenario) sẵn sàng được áp dụng cho một hoặc nhiều host.

### 17. web scenario
Một hoặc nhiều yêu cầu HTTP để kiểm tra tính khả dụng của một trang web.

### 18. frontend
Giao diện web được cung cấp với Zabbix.

### 19. dashboard
Một phần có thể tùy chỉnh của giao diện web hiển thị các tóm tắt và trực quan hóa của thông tin quan trọng trong các đơn vị trực quan được gọi là widgets.

### 20. widget
Đơn vị trực quan hiển thị thông tin về một loại và nguồn nhất định (một tóm tắt, một bản đồ, một biểu đồ, đồng hồ, v.v.), được sử dụng trong bảng điều khiển.

### 21. Zabbix API
Zabbix API cho phép bạn sử dụng giao thức JSON RPC để tạo, cập nhật và truy xuất các đối tượng Zabbix (như host, item, graph và các đối tượng khác) hoặc thực hiện bất kỳ nhiệm vụ tùy chỉnh nào khác.

### 22. Zabbix server
Một tiến trình trung tâm của phần mềm Zabbix thực hiện giám sát, tương tác với các proxy và agent Zabbix, tính toán các trigger, gửi thông báo; một kho dữ liệu trung tâm.

### 23. Zabbix proxy
Một tiến trình có thể thu thập dữ liệu thay mặt cho Zabbix server, giảm bớt một phần tải xử lý từ server.

### 24. Zabbix agent
Một tiến trình triển khai trên các mục tiêu giám sát để giám sát một cách tích cực các tài nguyên và ứng dụng cục bộ.

### 25. Zabbix agent 2
Một thế hệ mới của Zabbix agent để giám sát tích cực các tài nguyên và ứng dụng cục bộ, cho phép sử dụng các plugin tùy chỉnh cho giám sát.

### 26. encryption
Hỗ trợ giao tiếp được mã hóa giữa các thành phần Zabbix (server, proxy, agent, các tiện ích zabbix_sender và zabbix_get) bằng giao thức Transport Layer Security (TLS).

### 27. network discovery
Khám phá tự động các thiết bị mạng.

### 28. low-level discovery
Khám phá tự động các thực thể cấp thấp trên một thiết bị cụ thể (ví dụ: hệ thống tệp, giao diện mạng, v.v.).

### 29. low-level discovery rule
Bộ định nghĩa cho việc khám phá tự động các thực thể cấp thấp trên một thiết bị.

### 30. item prototype
Một số liệu với các tham số cụ thể như biến, sẵn sàng cho việc khám phá cấp thấp. Sau khi khám phá cấp thấp, các biến sẽ tự động thay thế bằng các tham số thực tế đã khám phá và số liệu tự động bắt đầu thu thập dữ liệu.

### 31. trigger prototype
Một trigger với các tham số cụ thể như biến, sẵn sàng cho việc khám phá cấp thấp. Sau khi khám phá cấp thấp, các biến sẽ tự động thay thế bằng các tham số thực tế đã khám phá và trigger tự động bắt đầu đánh giá dữ liệu.

Các mẫu của một số thực thể Zabbix khác cũng được sử dụng trong khám phá cấp thấp - các mẫu biểu đồ, mẫu host, mẫu nhóm host.

agent autoregistration

Quá trình tự động mà Zabbix agent được đăng ký là một host và bắt đầu giám sát.
