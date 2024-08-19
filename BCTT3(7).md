# Báo cáo thực tập
## Networking
### Network Address Translation (NAT): là kỹ thuật cho phép chuyển đổi từ một địa chỉ IP này thành một địa chỉ IP khác. Thông thường, NAT được sử dụng phổ biến trong mạng LAN sử dụng địa chỉ cục bộ khi cần truy cập ra mạng Internet công cộng và ngược lại
- Hoạt động:
  - Bộ định tuyến biên giới được cấu hình cho NAT, tức là bộ định tuyến có giao diện trong mạng cục bộ (bên trong) và một giao diện trong mạng toàn cầu (bên ngoài). Khi 1 gói đi qua bên ngoài mạng cục bộ, thì NAT sẽ chuyển đổi địa chỉ IP cục bộ đó thành địa chỉ IP toàn cầu. Khi một gói đi vào mạng cục bộ, địa chỉ IP toàn cầu được chuyển đổi thành địa chỉ IP cục bộ
  - Nếu NAT hết địa chỉ, tức là không còn địa chỉ nào trong nhóm được cấu hình thì các gói sẽ bị loại bỏ và gói không thể truy cập được của máy chủ ICMP đến đích được gửi
- NAT bên trong và ngoài địa chỉ:
  - Bên trong: đề cập đến các địa chỉ phải được dịch
  - Bên ngoài: đề cập đến các địa chỉ không nằm trong tầm kiểm soát của 1 tổ chức
  ![image](https://github.com/user-attachments/assets/9ef358d7-8e4b-4975-9bd9-7290f8c26c70)
  - Inside local address: địa chỉ IP được gán cho máy chủ lưu trữ trên mạng Inside (local). Địa chỉ có thể không phải là địa chỉ IP được chỉ định bởi nhà cung cấp dịch vụ, tức đây là những địa chỉ IP riêng. Đây là máy chủ bên trong nhìn từ mạng bên trong
  - Inside global address: địa chỉ IP đại diện cho 1 hoặc nhiều địa chỉ IP cục bộ bên trong với thế giới bên ngoài. Đây là máy chủ bên trong như được nhìn thấy từ mạng bên ngoài
  - Outside local address: đây là địa chỉ IP thực tế của máy chủ đích trong mạng cục bộ sau khi dịch
  - Outside global address: máy chủ bên ngoài như được nhìn thấy từ mạng bên ngoài. Nó là địa chỉ IP của máy chủ đích bên ngoài trước khi dịch
- Các loại dịch địa chỉ mạng: có 3 cách cấu hình NAT:
  - Static NAT: 1 địa chỉ IP chưa đăng ký (Private) duy nhất được ánh xạ với địa chỉ IP (Public) đã đăng ký hợp pháp, tức là ánh xạ 1-1 giữa các địa chỉ local và global. Điều này thường được sử dụng cho lưu trữ Web. Chúng không được sử dụng trong các tổ chức vì có nhiều thiết bị sẽ cần truy cập Internet và để cung cấp truy cập Internet, cần có địa chỉ IP công cộng
  - Dynamic NAT: 1 địa chỉ IP chưa đăng ký được dịch thành địa chỉ IP đã đăng ký (Public) từ 1 nhóm địa chỉ IP công cộng. Nếu địa chỉ IP của nhóm không miễn phí, thì gói sẽ bị loại bỏ vì chỉ có thể dịch 1 số địa chỉ IP riêng cố định sang địa chỉ công cộng
  - Port Address Translation (PAT): nhiều địa chỉ IP cục bộ (Private) có thể được dịch sang 1 địa chỉ IP đã đăng ký duy nhất. Số cổng được sử dụng để phân biệt lưu lượng truy cập, tức là lưu lượng truy cập nào thuộc về địa chỉ IP nào. Điều này được sử dụng thường xuyên nhất vì nó tiết kiếm chi phí bởi hàng ngàn người dùng có thể được kết nối với Internet bằng cách chỉ sử dụng 1 địa chỉ IP toàn cầu (public) thực
- Ưu điểm:
  - Bảo tồn các địa chỉ IP đã đăng ký hợp pháp
  - Cung cấp sự riêng tư vì địa chỉ IP của thiết bị, gửi và nhận lưu lượng truy cập sẽ bị ẩn
  - Loại bỏ việc đánh số lại địa chỉ khi mạng phát triển
- Nhược điểm:
  - Bản dịch dẫn đến độ trễ chuyển đổi đường dẫn
  - Một số ứng dụng nhất định sẽ không hoạt động trong khi NAT được bật
  - Làm phức tạp các giao thức đường hầm như IPsec
  - Ngoài ra, bộ định tuyến là 1 lớp thiết bị mạng, không nên giả mạo số cổng (lớp truyền tải) nhưng nó phải làm như vậy vì NAT
