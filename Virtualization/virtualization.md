## 1. Ảo hoá:
### 1.1. Khái niệm
- Là quá trình tạo ra phiên bản ảo của 1 thành phần nào đó, chẳng hạn như hệ điều hành, máy chủ, thiết bị lưu trữ, ...
- Công nghệ này sử dụng phần mềm để mô phỏng chức năng của phần cứng, cho phép nhiều hệ điều hành và ứng dụng chạy trên một máy chủ vật lý duy nhất, tăng khả năng sử dụng và tính linh hoạt của phần cứng.
- Là một trong những kĩ thuật tiết kiệm chi phí, giảm phần cứng và tiết kiệm năng lượng chính được các nhà cung cấp dịch vụ đám mây sử dụng.
- Ảo hoá cho phép chia sẻ 1 phiên bản vật lý duy nhất của 1 tài nguyên hoặc 1 ứng dụng giữa nhiều khách hàng và tổ chức cùng 1 lúc.
- Nó thực hiện điều này bằng cách chỉ định 1 tên logic cho bộ lưu trữ vật lý và cung cấp 1 con trỏ đến tài nguyên vật lý đó theo yêu cầu
- Công nghệ ảo hoá cung cấp 1 môi trường ảo không chỉ để thực thi các ứng dụng mà còn để lưu trữ, bộ nhớ và mạng
![image](https://github.com/user-attachments/assets/d0fb0c9e-1bcb-4773-a7d9-8f1ab8d68049)

  - **Host Machine:** Máy mà máy ảo được xây dựng đó
  - **Guest Machine:** Được đề cập như 1 máy ảo

### 1.2. Cách thức hoạt động của ảo hoá:
- Người giám sát tách các tài nguyên vật lý ra khỏi môi trường vật lý của chúng
- Các tài nguyên được lấy và phân chia, khi cần, từ môi trường vật lý đến các môi trường ảo khác nhau
- Người dùng hệ thống làm việc và thực hiện các phép tính trong môi trường ả
- Khi môi trường ảo đang chạy, người dùng hoặc chương trình có thể gửi 1 lệnh yêu cầu tài nguyên bổ sung tạo thành môi trường vật lý. Đáp lại, hypervisor chuyển tiếp thông báo tới hệ thống vật lý và lưu trữ các thay đổi. Quá trình này sẽ diễn ra với tốc độ gần như nguyên bản

### 1.3. Lợi ích của ảo hoá:
- Phân bổ nguồn lực linh hoạt và hiệu quả hơn
- Nâng cao năng suất phát triển
- Giảm chi phí cho cơ sở hạ tầng CNTT
- Truy cập từ xa và khả năng mở rộng nhanh chóng
- Tính khả dụng cao và phục hồi sau thảm hoạ
- Kiểm tra cơ sở hạ tầng CNTT theo yêu cầu
- Cho phép chạy nhiều hệ điều hành

### 1.4. Nhược điểm:
- Đầu tư ban đầu cao
- Rủi ro dữ liệu: Làm việc trên các phiên bản ảo trên tài nguyên được chia sẻ có nghĩa là dữ liệu được lưu trữ trên tài nguyên của bên thứ 3 khiến dữ liệu ở trong tình trạng dễ bị tấn công

### 1.5. Đặc điểm của ảo hoá:
- Tăng cường bảo mật: Khả năng kiểm soát việc thực thi chương trình khách theo cách hoàn toàn minh bạch mở ra những khả năng mới để cung cấp môi trường thực thi được kiểm soát và an toàn. Tất cả các hoạt động của chương trình khách thường được thực hiện trên máy ảo, sau đó máy ảo sẽ dịch và áp dụng chúng và các chương trình lưu trữ
- Thực thi được quản lý: Đặc biệt, chia sẻ, tổng hợp, mô phỏng và cô lập là những tính năng quan trọng nhất
- Chia sẻ: Ảo hoá cho phép tạo ra 1 môi trường điện toán riêng biệt trong cùng 1 máy chủ
- Tổng hợp: Có thể chia sẻ tài nguyên vật lý giữa nhiều khách, nhưng ảo hoá cũng cho phép tổng hợp, đây là quá trình ngược lại

## 2. Các loại ảo hoá:
