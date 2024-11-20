# System Information

## THÔNG TIN VỀ PHIÊN BẢN VÀ HĐH
### 1. Xem và thay đổi thông tin hostname của hệ thống
- Câu lệnh: `# hostnamectl`
- Lệnh này sẽ hiển thị thông tin chi tiết về tên máy chủ, icon-name, kernel và nhiều thông tin khác.

![image](https://github.com/user-attachments/assets/4ff08960-2113-4479-bb60-e32026ece367)

- Để thay đổi hostname, dùng câu lệnh: 
```
hostnamectl set-hostname new-hostname#
```

2. Hiển thị phiên bản của Linux
- Câu lệnh: `# cat /etc/*release`
- Lệnh này sẽ đọc và hiển thị nội dung của các tập tin trong thư mục /etc/ có tên chứa thông tin về phiên bản hệ điều hành.

![image](https://github.com/user-attachments/assets/b1f2423a-1cf0-49b2-bc5d-de725cb53efe)

3. Hiển thị thông tin về kernel của hệ thống.
- Để hiển thị những thông tin về kernel của hệ thống ta sử dụng câu lệnh **uname**
- Câu lệnh: `# uname -a`
- Lệnh này sẽ hiển thị tất cả thông tin chi tiết kernel và hệ thống

![image](https://github.com/user-attachments/assets/7466a6ee-cd84-4634-a627-926f2ca018df)

- Các tùy chọn khác phổ biến của lệnh **uname**
	- **uname -a**: Hiển thị tất cả các thông tin về kernel, bao gồm tên máy chủ, kernel name, version, release, machine, và platform.

	- **uname -s** hoặc **uname --kernel-name**: Chỉ hiển thị tên kernel.

	- **uname -r** hoặc **uname --kernel-release**: Hiển thị phiên bản của kernel.

	- **uname -v** hoặc **uname --kernel-version**: Hiển thị thông tin về phiên bản kernel và các thông tin mô tả khác.

	- **uname -m** hoặc **uname --machine**: Hiển thị thông tin về kiến trúc của máy (như x86_64 cho máy 64-bit).

	- **uname -o** hoặc **uname --operating-system**: Hiển thị tên hệ điều hành.

![image](https://github.com/user-attachments/assets/bcb2286f-d89e-4e42-b7c8-873e878c223d)

## THÔNG TIN VỀ PHẦN CỨNG
### 1. Hiển thị thông tin về CPU
- Câu lệnh: `lscpu`

![image](https://github.com/user-attachments/assets/cf7a03be-0b27-4595-8037-f70b32782730)

- Trong đó: 
  - **Architecture**: Kiến trúc của CPU (ví dụ: x86_64).
  - **CPU op-mode(s)**: Chế độ hoạt động của CPU (ví dụ: 32-bit, 64-bit).
  - **Byte Order**: Thứ tự byte của CPU (ví dụ: Little Endian, Big Endian).
  - **CPU(s)**: Số lượng CPU có sẵn trên hệ thống.
  - **Thread(s) per core**: Số luồng trên mỗi lõi.
  - **Core(s) per socket**: Số lõi trên mỗi socket.
  - **Socket(s)**: Số lượng socket CPU trên hệ thống.
  - **NUMA node(s)**: Số lượng NUMA node.
  - **Vendor ID**: ID của nhà sản xuất CPU.
  - **CPU family, model, và stepping**: Thông tin chi tiết về gia đình, mô hình và bước của CPU.
  - **CPU MHz**: Tốc độ xung nhịp của CPU.
  - **CPU max MHz, min MHz**: Giá trị tối đa và tối thiểu của tốc độ xung nhịp của CPU.
  - **CPU flags**: Các cờ hỗ trợ bởi CPU như SSE, AVX, ...
  - **Virtualization**: Hỗ trợ ảo hóa của CPU.
  - **L1/L2/L3 cache**: Kích thước của bộ nhớ cache.

### 2. Liệt kê các thông tin về ổ đĩa và phân vùng.
- **df**: Hiển thị thông tin về không gian đĩa đã sử dụng và còn trống trên các phân vùng đĩa.
- Câu lệnh : `# df -h`

![image](https://github.com/user-attachments/assets/844b3cb2-4752-446e-8e1a-3ee860bf6a23)

- Trong đó: 
	- **Filesystem**: Tên hệ thống tập tin hoặc đường dẫn đến phân vùng.
	- **Size**: Kích thước tổng của phân vùng.
	- **Used**: Số lượng không gian đã sử dụng.
	- **Available**: Số lượng không gian còn trống.
	- **Use%**: Phần trăm không gian đã sử dụng so với tổng không gian.
	- **Mounted on**: Đường dẫn mà phân vùng được gắn kết (mounted) vào hệ thống tập tin.

- Các tùy chọn phổ biến của lệnh **df**:
	- **-h, --human-readable**: Hiển thị kích thước dễ đọc cho con người (tính bằng MB, GB, ...).
	- **-T, --print-type**: Hiển thị kiểu hệ thống tập tin của các phân vùng.
  ![image](https://github.com/user-attachments/assets/0ff94785-c119-4198-9b69-cd106dd8df4c)

	- **-a, --all**: Hiển thị thông tin của tất cả các hệ thống tập tin, bao gồm cả các hệ thống tập tin ảo.
  ![image](https://github.com/user-attachments/assets/8e12b94e-87f3-45f1-8807-494db24ce475)

	- **-i, --inodes**: Thay vì hiển thị thông tin về không gian đĩa, hiển thị thông tin về số lượng inode đã sử dụng và còn trống trên phân vùng.
  ![image](https://github.com/user-attachments/assets/ade345c6-9c47-406f-b69c-5dd73d82b9e2)

	- **--total**: Hiển thị tổng cộng của tất cả các số liệu.
  ![image](https://github.com/user-attachments/assets/0bceabe6-b7a3-422c-b28c-d42ff70879ac)

- **lsblk**:  Liệt kê các thiết bị lưu trữ và các phân vùng trên hệ thống
- Câu lệnh: `lsblk`

![image](https://github.com/user-attachments/assets/a8a00cf6-ca27-46c6-87db-ca1e3c71dbb8)

- Trong đó:
	- **NAME**: Tên thiết bị hoặc phân vùng.
	- **MAJ:MIN**: Số hiệu (major và minor) của thiết bị.
	- **RM**: Số thứ tự (đối với các thiết bị có thể gỡ ra, như ổ đĩa USB).
	- **SIZE**: Kích thước của thiết bị hoặc phân vùng.
	- **RO**: Chế độ chỉ đọc (Read-Only) - '0' nếu không, '1' nếu có.
	- **TYPE**: Loại thiết bị hoặc phân vùng (disk, part - phân vùng, rom - đĩa CD/DVD).
	- **MOUNTPOINT**: Đường dẫn nơi thiết bị hoặc phân vùng được gắn kết (mounted) vào hệ thống tập tin.

- Các tùy chọn phổ biến với lệnh **lsblk**
	- **-a, --all**: Hiển thị tất cả các thiết bị, bao gồm cả các thiết bị loop và ram.
  ![image](https://github.com/user-attachments/assets/4ecc9af4-c4ed-410f-b69f-2f0a08e68644)

	- **-d, --nodes**: Không hiển thị các thiết bị con (các phân vùng của thiết bị).
  ![image](https://github.com/user-attachments/assets/cee775fb-a34e-4613-a8d4-5fe0f9c944f8)

	- **-o, --output list**: Chỉ định các cột cụ thể để hiển thị (ví dụ: lsblk -o NAME,SIZE,TYPE,MOUNTPOINT).
  ![image](https://github.com/user-attachments/assets/8ac78b0c-4947-4d5f-a7cb-13d06e7974d4)

	- **-p, --pairs**: Hiển thị đầu ra dưới dạng cặp key-value.
  ![image](https://github.com/user-attachments/assets/002db409-33a8-496d-ac83-ad7811168650)

	- **-r, --raw**: Hiển thị dữ liệu nguyên thủy mà không sắp xếp cột theo định dạng ASCII.
  ![image](https://github.com/user-attachments/assets/e89cb4cf-5baa-48c2-8f57-2a603a090539)

	- **-S, --scsi**: Hiển thị thông tin với định dạng SCSI.
  ![image](https://github.com/user-attachments/assets/c129ea12-1ecc-4c6b-b563-83d3e09e350a)

	- **-t, --fs**: Hiển thị thông tin về hệ thống tập tin trên các phân vùng.
  ![image](https://github.com/user-attachments/assets/d93c1da5-fdba-4831-bbfb-dd9206cb20c4)

	- **-h, --help**: Hiển thị trợ giúp về các tùy chọn của lệnh.

- **fdisk** Đây là các công cụ dùng để quản lý phân vùng đĩa. Có thể sử dụng chúng để xem thông tin chi tiết về các phân vùng.
- Câu lệnh: `fdisk -l`
- Trong đó: `-l` để hiển thị thông tin về các ổ đĩa cùng các phân vùng 

![image](https://github.com/user-attachments/assets/7ba98f36-83e5-4670-b80f-e6044275b40f)

- Trong đó: 
	- **Disk /dev/sdX**: Tên thiết bị ổ đĩa (vd: /dev/sda, /dev/nvme0n1).
	- **Disk identifier**: Định danh duy nhất của ổ đĩa.
	- **Device Boot**: Chỉ định xem phân vùng có khả năng khởi động không.
	- **Start**: Địa chỉ bắt đầu của phân vùng (trong sectors).
	- **End**: Địa chỉ kết thúc của phân vùng (trong sectors).
	- **Sectors**: Số lượng sectors của phân vùng.
	- **Size**: Kích thước của phân vùng.
	- **Type**: Kiểu phân vùng (Linux, NTFS, EFI, v.v.).
	- **Id**: Mã định danh kiểu phân vùng (ví dụ: 83 - Linux, 7 - NTFS).
	- **Boot**: Đánh dấu xem phân vùng có thể khởi động hay không.
	- **System**: Hệ thống tập tin của phân vùng (ví dụ: ext4, swap).

### 3. Hiển thị thông tin về bộ nhớ RAM
- Câu lệnh: `free -h`

![image](https://github.com/user-attachments/assets/defa5b9c-4ed2-4e74-9254-c2c85fa20b12)

- Trong đó: 
	- **total**: Tổng dung lượng bộ nhớ RAM và swap.
	- **used**: Dung lượng bộ nhớ đã được sử dụng.
	- **free**: Dung lượng bộ nhớ còn trống và chưa được sử dụng.
	- **shared**: Dung lượng bộ nhớ được chia sẻ giữa các tiến trình.
	- **buff/cache**: Dung lượng bộ nhớ được sử dụng cho bộ đệm (buffer) và bộ nhớ cache. Bộ đệm thường chứa dữ liệu đã được đọc từ đĩa, 	- **trong khi** bộ nhớ cache chứa dữ liệu được sử dụng gần đây.
	- **available**: Dung lượng bộ nhớ có sẵn để sử dụng mà không cần phải swap.

- Các tùy chọn phổ biến của lệnh **free**
	**-b, --bytes**: Hiển thị dung lượng bộ nhớ dưới dạng bytes.
	**-k, --kilo**: Hiển thị dung lượng bộ nhớ dưới dạng kilobytes (KB).
	**-m, --mega**: Hiển thị dung lượng bộ nhớ dưới dạng megabytes (MB).
	**-g, --giga**: Hiển thị dung lượng bộ nhớ dưới dạng gigabytes (GB).
	**-h, --human**: Hiển thị dung lượng bộ nhớ dưới dạng dễ đọc cho con người (ví dụ: KB, MB, GB).
	**-t, --total**: Hiển thị tổng cộng của các số liệu.
	**-s, --seconds <delay>**: Hiển thị thông tin về bộ nhớ sau mỗi khoảng thời gian <delay> giây.
	**-c, --count <count>**: Hiển thị thông tin về bộ nhớ theo số lần lặp lại <count>.

![image](https://github.com/user-attachments/assets/775a5bd2-a794-427e-b959-04ced8dc18a4)

## THÔNG TIN VỀ MẠNG
1. Hiển thi thông tin về địa chỉ IP và giao diện mạng 
- Câu lệnh: `# ip addr show`
- Lệnh này sẽ hiển thị danh sách các giao diện mạng và các địa chỉ gồm: địa chỉ ip, địa chỉ MAC,..

![image](https://github.com/user-attachments/assets/2f417ba7-1091-47c1-b61c-5672b7b6c2c8)

2. Kiểm tra kết nội mạng với một địa chỉ ip hoặc tên miền 
- Câu lệnh: `ping <địa_chỉ_tên_miền>`

![image](https://github.com/user-attachments/assets/5d50c233-da6d-4f06-9341-53650432a5a2)

- Tùy chọn phổ biến của lệnh **ping**
	- **-c <số lần>**: Xác định số lượng gói tin để gửi đi trước khi dừng quá trình ping
  ![image](https://github.com/user-attachments/assets/b3654ee9-1c9d-40d0-ae64-86c899335f06)

	- **-s <kích thước>**: Chỉ định kích thước gói tin được gửi đi (trong byte).
	- **-i <số giây>**: Thiết lập thời gian chờ giữa các gói tin ping.
	- **-w <thời gian>**: Đặt thời gian chờ để nhận phản hồi (timeout).
	- **-q**: Chế độ im lặng, chỉ hiển thị kết quả cuối cùng sau khi hoàn thành.
  ![image](https://github.com/user-attachments/assets/b0b93aa4-229a-444c-baf5-ed3375dc4e72)

	- **-v**: Chế độ verbose, hiển thị thông tin chi tiết hơn về quá trình ping.
	- **-t**: Ping liên tục đến khi bị dừng bằng cách sử dụng Ctrl + C.
	- **-f**: Gửi các gói tin ping với cờ "don't fragment".
	- **-n**: Hiển thị kết quả ping với địa chỉ IP (không thử phân giải tên miền).
	- **-R**: Gửi các gói tin ping có chứa thông tin route.

![image](https://github.com/user-attachments/assets/dadbd549-044e-4d26-bf51-5be1c8b2bc79)

## THÔNG TIN VỀ LOG
1. Xem log của hệ thống
- Câu lệnh: `journalctl`

![image](https://github.com/user-attachments/assets/f7540d71-18a2-4c6c-8099-4b3712a9578c)

