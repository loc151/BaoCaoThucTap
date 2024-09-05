## **1. Kron trên Cisco Switch là gì?**

**Kron** là một tính năng trên Cisco IOS dùng để thực hiện các tác vụ theo lịch trình định sẵn, tương tự như **cron** trên hệ điều hành UNIX/LINUX. Với Kron, ta có thể tự động hóa các tác vụ quản trị như sao lưu cấu hình, khởi động lại thiết bị...
### **1.1. Các Thành Phần Chính trong Kron**

- **Policy-List:** Định nghĩa các lệnh CLI sẽ được thực thi. Có thể có nhiều **policy-list** cho nhiều tác vụ khác nhau.
- **Occurrence:** Định nghĩa thời gian và tần suất để thực thi trong **policy-list**. Có thể đặt lịch theo thời gian cụ thể hoặc thiết lập để chạy định kỳ.

### **1.2. Tại Sao Nên Sử Dụng Kron Để Sao Lưu Định Kỳ?**

- **Tự động hóa và Tiết kiệm Thời gian:** Cho phép lập lịch các tác vụ sao lưu tự động, giúp giảm bớt công việc thủ công và tiết kiệm thời gian cho quản trị mạng
- **Đảm bảo tính nhất quán và độ tin cậy:** Việc sao lưu định kỳ giúp đảm bảo rằng luôn có bản sao lưu mới nhất của cấu hình thiết bị.
- **Tăng cường bảo mật:** Có thể được cấu hình để lưu trữ các bản sao lưu ở các vị trí an toàn, giúp bảo vệ dữ liệu cấu hình khỏi cái mối đe doạ bảo mật
- **Dễ dàng khôi phục và quản lý:** Có thể truy cập và khôi phục các bản sao lưu khi cần thiết, giúp giảm thiểu thời gian gián đoạn dịch vụ
- **Giảm thiểu lỗi do con người:** Tự động hóa giúp tránh được lỗi do con người gây ra khi sao lưu thủ công.
- **Tính linh hoạt:** Kron cho phép thực thi hầu hết mọi lệnh CLI của Cisco, giúp dễ dàng lên lịch các tác vụ quản trị khác.


## **2. Sao Lưu Định Kỳ Cấu Hình Sử Dụng Kron**

### **2.1. Cấu Hình Sao Lưu Định Kỳ Sử Dụng Kron**

#### **Bước 1: Tạo một Kron Policy-List**

Một **Kron policy-list** chứa các lệnh mà bạn muốn thực thi định kỳ. Trong trường hợp này, chúng ta sẽ tạo một policy-list để sao lưu cấu hình chạy (`running-config`) đến một máy chủ TFTP.

```shell
anhldl(config)#kron policy-list BackupConfig
anhldl(config-kron-policy)#cli copy running-config tftp://172.16.2.164/backup-config.cfg
anhldl(config-kron-policy)#exit
anhldl(config)#

```

- **Giải thích các câu lệnh:**
  - `kron policy-list BackupConfig`: Tạo một **policy-list** mới có tên là `BackupConfig`. Policy-list này sẽ chứa các lệnh cần thực thi.
  - `cli copy running-config tftp://172.16.2.164/backup-config.cfg`: Lệnh này sử dụng `cli` để chạy câu lệnh sao chép (`copy`) cấu hình đang chạy (`running-config`) từ switch tới máy chủ TFTP có địa chỉ IP là `172.16.2.164`, với tên file lưu trữ là `backup-config.cfg`.
  - `exit`: Thoát khỏi chế độ cấu hình `kron-policy`.

#### **Bước 2: Đặt Lịch Sao Lưu Định Kỳ với Kron Occurrence**

Sau khi đã tạo policy-list, bạn cần lên lịch để Kron thực thi policy này theo thời gian định sẵn.

```shell
anhldl(config)#kron occurrence backup-minute in 1 recurring
anhldl(config-kron-occurrence)#policy-list BackupConfig
anhldl(config-kron-occurrence)#exit

```

- **Giải thích các câu lệnh:**
  - `kron occurrence backup-minute in 1 recurring`: Tạo một tác vụ định kỳ có tên `backup-minute` sử dụng lệnh `occurrence`. Tác vụ này sẽ chạy 1 phút 1 lần và sẽ lặp lại hàng ngày (`recurring`).
  - `policy-list BackupConfig`: Chỉ định **policy-list** `BackupConfig` (đã tạo ở Bước 1) để thực thi khi `occurrence` này được kích hoạt. 
  - `exit`: Thoát khỏi chế độ cấu hình `kron-occurrence`.

### **2.2. Kiểm Tra và Quản Lý Cấu Hình Kron**

Sau khi cấu hình Kron, bạn có thể kiểm tra lại các cài đặt bằng lệnh `show`.
```shell
Switch#show kron schedule
```
![image](https://github.com/user-attachments/assets/4540c4c3-cea0-44ca-ae7b-0bd66252b01b)

- **Giải thích các câu lệnh:**

  - `show kron schedule`: Hiển thị lịch trình thực thi các Kron occurrence, bao gồm tên occurrence, thời gian chạy, và trạng thái.
 
**Ảnh dưới đây là folder lưu trữ các  file cấu hình tự động**

![](https://img001.prntscr.com/file/img001/VOsWvizGR-WyK4K5lrGIUg.png)

## **3. Sao Lưu Định Kỳ Cấu Hình Sử Dụng Archive**

## **4. So sánh KRON và Archive**

|Tiêu chí|KRON|Archive|
|:---|:---|:---|
|Mục đích|Lập lịch và thực thi các lệnh CLI tự động|Sao lưu cấu hình tự động khi có thay đổi|
|Linh hoạt|Cao, có thể thực hiện nhiều tác vụ khác nhau|Chuyên biệt cho sao lưu cấu hình|
|Cấu hình|Phức tạp hơn, cần tạo **Policy List** và **Occurance**|Đơn giản, chỉ cần thiết lập đường dẫn và tần suất|
|Tần suất sao lưu|Theo lịch định trước|Mỗi khi có thay đổi cấu hình|

- Kết luận:
  - `KRON`: khi cần thực hiện nhiều tác vụ tự động khác nhau, không chỉ sao lưu cấu hình
  - `Archive`: Khi cần 1 giải pháp đơn giản và tự động để sao lưu cấu hình mỗi khi có thay đổi
