|STT|Guidance|Explanation|Demo|
|:---|:---|:---|:---|
|01|Update your packet list and upgrade your OS|Cập nhật danh sách gói tin và nâng cấp hệ điều hành|[Checklist 1](https://github.com/loc151/BaoCaoThucTap/blob/main/Network%20Security%20Checklist/LinuxServer/01-05.md#1-update-your-packet-list-and-upgrade-your-os)|
|02|Remove unnecessary packages|Loại bỏ các gói không cần thiết|[Checklist 2](https://github.com/loc151/BaoCaoThucTap/blob/main/Network%20Security%20Checklist/LinuxServer/01-05.md#2-remove-unnecessary-packages))|
|03|Detect weak password with John the Ripper|Phát hiện mật khẩu yếu với John the Ripper|[Checklist 3](https://github.com/loc151/BaoCaoThucTap/blob/main/Network%20Security%20Checklist/LinuxServer/01-05.md#3-detect-weak-passwords-with-john-the-ripper)|
|04|Verify no accounts have empty passwords|Xác minh không có tài khoản nào có mật khẩu trống|[Checklist 4]()|
|05|Set password rules|Đặt các quy tắc cho mật khẩu|[Checklist 5]()|
|06|Set password expiration in login.defs|Đặt thời hạn sử dụng mật khẩu trong login.defs|[Checklist 6]()|
|07|Disable USB devices (for headless servers)|Vô hiệu hoá thiết bị USB (với máy chủ không đầu )|[Checklist 7]()|
|08|Check which services are started at boot time|Kiểm tra những dịch vụ nào được bật khi khởi động|[Checklist 8]()|
|09|Detect all world-writable files|Phát hiện các tệp world-writable|[Checklist 9]()|
|10|Configure iptables to block common attacks|Cấu hình iptables để chặn các cuộc tấn công phổ biến|[Checklist 10]()|
|11|Set GRUB boot loader password|Đặt mật khẩu cho bộ nạp khởi động GRUB|[Checklist 11]()|
|12|Disable interactive hotkey startup at boot|Tắt phím tắt tương tác khi khởi động|[Checklist 12]()|
|13|Enable audited to check for read/write events|Cho phép kiểm tra để kiểm tra các sự kiện read/write|[Checklist 13]()|
|14|Secure any Apache servers|Bảo mật mọi máy chủ Apache|[Checklist 14]()|
|15|Install and configure UFW|Cài đặt và cấu hình UFW|[Checklist 15]()|
|16|Configure SSH securely|Cấu hình SSH an toàn|[Checklist 16]()|
|17|Disable telnet|Vô hiệu hoá telnet|[Checklist 17]()|
|18|Configure sysctl securely|Cấu hình sysctl một cách an toàn|[Checklist 18]()|
|19|Lock user accounts after failed attempts with Fail2Ban|Khóa tài khoản người dùng sau khi thử đăng nhập không thành công với Fail2Ban|[Checklist 19]()|
|20|Configure root user timeout|Cấu hình thời gian chờ của người dùng root|[Checklist 20]()|
|21|Check for hidden open ports with netstat|Kiểm tra các cổng hoạt động ẩn với netstat|[Checklist 21]()|
|22|Set root permissions for core system files|Đặt quyền root cho các tập tin hệ thống cốt lõi|[Checklist 22]()|
|23|Scan for rootkits|Quét rootkit|[Checklist 23]()|
|24|Check that shut down mode is enabled for sensitive event log alerts|Kiểm tra xem chế độ tắt máy có được bật để cảnh báo nhật ký sự kiện nhạy cảm không|[Checklist 24]()|
|25|Check that all event log data is being securely backed up|Kiểm tra xem tất cả dữ liệu nhật ký sự kiện có được sao lưu an toàn không|[Checklist 25]()|
|26|Evaluate event log monitoring process|Đánh giá quy trình giám sát nhật ký sự kiện|[Checklist 26]()|
|27|Keep watch for any users logging on under suspicious circumstances|Theo dõi bất kỳ người dùng nào đăng nhập trong những trường hợp đáng ngờ|[Checklist 27]()|
|28|Check remote access logs regularly|Kiểm tra nhật ký truy cập từ xa thường xuyên|[Checklist 28]()|
|29|In case of remote access activity: Make sure that the suspicious activity is flagged and documented|Trong trường hợp hoạt động truy cập từ xa: Đảm bảo rằng hoạt động đáng ngờ được đánh dấu và ghi lại|[Checklist 29]()|
|30|Make sure that the Suspected account privileges temporarily frozen|Đảm bảo rằng các đặc quyền của tài khoản bị nghi ngờ đã bị đóng băng tạm thời|[Checklist 30]()|
|31|Evaluate server configuration control process|Đánh giá quy trình kiểm soát cấu hình máy chủ|[Checklist 31]()|
|32|Update service packs and patches for software|Cập nhật gói dịch vụ và bản vá cho phần mềm|[Checklist 32]()|
|33|Check event log monitoring is properly configured|Kiểm tra giám sát nhật ký sự kiện được cấu hình đúng|[Checklist 33]()|
|34|Check that all user account logins are being recorded|Kiểm tra xem tất cả thông tin đăng nhập tài khoản người dùng có được ghi lại không|[Checklist 34]()|
|35|Check that all system configuration changes are being recorded|Kiểm tra xem tất cả các thay đổi cấu hình hệ thống có được ghi lại không|[Checklist 35]()|
|36|Make sure that there is a process in place for changing system configurations|Đảm bảo rằng có một quy trình để thay đổi cấu hình hệ thống|[Checklist 36]()|
|37|Ensure start-up processes are configured correctly|Đảm bảo các quy trình khởi động được cấu hình đúng|[Checklist 37]()|
|38|Remove unnecessary startup processes|Xóa các tiến trình khởi động không cần thiết|[Checklist 38]()|
|39|Ensure regular users cannot change system startup configuration|Đảm bảo người dùng thường xuyên không thể thay đổi cấu hình khởi động hệ thống|[Checklist 39]()|
|40|Remove unused software and services|Xóa phần mềm và dịch vụ không sử dụng|[Checklist 40]()|
|41|Run a full system anti-virus scan|Chạy quét toàn bộ hệ thống chống virus|[Checklist 41]()|
|42|Review your server firewall security settings and make sure everything is properly configured|Xem lại cài đặt bảo mật tường lửa máy chủ và đảm bảo mọi thứ được cấu hình đúng|[Checklist 42]()|
|43|Disable or remove all user accounts that haven't been active in the last 3 months|Vô hiệu hóa hoặc xóa tất cả tài khoản người dùng không hoạt động trong 3 tháng qua|[Checklist 43]()|
|44|Make sure that membership to both the admin and superadmin group is restricted to as few users as possible without causing any problems|Đảm bảo rằng quyền thành viên của cả nhóm quản trị viên và siêu quản trị viên được giới hạn ở càng ít người dùng càng tốt mà không gây ra bất kỳ vấn đề nào|[Checklist 44]()|
