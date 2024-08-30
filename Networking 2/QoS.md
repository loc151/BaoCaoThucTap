# QoS (Quality of Service): là 1 tập hợp các kỹ thuật và công nghệ được thiết kế để đảm bảo chất lượng dịch vụ truyền tải dữ liệu trong mạng. QoS cho phép các doanh nghiệp điều chỉnh lưu lượng mạng tổng thể của họ bằng cách thiết lập mức độ ưu tiên cho các loại dữ liệu cụ thể như video, âm thanh, ...
## Ưu điểm:
- Ưu tiên lưu lượng: ưu tiên các loại lưu lượng quan trọng hơn, chẳng hạn như cuộc gọi VoIP hoặc video hội nghị, đảm bảo chúng không bị gián đoạn
- Giảm độ trễ: Bằng cách quản lý lưu lượng mạng, QoS giúp giảm độ trễ jitter, cải thiện trải nghiệm người dùng
- Phân bố băng thông: QoS có thể phân bổ băng thông 1 cách hiệu quả, đảm bảo rằng các ứng dụng quan trọng luôn có đủ băng thông để hoạt động tốt
## Cách thức hoạt động: Chỉ được bật khi xảy ra tình trạng "bottleneck". Điểm đặc biệt chính là những vị trí xảy ra hiện tượng này lại liên quan trực tiếp đến băng thông. Có 2 trường hợp thường xảy ra
- Thiết lập của QoS vượt quá mức băng thông mà nhà cung cấp cho phép: xảy ra khi băng thông mà thiết lập quá mức so với mức được cho phép. Tuy nhiên lúc này, lưu lượng traffic có sẵn trên router lại không được ưu tiên vì hệ thống ứng dụng cho rằng lưu lượng băng thông này là hợp lý
- Mức băng thông của QoS thấp hơn so với tiêu chuẩn của ISP: đây là trường hợp tạo ra các bottelneck rất cao. Hiện tượng "nút cổ chai" sẽ làm cho các dịch vụ bị gián đoạn
- Các tham số đo lường định lượng QoS:
  - Băng thông: là tốc độ truyền dữ liệu qua thiết bị truyền dẫn qua 1 giây. QoS cho phép 1 router biết cách sử dụng 1 băng thông
  - Jitter: Tốc độ không đều của các gói trên mạng do tắc nghẽn gây ra, có thể dẫn đến hệ quả các gói đến muộn và không theo trình tự. Việc này có thể làm biến dạng hoặc tạo khoảng trống trong video và âm thanh được truyền tải
  - Độ trễ: Thời gian cần thiết để 1 gói đi từ điểm xuất phát đến đích cuối. Yếu tố này có thể bị ảnh hưởng bởi độ trễ của hàng đợi, xảy ra trong quá trình tắc nghẽn và gói tin đợi trong hàng đợi trước khi truyền đi. QoS cho phép hạn chế điều này bằng cách tạo hàng đợi ưu tiên dành riêng cho 1 số loại lưu lượng
  - Mất gói: Lượng dữ liệu bị mất do mất gói, hiện tượng này thường thấy khi gặp tắc nghẽn mạng, QoS cho phép các tổ chức đưa ra quyết định loại bỏ gói
