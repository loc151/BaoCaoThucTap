# Monitoring trong Linux

### Mục lục

[Top](#top)

[free](#free)

[vmstat](#vmstat)

[iostat](#iostat)

[mpstat](#mpstat)

[iftop](#iftop)

[nmon](#nmon)

[htop](#htop)

## Top
- Lệnh "top" trong Linux là một tiện ích hữu ích để theo dõi tài nguyên hệ thống của máy tính của bạn. Khi bạn chạy lệnh "top" trong terminal, nó sẽ hiển thị một danh sách các quy trình đang chạy trên máy tính của bạn, cùng với thông tin về việc sử dụng CPU, bộ nhớ, và các tài nguyên hệ thống khác. Đây là một công cụ mạnh mẽ để theo dõi hiệu suất của hệ thống và xác định các quy trình tiêu tốn nhiều tài nguyên.

- Dưới đây là một số phím tắt phổ biến có thể sử dụng khi ở trong chế độ "top":
   - **h**: Hiển thị trợ giúp về các lệnh tắt.
   - **k**: Tắt một tiến trình bằng cách yêu cầu nhập ID của nó.
   - **q**: Thoát khỏi "top".
   - **Space**: Làm mới màn hình.
   - **s**: Thay đổi khoảng thời gian làm mới (mặc định là 3 giây).
   - **M**: Sắp xếp các quy trình theo bộ nhớ sử dụng.
   - **P**: Sắp xếp các quy trình theo CPU sử dụng.
   - **T**: Sắp xếp các quy trình theo thời gian CPU sử dụng.

- Để thoát khỏi "top", nhấn phím "q".
![image](https://github.com/user-attachments/assets/0966acfd-9675-4c81-a87c-99d6bb65a512)

- Khi chạy lệnh "top" trong Linux, ta sẽ thấy một bảng các thông số đầu ra, mỗi dòng trong bảng này tương ứng với một quy trình đang chạy trên hệ thống của bạn. Dưới đây là các thông số đầu ra thông thường có thể gặp khi chạy lệnh "top":

1. **PID (Process ID)**: ID của quy trình.
2. **USER**: Người dùng sở hữu quy trình.
3. **PR**: Ưu tiên của quy trình.
4. **NI**: Ưu tiên (nice) của quy trình. Một số dương thể hiện ưu tiên thấp, còn số âm thể hiện ưu tiên cao.
5. **VIRT (Virtual Memory)**: Tổng lượng bộ nhớ ảo (thường là tổng bộ nhớ đã cấp phát cho quy trình).
6. **RES (Resident Memory)**: Lượng bộ nhớ vật lý thực sự đang được sử dụng bởi quy trình.
7. **SHR (Shared Memory)**: Lượng bộ nhớ được chia sẻ với các quy trình khác.
8. **S (%CPU)**: Phần trăm thời gian CPU được sử dụng bởi quy trình.
9. **MEM (%MEM)**: Phần trăm bộ nhớ RAM được sử dụng bởi quy trình.
10. **TIME+**: Thời gian CPU đã sử dụng bởi quy trình từ khi nó bắt đầu chạy.
11. **COMMAND**: Tên của lệnh hoặc chương trình đang chạy.

Thông số này cung cấp cái nhìn tổng quan về các quy trình đang chạy trên hệ thống của bạn, bao gồm việc sử dụng bộ nhớ, thời gian CPU và các thông tin liên quan.


## Free
- Lệnh "free" trong Linux được sử dụng để hiển thị thông tin về bộ nhớ hệ thống. Khi bạn chạy lệnh "free" trong terminal, nó sẽ hiển thị thông tin về bộ nhớ RAM và swap trên hệ thống của bạn. Dưới đây là các thông số mà lệnh "free" thường hiển thị:
1. **total**: Tổng dung lượng bộ nhớ RAM hoặc swap trên hệ thống (được hiển thị trong đơn vị KiB, Megabyte, hoặc Gigabyte).
2. **used**: Tổng dung lượng bộ nhớ đã được sử dụng.
3. **free**: Tổng dung lượng bộ nhớ còn trống.
4. **shared**: Dung lượng bộ nhớ được chia sẻ giữa các quy trình.
5. **buff/cache (buffers/cache)**: Dung lượng bộ nhớ đang được sử dụng cho bộ đệm (buffers) và cache. Các dữ liệu ở đây được sử dụng để tăng tốc độ truy cập vào ổ đĩa và giảm tải cho ổ đĩa.
6. **available**: Dung lượng bộ nhớ có sẵn để sử dụng cho các quy trình mới mà không cần phải sử dụng swap.

Thông thường, bạn có thể sử dụng các tùy chọn như "-h" để hiển thị kết quả dễ đọc hơn với các đơn vị lớn hơn như Megabyte hoặc Gigabyte. Ví dụ: "free -h"

![image](https://github.com/user-attachments/assets/ce69532d-8a29-43b2-99e7-34385193b2cd)


## watch

Lệnh "watch" trong Linux được sử dụng để thực hiện một lệnh hoặc một chuỗi các lệnh theo định kỳ, và hiển thị kết quả trên màn hình terminal. Khi bạn chạy lệnh "watch", nó sẽ thực hiện lệnh được chỉ định và hiển thị kết quả của lệnh đó trên màn hình terminal. Sau đó, nó sẽ làm mới và hiển thị kết quả mới sau mỗi khoảng thời gian được xác định.

Ví dụ, nếu muốn theo dõi mức sử dụng bộ nhớ của hệ thống mỗi 2 giây, sử dụng lệnh:
```
watch -n 2 free -m
```
Trong đó:

- **-n 2**: Định kỳ làm mới kết quả sau mỗi 2 giây.
- **free -m**: Là lệnh hiển thị thông tin về bộ nhớ hệ thống với tùy chọn "-m" để hiển thị kết quả dưới dạng Megabytes.

Lệnh trên sẽ liên tục hiển thị thông tin về bộ nhớ của hệ thống, được cập nhật sau mỗi 2 giây trên màn hình terminal.

![image](https://github.com/user-attachments/assets/b605284e-d7b8-4f84-a6b0-9ebe8eacdcf0)

## vmstat

Lệnh "vmstat" trong Linux được sử dụng để hiển thị thống kê về sử dụng bộ nhớ, CPU, và các tài nguyên hệ thống khác. "vmstat" thường cung cấp thông tin về các chỉ số quan trọng như sự sử dụng của CPU, sự sử dụng của bộ nhớ, sự hoạt động của bộ nhớ đệm (buffers) và bộ nhớ cache, và các thông tin về I/O.

Khi bạn chạy lệnh "vmstat" mà không có bất kỳ tùy chọn nào, nó sẽ hiển thị các dòng thông tin theo các đơn vị thời gian mặc định (thường là mỗi giây). Dưới đây là một số thông số thông thường mà "vmstat" hiển thị:

1. **procs**: Thông tin về quy trình (processes), bao gồm số lượng quy trình đang chạy, đang chờ, và đã kết thúc.
2. **memory**: Thông tin về sử dụng bộ nhớ, bao gồm sử dụng, tự do, cache, và buffers.
3. **swap**: Thông tin về sử dụng của vùng trao đổi (swap), bao gồm sử dụng và tự do.
4. **io**: Thông tin về hoạt động I/O (input/output), bao gồm số lần ghi và đọc từ đĩa cứng.
5. **system**: Thông tin về sự sử dụng CPU, bao gồm phần trăm thời gian CPU được sử dụng cho các quy trình người dùng và hệ thống.

Bạn cũng có thể sử dụng các tùy chọn với lệnh "vmstat" để điều chỉnh cách hiển thị thông tin, chẳng hạn như tùy chọn "-t" để hiển thị thời gian, hoặc "-n" để xác định số lượng lần hiển thị. Ví dụ: "vmstat -t 5" sẽ hiển thị thông tin vmstat mỗi 5 giây cùng với thời gian.

![image](https://github.com/user-attachments/assets/e407e988-2816-4810-bd81-5130a345f32e)

- Các cột trong kết quả của lệnh `vmstat` thường được phân chia thành các phần tương ứng với thông tin về các khía cạnh của hệ thống. Dưới đây là giải thích chi tiết cho từng cột:

1. **procs**: Thống kê về quá trình (processes).
   - **r**: Số lượng quy trình đang chạy hoặc đang đợi để được xử lý (run queue).
   - **b**: Số lượng quy trình đang bị chặn (blocked) vì chờ I/O hoặc vì bị chặn bởi một sự kiện khác.

2. **memory**: Thống kê về bộ nhớ.
   - **swpd**: Số lượng bộ nhớ được sử dụng trong phân vùng swap.
   - **free**: Số lượng bộ nhớ RAM tự do (free memory).
   - **buff**: Số lượng bộ nhớ được sử dụng cho buffers.
   - **cache**: Số lượng bộ nhớ được sử dụng cho cache.

3. **swap**: Thống kê về vùng trao đổi (swap).
   - **si**: Số lượng dữ liệu được ghi từ bộ nhớ vào phân vùng swap (swap in).
   - **so**: Số lượng dữ liệu được đọc từ phân vùng swap vào bộ nhớ (swap out).

4. **io**: Thống kê về hoạt động I/O (input/output).
   - **bi**: Số lượng lệnh ghi vào từ thiết bị lưu trữ.
   - **bo**: Số lượng lệnh ghi ra từ thiết bị lưu trữ.

5. **system**: Thống kê về hệ thống.
   - **in**: Số lượng lệnh được xử lý bởi kernel mỗi giây.
   - **cs**: Số lượng lệnh được xử lý bởi CPU mỗi giây.

6. **cpu**: Thống kê về việc sử dụng CPU.
   - **us**: Phần trăm thời gian CPU được sử dụng cho các quy trình người dùng.
   - **sy**: Phần trăm thời gian CPU được sử dụng cho các tác vụ hệ thống.
   - **id**: Phần trăm thời gian CPU không hoạt động (idle).
   - **wa**: Phần trăm thời gian CPU đang chờ đợi I/O hoàn thành (waiting).
   - **st**: Phần trăm thời gian CPU bị gián đoạn (stolen) bởi các máy ảo khác nếu hệ thống sử dụng công nghệ ảo hóa.

Dưới đây là một số tùy chọn phổ biến của lệnh `vmstat`:

1. **-a, --active**: Hiển thị thông tin về các phần của bộ nhớ mà đang được sử dụng và không được sử dụng.
  
2. **-d, --disk**: Hiển thị thông tin về hoạt động đĩa và I/O.

3. **-s, --stats**: Hiển thị thống kê tóm tắt về sự sử dụng bộ nhớ, swap, số lượng quy trình và các thông tin khác.

4. **-t, --timestamp**: Hiển thị thời gian cho mỗi dòng kết quả.

5. **-w, --wide**: Hiển thị thông tin chi tiết hơn, bao gồm các thông tin mở rộng về bộ nhớ và I/O.

6. **-n, --interval**: Đặt khoảng thời gian giữa các lần hiển thị (trong giây).

7. **-h, --help**: Hiển thị trợ giúp về các tùy chọn của lệnh `vmstat`.

Ví dụ, để hiển thị thống kê về sử dụng bộ nhớ mỗi 5 giây, bạn có thể sử dụng tùy chọn `-n` như sau: `vmstat -n 5`. Điều này sẽ làm 
mới kết quả mỗi 5 giây.

![image](https://github.com/user-attachments/assets/d53d2e3b-1dde-44bd-8b7b-deec2f7b3efc)

## iostat

Lệnh "iostat" trong Linux được sử dụng để hiển thị thông tin về hoạt động của thiết bị lưu trữ, như ổ đĩa cứng và các thiết bị khác. Nó cung cấp thông tin về tốc độ truy cập đĩa, tốc độ ghi, thời gian trung bình để xử lý một yêu cầu, và nhiều thông tin khác liên quan đến hiệu suất lưu trữ.

Dưới đây là một số tùy chọn phổ biến của lệnh "iostat":

1. **-c**: Hiển thị thống kê về CPU.
   
2. **-d**: Hiển thị thông tin về hoạt động của các thiết bị lưu trữ (disk).

3. **-h**: Hiển thị kết quả dễ đọc hơn bằng cách sử dụng các đơn vị đo lường lớn hơn như Megabyte hoặc Gigabyte.

4. **-k**: Hiển thị kết quả với đơn vị đo lường là Kilobyte.

5. **-m**: Hiển thị kết quả với đơn vị đo lường là Megabyte.

6. **-t**: Hiển thị thời gian giữa các lần làm mới.

7. **-x**: Hiển thị thêm thông tin chi tiết về các thiết bị lưu trữ.

Ví dụ, để hiển thị thông tin về hoạt động của các thiết bị lưu trữ mỗi 1 giây, bạn có thể sử dụng lệnh sau: 

```
iostat -d 1
```

Điều này sẽ hiển thị thống kê về các thiết bị lưu trữ mỗi giây.

## mbstat

Lệnh "mpstat" trong Linux được sử dụng để hiển thị thông tin về sử dụng CPU của các CPU đa lõi (multi-core) hoặc đa xử lý (multi-processor). Nó cung cấp thông tin chi tiết về hiệu suất CPU, bao gồm phần trăm thời gian CPU được sử dụng cho các tác vụ người dùng (user), hệ thống (system), và thời gian CPU không hoạt động (idle).

Khi chạy lệnh "mpstat" trong Linux, bạn sẽ nhận được các thông số đầu ra tương tự như sau:

```sh
Linux 5.4.0-91-generic (hostname)  05/11/24  _x86_64_  (8 CPU)

05:30:05 AM  CPU   %user   %nice %system %iowait  %steal   %idle
05:30:06 AM  all    3.56    0.00    0.67    0.00    0.00   95.77
```

Dưới đây là giải thích cho các thông số đầu ra:

1. **Linux 5.4.0-91-generic (hostname)  05/11/24  _x86_64_  (8 CPU)**: Thông tin về phiên bản hệ điều hành, tên máy chủ (hostname), kiến trúc hệ thống (x86_64), và số lượng CPU (8 CPU).

2. **05:30:05 AM**: Thời gian khi báo cáo được tạo ra.

3. **CPU**: Chỉ số CPU, "all" đại diện cho tất cả các CPU.

4. **%user**: Phần trăm thời gian CPU được sử dụng cho các quy trình người dùng.

5. **%nice**: Phần trăm thời gian CPU được sử dụng cho các quy trình có ưu tiên (nice).

6. **%system**: Phần trăm thời gian CPU được sử dụng cho các tác vụ hệ thống.

7. **%iowait**: Phần trăm thời gian CPU đang chờ đợi I/O hoàn thành.

8. **%steal**: Phần trăm thời gian CPU bị lấy đi bởi các máy ảo khác.

9. **%idle**: Phần trăm thời gian CPU không hoạt động.

Trong trường hợp trên, tổng thời gian idle của tất cả các CPU là 95.77%, tức là CPU đang không hoạt động nhiều. Phần còn lại của thời gian được chia thành các phần trăm sử dụng cho các mục đích khác nhau như quy trình người dùng, hệ thống, và các hoạt động khác.


## iftop

Lệnh "iftop" trong Linux là một tiện ích dòng lệnh được sử dụng để theo dõi lưu lượng mạng trên giao diện mạng cụ thể của máy tính. Khi bạn chạy lệnh "iftop" trong terminal, nó sẽ hiển thị một bảng theo thời gian thực với các thông tin về lưu lượng mạng đang được trao đổi qua các kết nối mạng.

Dưới đây là một số thông tin mà "iftop" thường hiển thị:

1. **TX**: Lưu lượng mạng gửi đi (tải lên) qua giao diện mạng.
2. **RX**: Lưu lượng mạng nhận về (tải xuống) qua giao diện mạng.
3. **TOTAL**: Tổng lưu lượng mạng (TX + RX).
4. **cumulative**: Lưu lượng mạng tích lũy từ lúc bắt đầu hoặc từ lần làm mới trước đó của "iftop".

Ngoài ra, "iftop" cũng hiển thị các thông tin về các kết nối mạng cụ thể, bao gồm địa chỉ IP nguồn và đích, cổng nguồn và đích, và lưu lượng mạng được trao đổi giữa các cặp kết nối.

Các lựa chọn thường được sử dụng với "iftop" bao gồm:
- **-i interface**: Chỉ định giao diện mạng cụ thể để theo dõi (ví dụ: eth0, wlan0).
- **-n**: Hiển thị địa chỉ IP thay vì phân giải tên miền.
- **-N**: Hiển thị số lượng gói tin thay vì số byte.
- **-F filter code**: Áp dụng một bộ lọc để chỉ hiển thị các kết nối phù hợp với điều kiện được xác định.
- **-B**: Hiển thị bảng tần số chứa các địa chỉ MAC.
- **-F**: Hiển thị lưu lượng mạng tăng dần.

Ví dụ, để theo dõi lưu lượng mạng trên giao diện mạng "eth0", bạn có thể chạy lệnh:

```
iftop -i eth0
```

Điều này sẽ hiển thị thông tin về lưu lượng mạng trên giao diện "eth0".

# nmon

Lệnh "nmon" là một tiện ích dòng lệnh mạnh mẽ được sử dụng để thu thập và hiển thị các thông tin chi tiết về hiệu suất hệ thống Linux trong thời gian thực. Nó cung cấp một giao diện dễ đọc và đồ họa, giúp người quản trị hệ thống hiểu rõ hơn về tình trạng của hệ thống và tìm ra các vấn đề về hiệu suất.

Khi bạn chạy lệnh "nmon" trong terminal, nó sẽ mở một giao diện dòng lệnh với các tab khác nhau, mỗi tab hiển thị thông tin về các chỉ số quan trọng như CPU, bộ nhớ, đĩa, mạng, và các thông tin hệ thống khác. Các chỉ số này thường được cập nhật liên tục để bạn có thể theo dõi hiệu suất hệ thống trong thời gian thực.

Dưới đây là một số thao tác phổ biến mà bạn có thể thực hiện khi sử dụng "nmon":

- Sử dụng các phím mũi tên để di chuyển giữa các tab khác nhau.
- Sử dụng phím "q" để thoát khỏi "nmon".
- Sử dụng phím "h" để hiển thị trợ giúp về các phím tắt.
- Sử dụng phím "s" để lưu thông tin nmon vào một file để xem sau.

Nmon cung cấp một cách mạnh mẽ để theo dõi và phân tích hiệu suất hệ thống Linux, đặc biệt là khi bạn cần theo dõi hệ thống trong thời gian thực và làm nhanh chóng các quyết định về tinh chỉnh hoặc tìm kiếm và giải quyết các vấn đề.

# htop

"htop" là một tiện ích dòng lệnh được sử dụng để hiển thị thông tin chi tiết về hoạt động của các tiến trình trên hệ thống Linux. Nó cung cấp một giao diện dễ đọc và tương tác, cho phép bạn theo dõi và quản lý các tiến trình một cách hiệu quả.

Khi bạn chạy lệnh "htop" trong terminal, nó sẽ mở một giao diện tương tác với các thông tin chi tiết về các tiến trình đang chạy trên hệ thống. Giao diện của "htop" thường chia thành các phần như sau:

1. **Thanh tiêu đề (Header Bar)**: Hiển thị thông tin về tên máy chủ, thời gian hoạt động của hệ thống, số lượng CPU, và tải trung bình.
  
2. **Danh sách các tiến trình (Process List)**: Hiển thị các tiến trình đang chạy trên hệ thống, với thông tin như ID của tiến trình (PID), tên của tiến trình, người dùng chạy tiến trình, tỷ lệ sử dụng CPU và bộ nhớ, và các thông tin khác.

3. **Các thanh công cụ và các phím tắt (Toolbar and Function Keys)**: Cung cấp các tùy chọn tương tác như tắt tiến trình, sắp xếp tiến trình theo các tiêu chí khác nhau, và các chức năng khác.

4. **Biểu đồ sử dụng CPU và bộ nhớ (CPU and Memory Usage Graphs)**: Hiển thị đồ thị dạng thanh biểu diễn sự sử dụng của CPU và bộ nhớ.

"htop" cung cấp một số phím tắt để tương tác với tiến trình và cải thiện trải nghiệm người dùng, bao gồm các phím tắt để sắp xếp và lọc tiến trình, thay đổi cách hiển thị và ẩn/hiện các cột thông tin, và thậm chí là tiến hành các hành động như tắt tiến trình.

Để thoát khỏi "htop", bạn có thể sử dụng tổ hợp phím "Ctrl + C" hoặc chỉ đơn giản là đóng cửa sổ terminal.



![](./images/Sreenshot_18.png)
