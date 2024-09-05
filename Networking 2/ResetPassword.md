 ## 1. Reset Password switch Cisco
### Trường hợp 1: Nếu bạn muốn cấu hình lại thiết bị Switch từ một sw đã cấu hình từ trước, nhưng lại không có mật khẩu để vào switch; muốn xóa cả file config
### Trường hợp 2: Quên mật khẩu switch: muốn đặt lại pass nhưng không muốn mất cấu hình cũ trong switch.
- Không như router, đặt lại mật khẩu cho switch khác hẳn. Sau đây Lab sẽ hướng dẫn các bước để giải quyết các trường hợp trên.
  - Nguyên lý:
    - Khi ta boot switch vào chế độ ROM bằng cách giữ nút MODE
    - Thay đổi tên file lưu trữ cấu hình trong flash là config.text sang tên khác ví dụ như config.cu
    - Boot switch vào chế độ bình thường, vào chế độ Privilige và copy nội dung file cấu hình config.cu sang RAM
    - Thay đổi Password rồi ghi lại vào nvram
(nếu là áp dụng cho trường hợp 1 thì không cần 2 bước sau)

Yêu cầu:

B1: Kết nối Switch với PC qua cổng Console hoặc qua USB
– Trên PC có cài đặt phần mềm để kết nối dòng lệnh giống như Putty hoặc
SecureCRT… Trong trường hợp này sẽ dùng MobaXsterm

B2: Bật nguồn, trong khi đó, ta nhấn giữ nút MODE

Thực hiện lab:

Bước 1 – Tay nhấn vào nút MODE và tiến hành bật nguồn switch, giữ nút trong vòng khoảng 15s và thả ra

![image](https://github.com/user-attachments/assets/a2285f0a-588a-4f65-9939-12c1f2d2d95a)

Bước 2 –Ta sẽ nhìn thấy Switch hiển thị các thông tin trong chế độ ROM như sau:

```Boot Sector Filesystem (bs) installed, fsid: 2
Base ethernet MAC Address: 68:bd:ab:5c:0b:00
Xmodem file system is available.
The password-recovery mechanism is enabled.

The system has been interrupted prior to initializing the
flash filesystem. The following commands will initialize
the flash filesystem, and finish loading the operating
system software:

flash_init
boot
switch:
```
Bước 3 – ta nhập lệnh flash_init để nhận thiết bị flash
```
switch:flash_init
Initializing Flash…
flashfs[0]: 15 files, 1 directories
flashfs[0]: 0 orphaned files, 0 orphaned directories
flashfs[0]: Total bytes: 32514048
flashfs[0]: Bytes used: 23257088
flashfs[0]: Bytes available: 9256960
flashfs[0]: flashfs fsck took 9 seconds.
…done Initializing Flash.
```
![image](https://github.com/user-attachments/assets/1c30658b-bb61-4197-932d-6fb272a4b88d)

Bước 4 – Xem nội dung flash, mặc định file cấu hình của switch được lưu với tên config.text:

![image](https://github.com/user-attachments/assets/b8f65aa8-0836-4edc-91bc-2940377fe41a)

Bước 5: Nếu muốn xóa cả file cấu hình config.text này luôn, gõ lệnh:
```
delete flash:config.text
```
Còn nếu muốn chỉ thay mật khẩu mà giữ lại các cấu hình khác thì cần đổi tên file `config.text` sang tên khác

```
switch:rename flash:config.text flash:config.old
```
![image](https://github.com/user-attachments/assets/f17f27fe-9dcd-4e3e-b64d-c8aea1f7016c)

Bước 6 – Sau khi bạn đổi tên tệp `config.text` file sang `config.cu` ta xem lại nội dung flash bằng lệnh `dir flash:`

Sau khi đã đổi tên thành công ta boot vào switch bằng lệnh `boot`
![image](https://github.com/user-attachments/assets/3bc35ead-88f2-48e9-884a-f6d68e1fecbe)




Bước 7 — System Configuration Dialog —

`
Would you like to enter the initial configuration dialog? [yes/no]: no
`
`Switch>`

![image](https://github.com/user-attachments/assets/fc9fb518-5b4b-42ee-9981-b621207fae52)



Bước 8 vào chế độ 2 và copy nội dung file đã đổi tên vào RAM bằng lệnh 

`copy flash:config.old run`

```
Switch>enable
Switch#copy flash:config.old run
Destination filename [running-config]?
3436 bytes copied in 11.861 secs (290 bytes/sec)
```
![image](https://github.com/user-attachments/assets/138ab80c-a668-4218-97e6-6e0b92c4ed95)

Bước 9 – Sau khi ta copy nội dung file có chứa cấu hình vào running, cần đổi lại Password mới, nên đặt password cả 2 loại mã hóa (nếu cần) và ghi lại vào Nvram với lệnh copy run start.

```
Switch#configure terminal
Switch(config)#enable password NEWENABLEPASSWORD
Switch(config)#line 0
Switch(config-line)#password NEWCONSOLELINEPASSWORD
Switch(config-line)#end
Switch#copy run start
Destination filename [startup-config]?
Building configuration…
[OK]
0 bytes copied in 1.309 secs (0 bytes/sec)
```
