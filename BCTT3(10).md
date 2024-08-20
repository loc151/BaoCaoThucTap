# Báo cáo thực tập 3
## Networking
### Spanning Tree Protocol (STP): là giao thức được sử dụng để ngăn chặn vòng lặp trong mạng. Khi 1 mạng có nhiều đường kết nối giữa các thiết bị (như switch hoặc bridge), vòng lặp có thể xảy ra. STP cho phép các bridge truyền thông với nhau để phát hiện vòng lặp vật lý và sau đó tạo ra 1 cấu trúc cây không có vòng lặp, bao gồm các lá và các nhánh kết nối toàn bộ layer 2
- Cần Spanning Tree: xem xét kịch bản dưới với 3 switch với 1 người dùng được gắn vào mỗi switch
  ![image](https://github.com/user-attachments/assets/5a6933d8-670b-4705-a1f1-90fb71720140)
  - Arvind gửi 1 khung phát sóng đến mạng LAN và vì bản chất của khung chuyển đổi được gửi ra từ các cổng khác (Gi0/1 & Gi0/2), ngoại trừ cổng nhận (Fa0/3).
  - Bây giờ, khung hình này chuyển sang SW2, SW2 cũng phát khung ra khỏi cổng Gi0/2 và Fa0/2.
  - SW1 nhận khung trong các cổng Gi0/1 của nó.
  - SW1 cũng phát khung sau đó khung này chuyển sang SW3 và phát sóng khung hình tiếp tục.
  - Việc phát khung hình này cũng xảy ra theo hướng khác từ SW3 ra khỏi cổng Gi0/1.
  - Vòng lặp khung hình ở trên là từ các cổng Gi0/2 của SW3.
  - Vòng lặp mãi mãi của các khung hình xung quanh mạng LAN được gọi là Broadcast storm.
  - Vòng lặp khung hình này gây ra 3 vấn đề:
    - `MAC table instability`: do vòng lặp của khung xung quanh mạng LAN, MAC-Table được thay đổi thường xuyên. Vòng lặp gây ra các MAC-Table không chính xác dẫn đến phân phối khung không chính xác 
    - `Broadcast Storm`: Chuyển tiếp lặp đi lặp lại các khung xung quanh các liên kết trong mạng LAN gây ra việc sử dụng các liên kết không hiệu quả
    - `Multiple Frame Transmission`: 1 tác động tiêu cực rất nghiêm trọng của vòng lặp là nhiều bản sao của cùng 1 khung được gửi đến máy chủ. Quá trình này để lại cho máy chủ sự nhầm lẫn
- Tác dụng:
  - STP ngăn chặn vòng lặp các khung xung quanh mạng LAN bằng cách đặt các cổng chuyển mạch ở trạng thái *forwarding* hoặc *blocking*. Giao diện (cổng switch) ở trạng thái *forwarding* hoạt động như bình thường nhưng giao diện ở trạng thái *blocking* không xử lý bất kỳ khung nào nhận được ngoại trừ tin nhắn STP và các chi phí quan trọng khác
  - Giao diện *blocking* không tìm hiểu địa chỉ MAC, không chuyển tiếp khung và không xử lý các khung đã nhận.
  - Xem xét lại tình huống trên với giao diện Gi0/2 của SW3 ở trạng thái *blocking*
  ![image](https://github.com/user-attachments/assets/346c3123-02e4-4f1a-a3b1-a48136976ea6)
    - Arvind gửi khung đến SW3
    - SW3 chuyển tiếp khung chỉ đến cổng Gi0/1 vì cổng Gi0/2 đang ở trạng thái chặn
    - SW1 nhận khung và chuyển tiếp đến giao diện Fa0/1 và Gi0/1
    - SW2 nhận khung và chuyển tiếp đến giao diện Fa0/2 và Gi0/1
    - SW3 sẽ nhận khung trên giao diện Gi0/2 nhưng bỏ qua khung vì nó ở trạng thái chặn
  - Như vậy, vòng lặp khung xung quanh mạng LAN có thể được ngăn chặn bằng cách sử dụng STP
- Các loại giao thức:
  - `802.1D`: còn được gọi là CST (Common Spanning Tree). Nó là 1 tiêu chuẩn cây kéo dài được phát triển bởi IEEE, chỉ chọn 1 cầu gốc trên toàn bộ cấu trúc liên kết. Tất cả lưu lượng truy cập chảy qua cùng 1 đường dẫn (tốt nhất) nhưng điều này không phải lúc nào cũng tốt vì có thể có các tình huống trong đó đường dẫn được tối ưu hoá để đến VLAN khác với đường dẫn thu được khi chọn cầu gốc. Nó rất chậm vì phải mất 32 giây để hội tụ
    - Ưu điểm: Yêu cầu ít CPU và bộ nhớ
    - Nhược điểm: Tối ưu hoá ít hơn và Không cần băng tải
  - `Per VLAN Spanning Tree + (PVST +)`: là 1 tiêu chuẩn cây kéo dài được phát triển bởi Cisco cho các thiết bị để tìm cầu gốc trên mỗi VLAN. Đây là phiên bản STP mặc định của Cisco. Nó tìm thấy phiên bản cây kéo dài 802.1D riêng biết cho mỗi VLAN. Nó cung cấp khả năng so sánh ngược với 802.1D riêng biệt cho mỗi VLAN. Nó cũng cung cấp khả năng so sánh ngược với 802.D hoặc CST
    - Ưu điểm: Cung cấp nhiều tối ưu hoá hơn về hiệu suất của mạng so với CST. Mức tiêu thụ băng thông ít hơn CST. Đạt được cân bẳng tải tối ưu
    - Nhược điểm: Thời gian hội tụ chậm (50s) và cần nhiều tài nguyên
  - `802.1W - Rapid Spanning Tree Protocol (RSTP)`: Cung cấp sự hội tụ nhanh hơn CST nhưng giữ cùng ý tưởng tìm 1 cây cầu gốc duy nhất trong cấu trúc liên kết. Tài nguyên cầu nối cần thiết trong RSTP cao hơn CST nhưng ít hơn PVST+
    - Lợi thế: Ngăn chặn các vòng lặp mạng và ngăn ngừa dư thừa. Hội tụ nhanh hơn. Tương thích ngược với STP
  - `Rapid Per VLAN Spanning Tree+ (RPVST+)`: cung cấp khả năng hội tụ nhanh hơn PVST+  và tìm thấy phiên bản riêng biệt trên mỗi VLAN. Nó đòi hỏi nhiều CPU và bộ nhớ hơn các tiêu chuẩn STP khác
  - 
  - `802.1S (Multiple Spanning Tree)`: Nhóm các VLAN được thực hiện và đối với mỗi nhóm, RSTP được chạy. Về cơ bản, đây là một STP chạy trên 1 STP khác
    - Ưu điểm: Dự phòng cao và đạt được cân bằng tải. Mức sử dụng CPU và bộ nhớ thấp
    - Nhược điểm: Cần cấu hình nhiều hơn và không dễ thực hiện
