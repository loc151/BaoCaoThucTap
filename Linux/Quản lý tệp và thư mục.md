# Quản lý tệp và thư mục

## Cấu trúc hệ thống tệp: 
1. Một hoặc nhiều cây phân cấp thư mục và các tệp
- Tệp nhóm các bit
- Một thư mục dùng để tạo nhóm các tệp dữ liệu và thư mục

2. Thư mục gốc (root) (/) là điểm vào đầu tiên cho cả cây thư mục
3. Các tệp là các nút lá

## Các thư mục thông dụng trong Linux: 
- `/` (root): Thư mục tệp chương trình cơ bản
- `/boot` (Boot Loader Files): thư mục chứa hạt nhân (kernel) của hệ điều hành
- `/etc` (Configuration Files): thư mục chứa các tệp cấu hình
- `/dev` (Files device): thư mục chứa các tệp thiết bị
- `/home`: thư mục chứa dữ liệu của user
- `/lib` (System Libraies): Chứa các thư viện dùng chung cho các lệnh nằm trong `/bin` và `sbin`. Thư mục này cũng chứa các module của kernel
- `/usr` (User Programs): thư mục chứa những file cố định hoặc quan trọng để phục vụ tất cả người dùng. Chứa các ứng dụng, thư viện, tài liệu và mã nguồn các chương trình thứ cấp
- `/var`: thư mục chứa các tập tin ghi các số liệu biến đổi.
- `/bin` (User binaries) và `/sbin` (System binaries): Chứa những file cần thiết cho quá trình khởi động và những lệnh thiết yếu để duy trì hệ thống
- `/tmp` (Temporary Files): Thư mục chứa các file tạm thời
- `/srv` (Service Data): Chứa các service của máy chủ cụ thể liên quan đến dữ liệu

|Thư mục|Nội dung|
|---|---|
|/var/log|Hệ thống tập tin log|
|/var/lib|Các gói và các file dữ liệu|
|/var/mail|Email|
|/var/lock|Lock files|
|/var/tmp|Các file tạm thời khi cần reboot|
- `/proc`: chứa các tập tin ảo mà chỉ tồn tại trong bộ nhớ. Một số tập tin quan trọng:
```
/proc/cpuinfo
/proc/interrupts
/proc/meminfo
/proc/mounts
/proc/partitions
/proc/version
/proc/<process-id-#>
/proc/sys
```

## Đường dẫn và thư mục đặc biệt:
1. Truy cập tệp và thư mục cần dùng các đường dẫn
2. Đường dẫn có thể có mốc từ các thư mục đặc biệt:
- `/` : Thư mục gốc (root)
- `~/` : Thư mục nhà (home)
- `.` : Thư mục hiện tại
- `..` : Thư mục cha

## Quản lý thư mục: 
- `pwd`: Hiển thị đường dẫn tuyệt đối của thư mục hiện tại
- `cd`: thay đổi vị trí thư mục hiện tại sang thư mục được chỉ định
- `ls`: Liệt kê các tệp và thư mục trong thư mục hiện tại. Các tuỳ chọn trong lệnh ls:

|Tuỳ chọn|Ý nghĩa|
|----|----|
|-a|Hiển thị tất cả các tệp, bao gồm cả các tệp ẩn|
|-l|Hiển thị thông tin chi tiết về các tệp và thư mục, bao gồm quyền truy cập, số liên kết, chủ sở hữu, nhóm, kích thước, và thời gian sửa đổi cuối cùng|
|-lh|Hiển thị kích thước tệp ở định dạng dễ đọc (KB, MB, GB) khi sử dụng cùng với tùy chọn|
|-r|Hiển thị danh sách theo thứ tự ngược lại|
|-t|Sắp xếp các tệp theo thời gian sửa đổi, từ mới nhất đến cũ nhất|
|-S|Sắp xếp các tệp theo kích thước, từ lớn nhất đến nhỏ nhất|
|-R|Hiển thị đệ quy tất cả các tệp và thư mục con|
|-d|Hiển thị thông tin về thư mục thay vì nội dung của nó|
|-i|Hiển thị số inode của mỗi tệp|
|-F|Thêm ký tự đặc biệt vào cuối mỗi tên tệp để chỉ loại tệp (ví dụ: "/" cho thư mục, "*" cho tệp thực thi|
|--color|Hiển thị các tệp và thư mục với màu sắc khác nhau để dễ phân biệt|
  - Lưu ý: Lệnh `ls` có thể kết hợp nhiều tuỳ chọn để hiển thị thông tin theo ý muốn. Ví dụ: ls -alh, ls -lt

- `mkdir`: Tạo thư mục mới
- `rmdir`: Xoá thư mục rỗng

## Quản lý tệp:
- `touch`: Tạo tệp mới
- `cp`: Sao chép tệp
- `mv`: Di chuyển hoặc đổi tên tệp
- `rm`: Xoá tệp
- `cat`: Hiển thị nội dung tệp
- `less`: Hiển thị nội dung tệp với khả năng phân trang
- `head`: Hiển thị các dòng đầu tiên của tệp
- `tail`: Hiển thị các dòng cuối cùng của tệp
- `chmod`: Thay đổi quyền truy cập tệp
- `chown`: Thay đổi chủ sở hữu tệp
- `chgrp`: Thay đổi nhóm sở hữu tệp
