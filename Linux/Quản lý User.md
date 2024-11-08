# Quản lý người sử dụng

## Khái niệm:
1. **Root User**: Người dùng có quyền cao nhất trên hệ thống, có thể thực hiện mọi thao tác mà không bị hạn chế. **Root User** thường được sử dụng để thực hiện các tác vụ quản trị hệ thống
2. **Regular User**: Người dùng thông thường, có quyền hạn chế hơn so với root user. Mỗi regular user có một tài khoản riêng và chỉ có thể truy cập vào các tệp và thư mục mà họ có quyền.
3. **System User**: Tài khoản người dùng được tạo ra để chạy các dịch vụ hệ thống. Các tài khoản này thường không có quyền đăng nhập vào hệ thống.

## Quản lý User: 
1. **Tạo người dùng mới**: `sudo adduser username`

![image](https://github.com/user-attachments/assets/b5d07634-0bc3-4ddb-8c80-9d252697cd28)

2. **Xoá người dùng**: `sudo deluser username`
3. **Thay đổi mật khẩu người dùng**: `sudo passwd username`
4. **Liệt kê tất cả người dùng**: `cat /etc/passwd`

## Tệp thông tin các user: /etc/password

![image](https://github.com/user-attachments/assets/b521dbf1-72a5-48cf-8a4a-90d0dea0adf6)

- Cấu trúc của 1 dòng trong tệp /etc/password:
```
Username:Password:UID:GID:Info:Home:Shell
```
- Giải thích các trường dữ liệu của 1 user:
1. **Username = locanh**: Là tên đăng nhập của người dùng. Tên người dùng trong khoảng 1-32 ký tự 
2. **Password = x**: Mật khẩu. Ký tự `x` cho biết mật khẩu được lưu trữ trong tệp `/etc/shadow`
3. **UID = 1000**: Mỗi người dùng phải được chỉ định một ID người dùng (UID). UID 0 (số không) được dành riêng cho root và UID 1-99 được dành riêng cho các tài khoản được xác định trước khác. UID 100-999 tiếp theo được hệ thống dành riêng cho các tài khoản/nhóm quản trị và hệ thống.
4. **GID = 1000**: ID nhóm chính (thường được lưu trong tệp /etc/group)
5. **Info = anhldl**: Thông tin người dùng (User ID Info). Trường này thường chứa thông tin bổ sung về người dùng, chẳng hạn như tên đầy đủ, số điện thoại, ...
6. **Home = /home/anhldl**: Thư mục nhà (Home Directory). Đây là đường dẫn đến thư mục cá nhân của người dùng, nơi lưu trữ các tệp và cấu hình cá nhân. Nếu thư mục này không tồn tại thì thư mục người dùng sẽ trở thành /
7. **Shell = /bin/bash**: Đường dẫn tuyệt đối của lệnh hoặc shell mà người dùng sẽ sử dụng khi đăng nhập (/bin/bash). Thông thường, đây là một shell. Lưu ý rằng nó không nhất thiết phải là một shell.

## Tệp thông tin về mật khẩu: /etc/shadow
- Tệp `/etc/shadow` trong Linux chứa thông tin về mật khẩu của người dùng. Đây là một tệp quan trọng để bảo mật hệ thống, vì nó lưu trữ các mật khẩu đã được mã hóa và các thông tin liên quan đến mật khẩu.

![image](https://github.com/user-attachments/assets/8dfceac1-9165-45e8-9677-7a63fc867cb0)

- Cấu trúc của một dòng trong tệp /etc/shadow:
```
User:Pwd:Last pwd change:Minimum:Maximum:Warn:Inactive:Expire
```
- Giải thích:
1. **User**: Tên đăng nhập của người dùng.
2. **Password**: Mật khẩu đã được mã hóa. Nếu trường này chứa ký tự * hoặc !, tài khoản sẽ bị khóa.
3. **Last pwd change**: Số ngày kể từ ngày 1/1/1970 mà mật khẩu được thay đổi lần cuối.
4. **Minimum**: Số ngày tối thiểu giữa các lần thay đổi mật khẩu.
5. **Maximum**: Số ngày tối đa mà mật khẩu có hiệu lực trước khi người dùng phải thay đổi mật khẩu.
6. **Warn**: Số ngày trước khi mật khẩu hết hạn mà người dùng sẽ nhận được cảnh báo.
7. **Inactive**: Số ngày sau khi mật khẩu hết hạn mà tài khoản sẽ bị vô hiệu hóa.
8. **Expire**: Số ngày kể từ ngày 1 tháng 1 năm 1970 mà tài khoản sẽ bị vô hiệu hóa.

# Nhóm người sử dụng (Group):
## Mỗi người sử dụng có thể thuộc về một hoặc nhiều nhóm
- Một nhóm = tên nhóm + danh sách các thành viên
- Khả năng chia sẻ các file giữa những người sử dụng trong cùng một nhóm.
- Danh sách các nhóm được lưu trữ trong file: `/etc/group`
- root có khả năng tạo ra các nhóm bổ sung, ngoài các nhóm mà hệ điều hành đã ngầm định

## Tệp thông tin các nhóm: /etc/group
- Tệp `/etc/group` trong Linux chứa thông tin về các nhóm người dùng trên hệ thống

![image](https://github.com/user-attachments/assets/502c5f77-d0bd-4fca-87ce-8e9e05762b71)

- Cấu trúc của một dòng trong tệp /etc/group:
```
group_name:password:GID:user_list
```

- Giải thích:
1. **group_name**: Tên của nhóm.
2. **password**: Mật khẩu của nhóm (thường để trống hoặc chứa ký tự x vì mật khẩu nhóm không thường được sử dụng).
3. **GID (Group ID)**: Số định danh duy nhất của nhóm. Có thể thấy số định danh này trong tệp `/etc/passwd`
4. **user_list**: Danh sách các thành viên của nhóm, được phân tách bằng dấu phẩy

## Tệp thông tin các nhóm: /etc/gshadow
- Tệp /etc/gshadow trong Linux chứa thông tin về các nhóm và mật khẩu nhóm. Đây là một tệp quan trọng để quản lý quyền truy cập nhóm và bảo mật hệ thống

![image](https://github.com/user-attachments/assets/02b8a951-dd9c-4097-9c05-03c7c3014dae)

- Cấu trúc của 1 dòng trong tệp 
