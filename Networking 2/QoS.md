# QoS (Quality of Service): là 1 tập hợp các kỹ thuật và công nghệ được thiết kế để đảm bảo chất lượng dịch vụ truyền tải dữ liệu trong mạng. QoS cho phép các doanh nghiệp điều chỉnh lưu lượng mạng tổng thể của họ bằng cách thiết lập mức độ ưu tiên cho các loại dữ liệu cụ thể như video, âm thanh, ...
## 1. Ưu điểm:
- Ưu tiên lưu lượng: ưu tiên các loại lưu lượng quan trọng hơn, chẳng hạn như cuộc gọi VoIP hoặc video hội nghị, đảm bảo chúng không bị gián đoạn
- Giảm độ trễ: Bằng cách quản lý lưu lượng mạng, QoS giúp giảm độ trễ jitter, cải thiện trải nghiệm người dùng
- Phân bố băng thông: QoS có thể phân bổ băng thông 1 cách hiệu quả, đảm bảo rằng các ứng dụng quan trọng luôn có đủ băng thông để hoạt động tốt
## 2. Cách thức hoạt động: Chỉ được bật khi xảy ra tình trạng "bottleneck". Điểm đặc biệt chính là những vị trí xảy ra hiện tượng này lại liên quan trực tiếp đến băng thông. Có 2 trường hợp thường xảy ra
- Thiết lập của QoS vượt quá mức băng thông mà nhà cung cấp cho phép: xảy ra khi băng thông mà thiết lập quá mức so với mức được cho phép. Tuy nhiên lúc này, lưu lượng traffic có sẵn trên router lại không được ưu tiên vì hệ thống ứng dụng cho rằng lưu lượng băng thông này là hợp lý
- Mức băng thông của QoS thấp hơn so với tiêu chuẩn của ISP: đây là trường hợp tạo ra các bottelneck rất cao. Hiện tượng "nút cổ chai" sẽ làm cho các dịch vụ bị gián đoạn
- Các tham số đo lường định lượng QoS:
  - Băng thông: là tốc độ truyền dữ liệu qua thiết bị truyền dẫn qua 1 giây. QoS cho phép 1 router biết cách sử dụng 1 băng thông
  - Jitter: Tốc độ không đều của các gói trên mạng do tắc nghẽn gây ra, có thể dẫn đến hệ quả các gói đến muộn và không theo trình tự. Việc này có thể làm biến dạng hoặc tạo khoảng trống trong video và âm thanh được truyền tải
  - Độ trễ: Thời gian cần thiết để 1 gói đi từ điểm xuất phát đến đích cuối. Yếu tố này có thể bị ảnh hưởng bởi độ trễ của hàng đợi, xảy ra trong quá trình tắc nghẽn và gói tin đợi trong hàng đợi trước khi truyền đi. QoS cho phép hạn chế điều này bằng cách tạo hàng đợi ưu tiên dành riêng cho 1 số loại lưu lượng
  - Mất gói: Lượng dữ liệu bị mất do mất gói, hiện tượng này thường thấy khi gặp tắc nghẽn mạng, QoS cho phép các tổ chức đưa ra quyết định loại bỏ gói

## 3. Các thành phần cơ bản của QoS
- **Classification (Phân loại):** Phân loại các lưu lượng khác nhau và đánh dấu chúng để áp dụng các chính sách QoS khác nhau
- **Marking (Đánh dấu):** Gán các giá trị QoS cho lưu lượng đã được phân loại
- **Policing and Shaping:** Định lượng lưu lượng kiểm soát băng thông cho các loại lưu lượng khác nhau
- **Queueing and Scheduling**: Quản lý cách các gói tin được xếp hàng và xử lý trên các cổng mạng

## Cấu hình QoS trên Switch Cisco:
- Trước khi cấu hình QoS, cần kích hoạt tính năng QoS trên switch
  ```
  anhldl(config)#mls qos
  ```
  - `mls qos` là lệnh dùng để bật QoS trên switch. Khi lệnh này được bật, switch sẽ bắt đầu xử lý QoS cho tất cả các lưu lượng đi qua nó
- Kiểm tra xem tính năng đã được bật hay chưa:
  ```
  andldl#show mls qos
  ```
  ![image](https://github.com/user-attachments/assets/60fb5834-78d0-4eb3-ad14-37dbeb60dd61)

- Tạo một Extended Access List (ACL) để cho phép truy cập
  ```
  anhldl(config)#ip access-list extended ACL_Example
  anhldl(config-ext-nacl)#permit ip any any
  ```
  - `ip access-list extended ACL_Example`: Tạo 1 ACL Extended có tên *ACL_Example*
  -  `permit ip any any`: cho phép tất cả các gói tin ip từ bất kỳ nguồn nào đến bất kỳ đích nào
- Tạo **Class Map** để phân loại lưu lượng dựa trên ACL đã tạo:
  ```
  anhldl(config)#class-map match-all Class_Example
  anhldl(config-cmap)#match access-group name ACL_Example
  ```
  - `class-map match-all Class_Example`: Tạo 1 Class Map tên là Class_Example để phân loại lưu lượng
  - `match access-group name ACL_Example`: Áp dụng ACL ACL_Example để phân loại gói tin

- Tạo Policy Map để chỉ định hành động đối với các loại lưu lượng đã được phân loại:
  ```
  anhldl(config)#policy-map Policy_Example
  anhldl(config-pmap)#class Class_Example
  anhldl(config-pmap-c)#police 30000 8000 exceed-action drop
  anhldl(config-pmap-c)#exit
  ```

- Gán **Policy Map** cho cổng mạng muốn hạn chế tốc độ
  - Áp dụng cho traffic đi vào (Input):
    ```
    anhldl(config)#interface GigabitEthernet 2/0/1
    anhldl(config-if)#service-policy input Policy_Example
    ```
  - Áp dụng cho traffic đi ra (Output)
    ```
    anhldl(config)#interface GigabitEthernet 2/0/1
    anhldl(config-if)#service-policy output Policy_Example
    ```
- Trong trường hợp này, Switch không hỗ trợ Policy Map cho trafic đi ra
  ![image](https://github.com/user-attachments/assets/98f931b6-2f7b-4564-ae0c-81e73d3dc1ff)
