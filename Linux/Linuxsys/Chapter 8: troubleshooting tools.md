# Troubleshooting tools

## 1. lsof
- Lệnh `lsof` là một công cụ mạnh mẽ trên các hệ điều hành Unix/Linux để liệt kê các tệp đang được mở bởi các tiến trình. Tên `lsof` đại diện cho "list open files" (liệt kê các tệp đã mở). Cú pháp cơ bản của lệnh `lsof` là:
```
lsof [options]
```

- `options`: Các tùy chọn để điều chỉnh đầu ra của `lsof`. Một số tùy chọn phổ biến bao gồm `-u` để chỉ định người dùng, `-i` để chỉ định cổng, `-c` để chỉ định tên của tiến trình, vv.

- Ví dụ, để hiển thị tất cả các tệp đang được mở trên hệ thống, bạn có thể sử dụng:

```
lsof
```

![image](https://github.com/user-attachments/assets/5393dca3-230a-424b-aaa5-feea7eb9cf18)

- Hoặc để liệt kê các tệp được mở bởi một người dùng cụ thể (ví dụ, `root`), sử dụng lệnh sau:

```
lsof -u root
```

![image](https://github.com/user-attachments/assets/560f7b2a-1eb7-4a08-a046-3aea58fe28f4)

- Để xem các kết nối mạng đang được sử dụng trên máy, sử dụng lệnh sau:
```
lsof -i
```

Hãy thử nghiệm các tùy chọn khác của `lsof` để tìm ra thông tin cụ thể mà bạn quan tâm. Lưu ý rằng việc sử dụng `lsof` đòi hỏi quyền truy cập root hoặc quyền sudo để hiển thị đầy đủ thông tin.


```sh
anhldl@anhldl:~$ sudo lsof | head -10
COMMAND     PID  TID TASKCMD               USER   FD      TYPE             DEVICE SIZE/OFF       NODE NAME
systemd       1                            root  cwd       DIR              253,0     4096          2 /
systemd       1                            root  rtd       DIR              253,0     4096          2 /
systemd       1                            root  txt       REG              253,0  1849992     796746 /usr/lib/systemd/systemd
systemd       1                            root  mem       REG              253,0   149760     797649 /usr/lib/x86_64-linux-gnu/libgpg-error.so.0.32.1
systemd       1                            root  mem       REG              253,0    27072     797591 /usr/lib/x86_64-linux-gnu/libcap-ng.so.0.0.0
systemd       1                            root  mem       REG              253,0   613064     797756 /usr/lib/x86_64-linux-gnu/libpcre2-8.so.0.10.4
systemd       1                            root  mem       REG              253,0   170456     797697 /usr/lib/x86_64-linux-gnu/liblzma.so.5.2.5
systemd       1                            root  mem       REG              253,0   841808     797846 /usr/lib/x86_64-linux-gnu/libzstd.so.1.4.8
systemd       1                            root  mem       REG              253,0  4455728     797596 /usr/lib/x86_64-linux-gnu/libcrypto.so.3

```

Câu lệnh (`sudo lsof | head -10`) sẽ hiển thị 10 dòng đầu tiên của kết quả của lệnh `lsof`. Dưới đây là giải thích của mỗi cột trong kết quả:

- **COMMAND**: Tên của tiến trình hoặc lệnh.
- **PID**: ID của tiến trình.
- **TID**: ID của luồng (thread) của tiến trình. Trường này thường để trống.
- **TASKCMD**: Tên của tiến trình cha hoặc câu lệnh gốc mà tiến trình được tạo ra từ đó.
- **USER**: Tên người dùng sở hữu tiến trình hoặc tệp.
- **FD**: File Descriptor, số mô tả tệp hoặc socket mà tiến trình đang sử dụng. 
- **TYPE**: Loại tài nguyên mà file descriptor đang tham chiếu đến.
- **DEVICE**: Thiết bị nơi tệp đang mở được lưu trữ.
- **SIZE/OFF**: Kích thước hoặc vị trí của tệp trong thiết bị.
- **NODE**: Số inode của tệp hoặc tài nguyên.
- **NAME**: Tên của tệp hoặc tài nguyên.

Trong trường hợp này, các dòng đầu tiên liệt kê thông tin về các tệp và thư mục được mở bởi tiến trình systemd, bao gồm cả thư mục làm việc hiện tại (`cwd`), tệp thực thi (`txt`), và các thư viện được sử dụng (`mem`).

## 2. fuser
- Lệnh `fuser` trong hệ điều hành Unix/Linux được sử dụng để xác định các tiến trình đang sử dụng hoặc có tệp được mở. Cụ thể, nó sẽ hiển thị ID của các tiến trình đang sử dụng tệp, thư mục hoặc thiết bị được chỉ định.

- Cú pháp cơ bản của lệnh `fuser` là:

```
fuser [options] [file|directory]
```

- `options`: Các tùy chọn để điều chỉnh hoặc mở rộng hành vi của lệnh.
- `file|directory`: Tệp hoặc thư mục mà bạn muốn kiểm tra các tiến trình đang sử dụng.

Một số tùy chọn phổ biến của `fuser` bao gồm:
- `-k`: Gửi tín hiệu kill đến các tiến trình đang sử dụng tệp hoặc thư mục.
- `-v`: Hiển thị đầu ra dưới dạng cơ bản (basic).
- `-u`: Hiển thị tên người dùng của các tiến trình thay vì ID tiến trình.
- `-m`: Xem xét tệp dưới dạng thiết bị.

Ví dụ, để xác định các tiến trình đang sử dụng tệp `file.txt`, bạn có thể sử dụng:

```
fuser file.txt
```

Hoặc để hiển thị tên người dùng của các tiến trình:

```
fuser -u file.txt
```


```sh
anhldl@anhldl:~$ vi A.txt

[1]+  Stopped                 vi A.txt
anhldl@anhldl:~$ fuser -m A.txt
/home/anhldl/A.txt:  3593rce  4506rce  4589rce  4590rce  4596rce  4601rce  4618rce
anhldl@anhldl:~$ fuser -m -u hello.txt
/home/anhldl/A.txt:  3593rce(anhldl)  4506rce(anhldl)  4589rce(anhldl)  4590rce(anhldl)  4596rce(anhldl)  4601rce(anhldl)  4618rce(anhldl)
```

Lệnh `fuser` rất hữu ích trong việc xác định và giải quyết các vấn đề liên quan đến việc các tiến trình có thể gây ra khi sử dụng các tệp hoặc thư mục cụ thể trên hệ thống của bạn.

## 3. iostat:
- Lệnh `iostat` là một công cụ dòng lệnh hữu ích để giám sát hiệu suất CPU và I/O của đĩa. Nó là một phần của gói sysstat và cung cấp thông tin chi tiết về việc sử dụng tài nguyên của hệ thống, giúp xác định các điểm nghẽn và tối ưu hóa hiệu suất.
- Cú pháp:
```
iostat [options] [devices] [interval] [count]
```
- Các tuỳ chọn phổ biến:
  - `-c`: Hiển thị thống kê CPU.
  - `-d`: Hiển thị thống kê I/O của đĩa.
  - `-x`: Hiển thị thống kê chi tiết về I/O của đĩa.
  - `-k`: Hiển thị thống kê với đơn vị kilobyte
  
- Cài đặt gói sysstat nếu chưa có trong máy chủ:
```
sudo apt-get install sysstat      # Debian/Ubuntu-based
sudo yum install sysstat          # RHEL/CentOS/Fedora-based
```

- Hiển thị thống kê cơ bản về CPU và I/O của đĩa: `iostat`
![image](https://github.com/user-attachments/assets/27cfba65-f2a8-48fb-b4e8-c166b8876280)

- Hiển thị thống kê với khoảng thời gian cập nhật: `iostat 5` . Lệnh này sau 5 giây sẽ cập nhật trạng thái:
![image](https://github.com/user-attachments/assets/340cec19-bc1b-4d23-9117-8a6e13635f67)

- Hiển thị thống kê cho một thiết bị cụ thể: `iostat -d /dev/sda`
![image](https://github.com/user-attachments/assets/f0329f55-431e-4189-9b44-7d99f44477f4)

- Giải thích các trường dữ liệu ở đầu ra của lệnh:
- **CPU Statistics**:
  - `%user`: Phần trăm thời gian CPU dành cho các tiến trình người dùng.
  - `%nice`: Phần trăm thời gian CPU dành cho các tiến trình người dùng với giá trị nice dương.
  - `%system`: Phần trăm thời gian CPU dành cho các tiến trình hệ thống.
  - `%iowait`: Phần trăm thời gian CPU chờ đợi các hoạt động I/O hoàn thành.
  - `%idle`: Phần trăm thời gian CPU không hoạt động.

- **Devices Statistics**:
  - `Device`: Tên thiết bị (ví dụ: sda, sdb).

  - `tps`: Số lần chuyển mỗi giây (yêu cầu I/O) gửi đến thiết bị.

  - `kB_read/s`: Số kilobyte đọc từ thiết bị mỗi giây.

  - `kB_wrtn/s`: Số kilobyte ghi vào thiết bị mỗi giây.

