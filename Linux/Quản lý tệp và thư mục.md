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
![image](https://github.com/user-attachments/assets/f4e7053a-5afb-4df9-9cd6-70b62f99a429)

- `cp`: Sao chép tệp
- `mv`: Di chuyển hoặc đổi tên tệp
![image](https://github.com/user-attachments/assets/bfb578d2-0eaf-409c-8c74-22337d357b0f)

- `rm`: Xoá tệp
![image](https://github.com/user-attachments/assets/f543458f-0dfa-4b9f-8fbb-fe1562104226)

- `cat`: Hiển thị nội dung tệp
- `less`: Hiển thị nội dung tệp với khả năng phân trang
- `head`: Hiển thị các dòng đầu tiên của tệp
- `tail`: Hiển thị các dòng cuối cùng của tệp
- `chmod`: Thay đổi quyền truy cập tệp
![image](https://github.com/user-attachments/assets/3a89a7c5-8068-43cd-ba16-bb80735f1369)

- `chown`: Thay đổi chủ sở hữu tệp
- `chgrp`: Thay đổi nhóm sở hữu tệp

## File Permissions:
- Trong Linux mọi tệp đều liên kết với người dùng là chủ sở hũu. Mỗi tệp cũng được liên kết với 1 nhóm có liên quan đến tệp và các quyền hoặc quyền nhất định: đọc, viết, thực thi...
- Các tệp có 3 loại quyền: đọc(r), ghi(w), thực thi(x). 3 quyền này được đại diện theo thứ tự: Người dùng (User), nhóm (group), người dùng khác (other user).

|rwx: |rwx: |rwx:|
|---|---|---|
|u: |g:|o:|
- Ví dụ:
![image](https://github.com/user-attachments/assets/37d02fc4-d680-402d-a307-fc17f49cb75a)


-> Tại dòng locanh1
- `d`: Nghĩa là `locanh1` là 1 folder
- `rwx`: Là quyền của User. Ở đây User có đầy đủ 3 quyền là read (đọc), write (ghi) và excute (thực thi) 
- `rwx`: Là quyền của Group. Ở đây Group có đầy đủ 3 quyền là read (đọc), write (ghi) và excute (thực thi) 
- `r-x`: Là quyền của các User khác. Ở đây các User khác có 2 quyền là read (đọc) và excute (thực thi)
- `anhldl anhldl`: Các quyền ở trên là quyền của User anhldl và Group anhldl
-> Tại dòng locanh
- `-`: Nghĩa là `locanh` là 1 file
- `rw-`: Là quyền của User. Ở đây User có 2 quyền là read (đọc) và write (ghi)
- `rw-`: Là quyền của Group. Ở đây Group có 2 quyền là read (đọc) và write (ghi)
- `r--`: Là quyền của User khác. Ở đây các User khác có 1 quyền là read (đọc)
- `anhldl anhldl`: Các quyền ở trên là quyền của User anhldl và Group anhldl

- `ls -lah`: Kiểm tra đầy đủ thông tin của một file (bao gồm quyền)
- `chmod`: Thay đổi quyền truy cập của người dùng tới file/folder
## 5.1 Cấu trúc lệnh
### Thay đổi quyền của file và folder
```sh
chmod [options] [mode] file1 file2 file3 ...
```
- Các options: 
	+ `-R`: Recursive, áp dụng cho tất cả các file và folder bên trong
	+ `-f`: force, thay đổi quyền trong cả trường hợp xảy ra lỗi
	+ `-v`: verbose, hiển thị đối tượng đã xử lý
- Các mode:

|#|Permission|rwx|
|-|----------|---|
|7|read (2^2), write (2^1) and execute (2^0)|rwx|
|6|read (2^2) and write (2^1)|rw-|
|5|read (2^2) and execute (2^0)|r-x|
|4|read (2^2) only|r--|
|3|write (2^1) and execute (2^0)|-wx|
|2|write (2^1) only|-w-|
|1|execute (2^0) only|--x|
|0|none|---|
