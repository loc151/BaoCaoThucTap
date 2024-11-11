# Process
Mỗi lệnh trên Linux khi thực thi sẽ 'run' một process hoặc một group các process
## 1. Tổng quan 
- Tất cả các chương trình trong Linux thực chất là các "process". Process chính là đơn vị cấu thành nên Linux.
- Mỗi tiến trình sẽ tương ứng với một tập các thông tin sau:
  - Một định danh (pid)
  - Một tiến trình cha (ppid)
  - Người sở hữu (uid) và nhóm (gid)
  - Một đầu vào chuẩn (stdin), một đầu ra chuẩn (stdout), một kênh báo lỗi chuẩn (stderr)
  - Thời gian sử dụng CPU (CPU time) và mức độ ưu tiên
  - Thư mục hoạt động hiện tại của tiến trình
  - Bảng các tham chiếu đến các file được tiến trình sử dụng

## 2. Kiểm tra tất cả các process đang chạy trên hệ thống
- Lệnh `ps`: Hiển thị các tiến trình
- Sử dụng lệnh `ps` và show thêm các thuộc tính `opid,ppid,user,rss,command` của process
```sh
ps -e -opid,ppid,user,rss,command
```

![image](https://github.com/user-attachments/assets/08e9dc42-6488-4ce6-b678-83ab83d661c7)

- Trong đó:
  - `-e`: Hiển thị tất cả các tiến trình đang chạy trên hệ thống
  - `-o`: Chỉ định định dạng đầu ra, cho phép chọn các trường cụ thể để hiển thị
  - `pid`: Số định danh duy nhất của mỗi tiến trình
  - `ppid`: ID của tiến trình cha đã tạo ra tiến trình hiện tại
  - `user`: Tên người dùng sở hữu tiến trình
  - `rss`: Resident Set Size: Lượng bộ nhớ vật lý (RAM) mà tiến trình đang sử dụng
  - `command`: Lệnh được sử dụng để khởi chạy tiến trình

- Lệnh `ps aux`: Hiển thị thông tin chi tiết về tất cả các tiến trình đang chạy trên hệ thống:
![image](https://github.com/user-attachments/assets/6160107a-de80-4f41-9f1a-122ebc860fd7)

- Trong đó:
  - `a`: Hiển thị thông tin về tất cả các tiến trình của tất cả người dùng trên hệ thống
  - `u`: Hiển thị thông tin chi tiết về user, bao gồm user, thời gian CPU sử dụng và mức độ ưu tiên của tiến trình
  - `x`: Hiển thị thông tin về các tiến trình không có terminal điều khiển
  - `%CPU`: Phần trăm CPU mà tiến trình đang sử dụng
  - `%MEM`: Phần trăm bộ nhớ vật lý (RAM) mà tiến trình đang sử dụng
  - `VSZ`: Kích thước bộ nhớ ảo của tiến trình
  - `RSS`: Kích thước bộ nhớ vật lý mà tiến trình đang sử dụng
  - `TTY`: Terminal liên kết với tiến trình (nếu có)
  - `STAT`:Trạng thái của tiến trình (R: Running, S: Sleeping)
  - `START`: Thời gian tiến trình bắt đầu chạy
  - `TIME`: Tổng thời gian CPU mà tiến trình đã sử dụng
    
## 3. Kiểm tra live các process đang chạy
```sh
top
```

![image](https://github.com/user-attachments/assets/db7934bd-f8bd-4e27-b224-d37968cda4a6)

- Thông tin được hiển thị:
	+ Dòng 1: 
		+ Thời gian
		+ Máy tính đã chạy được bao lâu rồi
		+ Số lượng người dùng
		+ Trung bình tải
		+ Trung bình tải hiển thị thời gian load hệ thống trong 1, 5 và 15 phút cuối.

	+ Dòng 2: 
		+ Tổng số nhiệm vụ
		+ Số lượng tác vụ đang chạy
		+ Số lượng tác vụ trong trạng thái “ngủ”
		+ Số lượng tác vụ đã dừng
		+ Số lượng tác vụ zombie (tiến trình không tồn tại)

	+ Dòng 3:
		+ Mức sử dụng CPU bởi người dùng theo tỷ lệ phần trăm
		+ Mức sử dụng CPU bởi hệ thống theo tỷ lệ phần trăm
		+ Mức sử dụng CPU bởi các tiến trình có mức ưu tiên thấp theo tỷ lệ phần trăm
		+ Mức sử dụng CPU bởi idle process (tiến trình cho biết bộ xử lý đang rảnh rỗi) theo tỷ lệ phần trăm
		+ Mức sử dụng CPU bởi io wait (thời gian CPU không hoạt động để chờ I/O disk hoàn thành) theo tỷ lệ phần trăm
		+ Mức sử dụng CPU bởi việc ngắt phần cứng theo tỷ lệ phần trăm
		+ Mức sử dụng CPU bởi việc ngắt phần mềm theo tỷ lệ phần trăm
		+ Mức sử dụng CPU bởi steal time (thời gian CPU ảo “chờ” CPU thực) theo tỷ lệ phần trăm

	+ Dòng 4:
		+ Tổng bộ nhớ hệ thống
		+ Bộ nhớ trống
		+ Bộ nhớ đã sử dụng
		+ Bộ nhớ đệm buffer cache

	+ Dòng 5: 
		+ Tổng swap có sẵn
		+ Tổng swap còn trống
		+ Tổng swap đã sử dụng
		+ Bộ nhớ khả dụng

	+ Bảng chính:
		+ ID tiến trình
		+ Người dùng
		+ Mức độ ưu tiên
		+ Mức độ nice (gọi một tập lệnh shell với mức độ ưu tiên cụ thể)
		+ Bộ nhớ ảo được sử dụng bởi tiến trình
		+ Bộ nhớ “thường trú” mà một tiến trình sử dụng (tức là tiến trình luôn ở trong bộ nhớ và không thể chuyển ra thiết bị lưu trữ khác)
		+ Bộ nhớ có thể chia sẻ
		+ CPU được sử dụng bởi tiến trình theo tỷ lệ phần trăm
		+ Bộ nhớ được sử dụng bởi tiến trình theo tỷ lệ phần trăm
		+ Thời gian tiến trình đã được chạy
		+ Lệnh

## 4. Sơ đồ pstree
- Lệnh `pstree` hiển thị các quy trình đang chạy trên hệ thống dưới dạng sơ đồ cây thể hiện mối quan hệ giữa một quy trình và quy trình mẹ của nó và bất kỳ quy trình nào khác mà nó tạo ra
```sh
pstree
```

![image](https://github.com/user-attachments/assets/329b9862-1276-4e3b-ad72-f69057d8e8c6)

## 5. Kill process
- Lệnh `kill`: Sử dụng để gửi tín hiệu đến một hoặc nhiều tiến trình, thường là để dừng hoặc kết thúc tiến trình đó.
```
kill [tuỳ chọn] PID
```
- Các tín hiệu phổ biến:
  - `- SIGTERM` (15): Tín hiệu kết thúc tiến trình 1 cách an toàn. Đây là tín hiệu mặc định nếu không chỉ định tín hiệu nào
  - `- SIGKILL` (9): Tín hiệu buộc dừng tiến trình ngay lập tức. Sử dụng tín hiệu này khi tiến trình không phản hồi với `SIGTERM`
  - `- SIGHUP` (1): Tín hiệu yêu cầu tiến trình khởi động lại. Thường được sử dụng để yêu cầu các dịch vụ đọc lại tệp cấu hình
  
```
kill -SIGTERM PID
hoặc
kill PID
```

- Lệnh `killall`: Sử dụng để gửi tín hiệu đến tất cả các tiến trình có cùng tên
- Lưu ý:
  - Sử dụng lệnh `kill` cẩn thận, đặc biệt là `SIGKILL`, vì nó sẽ buộc dừng tiến trình ngay lập tức mà không lưu lại bất kỳ dữ liệu nào
  - Cần có quyền quản trị để gửi tín hiệu đến các tiến trình không thuộc sở hữu của user
  
## 6. Process ID
- Process ID được đánh số theo thứ tự tăng dần. Bắt đầu từ 0 và tăng dần lên khi tới giá trị maximum. Giá trị maximum của Process ID có thể cấu hình được tùy vào từng hệ thống
- Có thể thay đổi giá trị Process ID maximum bằng cách thay đổi file `/proc/sys/kernel/pid_max`

## 7. Process Resource
- Process Resource chính là bộ nhớ mà Process sử dụng, không gian địa chỉ của Process là riêng biệt, nhờ thiết kế này mà các Process là độc lập với nhau

## 8. Độ ưu tiên của các tiến trình: 
- Tất cả các tiến trình đều có độ ưu tiên ban đầu được ngầm định là 0
- Mức độ ưu tiên của 1 tiến trình dao động trong khoảng từ -19 đến +19
- Chỉ người sử dụng có quyền `root` mới có thể giảm giá trị biểu diễn độ ưu tiên của tiến trình
- Lệnh `nice`: sử dụng để thay đổi độ ưu tiên của 1 tiến trình. Độ ưu tiên này ảnh hưởng đến các hệ điều hành phân bổ tài nguyên CPU cho tiến trình đó
```
sudo nice -nice_value command-arguments
```
- Lệnh `renice`: Cho phép thay đổi độ ưu tiên của 1 tiến trình sau khi đã chạy 
```
sudo renice -n nice_value  -p pid_of_the_process
```
