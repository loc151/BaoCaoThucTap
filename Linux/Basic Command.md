# 1. Lệnh cơ bản trên hệ thống
- `# exit` hoặc `# logout` : thoát ra khỏi trạng thái đăng nhập
- `# reboot`: Khởi động lại hệ thống
- `# ps`: Liệt kê các tiến trình đang hiện hành và PID (Process ID) của tiến trình đó.

![image](https://github.com/user-attachments/assets/c5de5aa5-3813-4f7e-875c-3eadd065deb8)

- `# sleep <thoi_gian>`: Cho phép hệ thống ngừng hoạt động trong một thời gian (thoi_gian tính bằng giây). Ví dụ `# sleep 6`, thì máy chủ sẽ tạm thời ngưng hoạt động trong 6 giây
- `# useradd <ten_user>`: Thêm 1 user vào hệ thống
- `# passwd <ten_user>`: Cập nhật mật khẩu cho user đã tạo. Ví dụ

![](./images/taouser.png)

> Sau khi tạo xong user ta thư mục home để kiểm tra user đã được thêm chưa

- `# who`: Cho biết user nào đang sử dụng hệ thống

![image](https://github.com/user-attachments/assets/f23fa4bf-16e0-42de-9627-3e7da23573eb)


- `# whoami`: Cho biết user nào đang đăng nhập

![image](https://github.com/user-attachments/assets/b8765f62-b9a2-4abb-a7ff-c845bfed6a98)


- `# top`: Hiển thị các tiến trình đang chạy trên hệ thống. Tương tự nhu task manager của window

- `# usermod -aG wheel <username>`: Cho phép user sử dụng quyền sudo
- `#su - <username>`: Đăng nhập bằng user khác

![](./images/lenhsu.png)

- Nhấn tổ hợp "ctrl + L" hoặc `# clear` đề làm sạch commandline
- `#ifconfig` : Xem địa chỉ IP của máy

![image](https://github.com/user-attachments/assets/1bb64d82-82fb-4007-99ee-f12af17731fa)

- `# history`: Để xem lịch sử các lệnh đã được thực thi bởi user hiện tại

![image](https://github.com/user-attachments/assets/32f92cda-1b24-4ee9-8a70-1e080a84bc8a)

- `# pwd`: Hiển thị đường dẫn tại nơi hiện hành

![image](https://github.com/user-attachments/assets/cccb2c75-5e0e-4fa4-a165-fbed655ac8bc)

- `# date`: Kiểm tra ngày giờ trên máy
- `free`: Kiểm tra RAM của máy
	+ -b: Hiển thị dưới dạng byte
	+ -k: Hiển thị dưới dạng Kb
	+ -m: Hiển thị dưới dạng Mb
	+ -g: Hiển thị dưới dạng Gb

![image](https://github.com/user-attachments/assets/0b6b66b8-fa2b-454d-b336-731c14a0fd3e)

- `# hostnamectl`: Xem thông tin hostname hiện tại của máy

![image](https://github.com/user-attachments/assets/51cf7d5d-e590-4458-8744-e830ea9e645b)

- `# uname`: Kiểm tra hệ điều hành đang sử dụng

![image](https://github.com/user-attachments/assets/5cecdc5d-8999-4b6a-8c99-3db1c33e55f0)

- `# yum update` hoặc `# apt update`: Cập nhật hệ thống
- `# init 0`: Tắt máy
- `# init 6`: Khởi động lại 
- `# w`: Kiểm tra các phiên SSH

![image](https://github.com/user-attachments/assets/e830f6b8-1f49-40bf-95a7-0844be910b89)

- `# df -h`: Hiển thị dung lượng ổ cứng của máy (dung lượng sẵn sàng và được sử dụng...)

![image](https://github.com/user-attachments/assets/a1c002f6-bba8-4782-b881-d3d4e814a5ec)

- `# df -i`: Hiển thị thông tin Inodes của máy (tổng số file đã tạo ra, số file còn có thể tạo, số file đã tạo...)

![image](https://github.com/user-attachments/assets/4d2d206b-2eb0-4e20-9429-676a49f420ee)

# 2. Thao tác với tập tin
- `# ls`: Xem danh sách các file và thư mục hiện hành

![image](https://github.com/user-attachments/assets/9a6dc7ec-4631-431e-928c-6694a8ebd114)

- `# ll`: Xem danh sách các file và thư mục hiện hành chi tiết

![image](https://github.com/user-attachments/assets/1b354304-ec01-4ed2-9b69-ebb4a4472d12)

- Chuyển thư mục (change directory): `# cd`
	+ cd /etc/selinux: Chuyển tới thư mục /selinux/
	+ cd: Chuyển về thư mục chính của người dùng
	+ cd A && ls: Chuyển tới thư mục A và hiển thị danh sách file và các thư mục của nó
	+ cd ..: Chuyển về thư mục cha của thư mục hiện tại

![image](https://github.com/user-attachments/assets/2330f74d-bcf3-481b-a7ba-75ce22f7d96e)

- Tạo 1 thư mục mới: `# mkdir <ten_thu_muc>`
- Tạo 1 tập tin: `# touch <ten_tap_tin>`
- Tạo 1 tập tin dạng text: `# echo "" >> ~/<ten_tap_tin>`
- Xóa tập tin: `# rm`
	+ `# rm <ten_tap_tin>`: Xóa 1 tập tin
	+ `# rm <tap_tin_1> <tap_tin_2>`: Xóa nhiều tập tin
	+ `# rm /a/b/c/<tap_tin>`: Xóa tập tin theo đường dẫn
	+ `# rm -i`: Xóa có xác nhận lại
	+ `# rm -f`: Xóa không xác nhận
	+ `# rm -I <ten_thu_muc>/file*`: Xóa hàng loạt file có cấu trúc file[...]
- Xóa thư mục: `# rmdir`
	+ `# rmdir <ten_thu_muc>`: hoặc `# rm -d`: Xóa 1 thư mục rỗng
	+ `# rm -r <ten_thu_muc>`: Xóa thư mục chứa các thư mục con và tập tin (có xác nhận cho từng đối tượng)
	+ `# rm -rf <ten_thu_muc>`: Xóa thư mục chứa các thư mục con và tập tin (không xác nhận)
- Mở tập tin: `# cat <tap_tin>` hoặc `# tail <tap_tin>`
- Khởi động trình soạn thảo VI:
	+ Câu lệnh `# vi <ten_file>`
	+ Nếu file chưa tồn tại thì hệ thống sẽ tạo ra file đó
	+ Nhấn phía "i" (Insert): Để chỉnh sửa văn bản
	+ Nhấn phím "ESC" để thoát khoải trạng thái nhập
	+ Nhập `:wq` (Để lưu lại file sửa đổi) hoặc `:q!` (Để thoát mà không lưu)
	+ Nhập `: <so_dong>`: Để chuyển đến dòng muốn tới
	+ Nhập `/ <tu_muon_tim_kiem>`: Để tìm kiếm trong file đó
- Khởi động trình soạn thảo nano:
	+ Câu lệnh `# nano <ten_file>`
	+ Nếu file chưa tồn tại thì hệ thống sẽ tạo ra file đó
	+ Trình soạn thảo có nhiều phím tắt để hỗ trợ thuận tiện hơn

![image](https://github.com/user-attachments/assets/34f425be-3b23-4020-810d-1a34a72744fe)

- Copy file: `# cp`
	+ Copy file A thành file B tại thư mục hiện hành
	```sh
	cp A.txt B.txt 
	```
	+ Copy nhiều file vào 1 thư mục khác. Ví dụ: Copy file A.txt, B.txt, C.txt, D.exe, E.exe vào thư mục tu vừa tạo
	```sh
	mkdir anhldl
	touch ./{A,B,C}.txt
	touch ./{D,E}.exe
	cp A.txt B.txt C.txt D.exe E.exe anhldl/
	```
	+ Copy file từ thư mục này sang thư mục khác. Ví dụ: Copy file A.txt từ thư mục tu sang thư mục B
	```sh
	mkdir B
	cp /anhldl/A.txt B
	```
	+ Để xem thông tin copy ta thêm `-v`. Ví dụ
	```sh
	cp -v A.txt B.txt C.txt D.exe E.exe anhldl/
	"A.txt" -> "anhldl/A.txt"
	"B.txt" -> "anhldl/B.txt"
	"C.txt" -> "anhldl/C.txt"
	"D.exe" -> "anhldl/D.exe"
	"E.exe" -> "anhldl/E.exe"
	```
	+ Để giữ nguyên thuộc tính file khi copy ta thêm `-p`. Các thuộc tính giữ nguyên là: access time, modification date, user ID, group ID, file flag, file mode, access control lists
	```sh
	cp -p /anhldl/A.txt B
	```
- Copy thư mục: tương tự file. Ta thêm `-a` hoặc `-r` 
	+ `-r`: Copy toàn bộ thư mục hoặc file con của thư mục được copy
	+ `-a`: Bao gồm option `-r` và thực hiện duy trì các thuộc tính của file hoặc folder như file mode, ownership, timestamps...
- Copy không cho ghi đè: thêm `-n`
- Copy cho ghi đè không cần xác định `-f`
- So sánh 2 tệp tin hoặc 2 thư mục `diff`
```sh
diff -c a.txt b.txt
```

![image](https://github.com/user-attachments/assets/8d49c979-89d9-45e6-97ff-f8d8e6f67c81)

- Xác định kiểu file: `# file <duong_dan_toi_file>`

![image](https://github.com/user-attachments/assets/cb7383c1-9fd1-40cf-b508-4a055093fa0c)

# 3. Lệnh nén và giải nén
- Các option dùng với lệnh `tar`
	+ `-c`: Tạo file nén.tar
	+ `-x`: Giải file nén .tar
	+ `-v`: Hiển thị quá trình nén và giải nén dữ liệu ra màn hình
	+ `-f`: Chỉ định nén thành file
	+ `-t`: Xem dữ liệu trong file nén
	+ `-j`: Tạo file nén với bzip2 có định dạng file.tar.bz2
	+ `-z`: Tạo file nén với gzip có định dạng file.tar.gz
	+ `-r`: Thêm một file và thư mục và file nén đã tồn tại
	+ `--wildcards`: Tìm và xuất file bất kỳ trong file nén
## 3.1 Các lệnh nén
- Nén file/thư mục sang định dạng "tar": `# tar -cvf`
	+ `# tar -cvf filenenA.tar /mnt/A` : Nén thư mục `A` thành `filenenA.tar` và show quá trình nén
- Nén file/thư mục sang định dạng "tar.gz": `# tar -cvzf`
	+ `# tar -cvfz filenenA.tar.gz /mnt/A`: Nén thư mục `A` thành `filenenA.tar.gz` và show quá trình nén
## 3.2 Các lệnh giải nén
- `tar -xvf filenenA.tar /mnt/A`
- `tar -xvfz filenenA.tar.gz /mnt/A`
- `tar -xvfj filenenA.tar.bz2 /mnt/A`
## 3.3. Thêm file và folder vào file nén
- Thêm file `abc.txt` vào `filenenA.tar`
	+ `# tar -rvf filenenA.tar abc.txt`
- Thêm thư mục `A` vào `filenenA.tar`
	+ `# tar -rvf filenenA.tar A`
# 4. File hệ thống
- Hệ thống tập tin của Linux được tổ chức theo 1 hệ thống phân bậc tương tự cấu trúc của 1 cây phân cấp. Bậc cao nhất là thư mục gốc, ký hiệu là "/" (root directory)
- Kiến trúc phân cấp của hệ thống file trong Linux

![](./images/cautrucphancap.png)

- `/bin` - User binaries và `sbin` - System binaries
	+ Chứa những file cần thiết cho quá trình khởi động và những lệnh thiết yếu để duy trì hệ thống
- `/dev` - Files device
	+ Chứa các định danh ánh xạ của thiết bị hoặc những file đặc biệt 
- `/etc` - Configuration Files
	+ Chứa các file cấu hình của hệ thống và nhiều chương trình tiện ích
- `/lib` - System Libraries
	+ Chứa các thư viện dùng chung cho các lệnh nằm trong `/bin` và `/sbin`. Và thư mục này cũng chứa các module của nhân.
- `/mnt` - Mount Directory
	+ Mount point mặc định cho những hệ thống file kết nối ra ngoài
- `/proc` - Mount Directory
	+ Chứa các thông tin về tiến trình hệ thống
- `/boot` - Boot Loader Files
	+ Chứa tập tin cấu hình cho quá trình khởi động của hệ thống
- `/home` - Thư mục Home
	+ Thư mục mặc dành cho người dùng khác root. Lưu trữ các tập tin cá nhân của tất cả user
- `/root` - Thư mục Root
	+ Thư mục mặc định của người dùng root
- `/tmp` - Temporary Files
	+ Thư mục chứa các file tạm thời
- `/usr` - User Programs
	+ Thư mục chứa những file cố định hoặc quan trọng để phục vụ tất cả người dùng
	+ Chứa các ứng dụng, thư viện, tài liệu và mã nguồn các chương trình thứ cấp
- `/var`
	+ Thư mục chứa các tập tin ghi các số liệu biến đổi
	+ Bao gồm: Hệ thống tập tin log `/var/log`, các gói và các file dữ liệu `/var/lib`, email `/var/mail`, print queues `/var/spool`, lock files `/var/lock`, các file tạm thời cần khi reboot `/var/tmp`
- `/media` - Removable Media Devices
	+ Gắn kết các thư mục tạm thời được hệ thống tạo ra khi một thiết bị lưu động (removable media)
- `/srv` - Service Data
	+ Chứa các service của máy chủ cụ thể liên quan đến dữ liệu
## 4.1 Hệ thống tập tin
Hệ thống linux gốc 'ext3', 'ext4', 'btrfs', 'xfs'. Trước khi sử dụng 1 hệ thống tập tin, phải gắn nó vào cây hệ thống tại `mountpoint`. Nên gắn vào thư mục trống.
- `mount`: Sử dụng để gắn vào cây tập tin
```sh
mount /dev/sd5a /mnt
```
> Đính kèm hệ thống tập tin có trong phân vùng đĩa được liên kết với dev/sd5a trên thiết bị vào cây tệp tin tại /mnt

- `unmount`: Tác các hệ thống tập tin từ điểm gắn
```sh
unmount /mnt
```

