# Báo cáo thực tập 3
## Networking
### Spanning Tree Protocol (STP): là giao thức được sử dụng để ngăn chặn vòng lặp trong mạng. Khi 1 mạng có nhiều đường kết nối giữa các thiết bị (như switch hoặc bridge), vòng lặp có thể xảy ra. STP cho phép các bridge truyền thông với nhau để phát hiện vòng lặp vật lý và sau đó tạo ra 1 cấu trúc cây không có vòng lặp, bao gồm các lá và các nhánh kết nối toàn bộ layer 2
- Thuật ngữ liên quan:
  - Bridge Priority Data Unit (BPDU): chứa ID Bridge, ID Bridge của người gửi, chi phí cho Root Bridge, giá trị hẹn giờ trên Root Bridge. Tất cả các switch chuyển mạch BPDU để chọn Root Bridge. Switch có ID Bridge thấp nhất trở thành Root Bridge.
  - ID Bridge: là trường 8 byte kết hợp giữa mức độ ưu tiên bridge (2 byte) và địa chỉ MAC cơ sở (6 byte) của thiết bị. Nếu có sự ràng buộc về mức độ ưu tiên Bridge thì địa chỉ MAC cơ sở được xem xét
  - Priority Bridge: là mức độ ưu tiên, được gán cho mọi công tắc, mặc định là 32768
  - Root Bridge: là Bridge có ID thấp nhất. Tất cả các quyết định như cổng nào là cổng gốc (cổng có đường dẫn tốt nhất đến cầu gốc) được thực hiện theo luật xa gần của Root Bridge
  - Path cost: 1 công tắc có thể gặp 1 hoặc nhiều công tắc trong đường dẫn đến Root Bridge. Tất cả các đường dẫn có Path cost thấp nhất sẽ được chọn.
  
    |Speed|Link Cost|
    |:---|:---|
    |10 Mbps|100|
    |100 Mbps|19|
    |1 Gbps|4|
    |10 Gbps|2|
  - Designated port: Cổng gửi BPDU tốt nhất, tức là các cổng trên Root Bridge sẽ ở trạng thái chuyển tiếp
  - Root port: Cổng nhận BPDU tốt nhất trên Non-root bridge. Tiêu chí chọn cổng root:
    - Chi phí đường dẫn thấp nhất để đến Root Bridge
    - ID bridge người gửi thấp nhất
    - ID port người gửi thấp nhất
    - (Port priority + Port number) - Port priority mặc định là 128 và Port number là số giao diện chuyển đổi
- Thủ tục bầu cử: Tất cả các switch trong mạng đều tự khai báo các Root Bridge và bắt đầu trao đổi BPDU của riêng chúng. BPDU có ID thấp nhất được coi là vượt trội. Switch nhận BDPU vượt trội tạo ra những thay đổi trong BPDU của chính nó và chuyển sang các lân cận. Nó thay đổi giá trị của ID Root Bridge bằng ID Bridge BPDU cao cấp của nó. Quá trình này diễn ra cho đến khi tất cả các switch hài lòng với Bridge có ID thấp nhất và do đó Switch sẽ được khai báo là Root Bridge. Theo tiêu chí, các Root port sẽ được chọn và các cổng còn lại sẽ ở chế độ *blocking*
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
  - `802.1S (Multiple Spanning Tree)`: Nhóm các VLAN được thực hiện và đối với mỗi nhóm, RSTP được chạy. Về cơ bản, đây là một STP chạy trên 1 STP khác
    - Ưu điểm: Dự phòng cao và đạt được cân bằng tải. Mức sử dụng CPU và bộ nhớ thấp
    - Nhược điểm: Cần cấu hình nhiều hơn và không dễ thực hiện

### EtherChannel: là 1 công nghệ tổng hợp liên kết cổng, trong đó nhiều liên kết cổng vật lý được nhóm lại thành một liên kết logic. Nó được sử dụng để cung cấp các liên kết tốc độ cao và dự phòng. Tối đa 8 liên kết có thể được tổng hợp tạo thành 1 liên kết logic duy nhất
- EtherChannel, hay Link Aggregation Control Protocol (LACP), là 1 kỹ thuật được sử dụng trong các mạng máy tính để kết hợp nhiều liên kết vật lý giữa 2 switch thành 1 liên kết logic duy nhất. Liên kết logic này cung cấp băng thông và dự phòng, cũng nhau cải thiện cân bằng tải
- Hoạt động: Nhóm 2 hoặc nhiều liên kết vật lý giữa 2 switch thành 1 liên kết logic duy nhất. Liên kết logic này được coi là 1 thực thể duy nhất, với các thiết bị chuyển mạch coi nó như một liên kết duy nhất. Lưu lượng truy cập được phân phối trên các liên kết vật lý trong liên kết logic, cung cấp băng thông và cân bằng tải được cải thiện
- Tiêu chí: Để tạo thành 1 EtherChannel, tất cả các cổng phải có:
  - Cùng duplex
  - Cùng tốc độ
  - Cùng 1 cấu hình VLAN (tức là VLAN root và VLAN được phép phải giống nhau)
  - Chế độ Switch port phải giống nhau (Access or trunk)
- Các loại giao thức:
  - `Port Aggregation Protocol (PAgP)`: giao thức độc quyền của Cisco. Đó là 1 loại cân bằng tải dữ liệu/lưu lượng liên quan đến việc tổng hợp logic các cổng chuyển mạch cho Cisco Ethernet. 1 PAgP EtherChannel có thể hợp nhất tối đa 8 liên kết vật lý thành 1 liên kết ảo. LACP, hay Link Aggregation Control Protocol:
    - ON: giao diện sẽ là 1 phần của EtherChannel nhưng không có cuộc đàm phán nào diễn ra
    - Desirable: giao diện sẽ liên tục cố gắng chuyển đổi giao diện bên kia thành EtherChannel
    - Auto: giao diện sẽ trở thành 1 phần EtherChannel nếu và chỉ khi nó được yêu cầu bởi giao diện ngược lại
    - OFF: Không có EtherChannel nào được cấu hình trên giao diện
  - Configuration:
  ![image](https://github.com/user-attachments/assets/1b51fada-a4f1-430f-a7e6-9182ab349f1a)
    - Có 1 cấu trúc liên kết nhỏ trong đó 2 thiết bị chuyển mạch S1 và S2 được kết nối với nhau và phải gói 2 liên kết này thành 1 liên kết logic duy nhất
    ```
    S1(config)# interface fa0/1
    S1(config-if)# channel-group 1 mode desirable
    S1(config)# interface fa0/2
    S1(config-if)# channel-group 1 mode desirable
    S1(config)# interface port-channel 1
    S1(config-if)# switchport trunk encapsulation dot1q
    S1(config-if)# switchport mode trunk 
    ```
    - Người dùng đã sử dụng chế độ **desirable** và chế độ switch-port trunk. Các chế độ phải giống nhau trên cả 2 switch, do đó cần cấu hình trên switch còn lại. Cấu hình trên switch S2:
    ```
    S2(config)# interface fa0/1
    S2(config-if)# channel-group 1 mode desirable
    S2(config)# interface fa0/2
    S2(config-if)# channel-group 1 mode desirable
    S2(config)# interface port-channel 1
    S2(config-if)# switchport trunk encapsulation dot1q
    S2(config-if)# switchport mode trunk 
    ```
  - `Link Aggregation Control Protocol (LACP)`: được định nghĩa trong 802.3AD, được sử dụng để tạo thành EtherChannel. Giao thức này gần giống với Cisco PAgP. Có nhiều chế độ khác nhau để cấu hình giao diện:
    - ON: Giao diện sẽ là 1 phần của EtherChannel nhưng không có cuộc đàm phán nào diễn ra
    - Active: Giao diện sẽ liên tục cố gắng chuyển đổi giao diện bên kia thành EtherChannel
    - Passive: giao diện sẽ trở thành 1 phần của EtherChannel nếu và chỉ khi nó được yêu cầu bởi giao diện ngược lại
    - OFF: Không có EtherChannel nào được cấu hình trên giao diện
  - Configuration:
  ![image](https://github.com/user-attachments/assets/5c8669b9-be1a-41d3-a4f2-54852d5604c3)
  - Cấu hình LACP cho S1:
    ```
    S1(config)# interface fa0/1
    S1(config-if)# channel-group 1 mode active
    S1(config)# interface fa0/2
    S1(config-if)# channel-group 1 mode active
    S1(config)# interface port-channel 1
    S1(config-if)# switchport trunk encapsulation dot1q
    S1(config-if)# switchport mode trunk 
    ```
  - Cấu hình LACP cho S2:
    ```
    S2(config)# interface fa0/1
    S2(config-if)# channel-group 1 mode active
    S2(config)# interface fa0/2
    S2(config-if)# channel-group 1 mode active
    S2(config)# interface port-channel 1
    S2(config-if)# switchport trunk encapsulation dot1q
    S2(config-if)# switchport mode trunk 
    ```
- Ưu điểm:
  - Tăng băng thông: Bằng cách kết hợp nhiều liên kết vật lý thành 1 liên kết logic duy nhất, EtherChannel cung cấp băng thông tăng lên giữa các thiết bị chuyển mạch, giúp cải thiện hiệu suất mạng và giảm tắc nghẽn
  - Cải thiẻn dự phòng: Cung cấp dự phòng được cải thiện bằng cách cho phép lưu lượng truy cập được định tuyến qua nhiều liên kết vật lý. Nếu 1 liên kết không thành công, lưu lượng truy cập sẽ tự động được định tuyến qua các liên kết còn lại
  - Cân bằng tải: phân phối lưu lượng truy cập trên nhiều liên kết vật lý, cung cấp cân bằng tải được cải thiện và ngăn ngừa tắc nghẽn trên bất kỳ 1 liên kết nào
  - Cấu hình mạng đơn giản: Đơn giản hoá cấu hình mạng bằng cách xử lý nhiều liên kết vật lý như 1 liên kết logic duy nhất. Điều này có thể làm giảm sự phức tạp của cấu hình mạng và giúp khắc phục dễ dàng hơn
  - Hiệu quả: Là 1 cách hiệu quả về chi phí để tăng băng thông và dự phòng trong mạng, vì nó cho phép sử dụng các liên kết vật lý hiện có thay vì yêu cầu phần cứng mới
