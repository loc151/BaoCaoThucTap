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

- Cấu trúc của 1 dòng trong tệp **/etc/password**:
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

- Cấu trúc của một dòng trong tệp **/etc/shadow**:
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
- Tệp `**/etc/group**` trong Linux chứa thông tin về các nhóm người dùng trên hệ thống

![image](https://github.com/user-attachments/assets/502c5f77-d0bd-4fca-87ce-8e9e05762b71)

- Cấu trúc của một dòng trong tệp **/etc/group**:
```
group_name:password:GID:user_list
```

- Giải thích:
1. **group_name**: Tên của nhóm.
2. **password**: Mật khẩu của nhóm (thường để trống hoặc chứa ký tự x vì mật khẩu nhóm không thường được sử dụng).
3. **GID (Group ID)**: Số định danh duy nhất của nhóm. Có thể thấy số định danh này trong tệp `/etc/passwd`
4. **user_list**: Danh sách các thành viên của nhóm, được phân tách bằng dấu phẩy

## Tệp thông tin các nhóm: /etc/gshadow
- Tệp **/etc/gshadow** trong Linux chứa thông tin về các nhóm và mật khẩu nhóm. Đây là một tệp quan trọng để quản lý quyền truy cập nhóm và bảo mật hệ thống

![image](https://github.com/user-attachments/assets/02b8a951-dd9c-4097-9c05-03c7c3014dae)

- Cấu trúc của 1 dòng trong tệp **/etc/gshadow** :
```
group_name:password:admin:member
```

## Các lệnh hỗ trợ: 

1. **useradd**: Tạo user mới trên hệ thống
```
sudo useradd [options] username
```
- VD: tạo user mới với thư mục home cụ thể:
```
sudo useradd -m -d /home/loc151 loc151
```
- Giải thích:
  - `-m`: Tạo thư mục home cho user
  - `-d`: Chỉ định thư mục home cho user
 
2. **usermod**: Dùng để sửa đổi thông tin user hiện có:
```
sudo usermod [options] username
```
- VD: Thay đổi tên đăng nhập của user:
```
sudo usermod -l loc123 loc151
```

- Thêm người dùng vào nhóm `sudo`:
```
sudo usermod -aG sudo loc123
```

- Giải thích:
  - `-l`: Thay đổi tên đăng nhập của user
  - `-aG`: Thêm user vào các nhóm bổ sung
 
3. **userdel**: Xoá user khỏi hệ thống
```
sudo userdel [options] username
```

VD: Xoá user và thư mục home của họ: 
```
sudo userdel -r loc123
```
- `-r` xoá thư mục home của user cùng với tài khoản người dùng

4. **passwd**: Sử dụng để thay đổi mật khẩu của người dùng
```
sudo passwd [options] [username]
```
- Các tuỳ chọn:
  - `-l`: Khoá tài khoản user
  - `-u`: Mở khoá tài khoản user
  - `-d`: Xoá mật khẩu (cho phép đăng nhập không cần mật khẩu)

5. **gpasswd**: Sử dụng để quản lý mật khẩu và thành viên trong nhóm
```
gpasswd [options] groupname
```
- Ví dụ:
  - Thêm người dùng vào nhóm: `sudo gpasswd -a username groupname`
  - Xoá người dùng khỏi nhóm: `sudo gpasswd -d username groupname`
  - Xoá mật khẩu của nhóm: `sudo gpasswd -r groupname`

6. **groupadd**: Tạo nhóm mới trên hệ thống:
```
sudo groupadd [options] groupname
```

- Ví dụ: `-g GID`: chỉ định Group ID cho nhóm mới
```
sudo groupadd -g 1001 groupname
```

7. **groupmod**: Sửa đổi thông tin nhóm:
```
sudo groupmod [options] groupname
```

- Ví dụ:
  - Đổi tên nhóm: `sudo groupmod -n newname oldname`
  - Đổi GID nhóm: `sudo groupmod -g GID groupname'

8. **groupdel**: Xoá nhóm:
```
sudo groupdel groupname
```

9. **sg**: Sử dụng để thực thi một lệnh dưới quyền của một nhóm khác
```
sg groupname -c "command"
```

10. **newgrp**: Sử dụng để thay đổi nhóm hiện tại của người dùng trong một phiên làm việc mới. Khi sử dụng lệnh này, người dùng sẽ chuyển sang một nhóm khác và có thể thực thi các lệnh với quyền của nhóm đó
```
newgrp groupname
```

11. **su**: Sử dụng để chuyển đổi người dùng hiện tại sang một người dùng khác trong cùng một phiên làm việc. Tên lệnh su là viết tắt của "substitute user" hoặc "switch user". Khi sử dụng lệnh này, ta có thể thực hiện các tác vụ với quyền của người dùng khác mà không cần phải đăng xuất và đăng nhập lại
```
su [options] [username]
```

- Ví dụ:
  - Chuyển sang user **root**: `sudo root`
  - Chuyển sang user khác: `sudo username`
  - Chuyển sang môi trường đăng nhập của user mới, bao gồm các biến môi trường và thư mục nhà: `su - anhldl`
  - Thực thi một lệnh cụ thể dưới quyền của người dùng mới: `su -c "ls /root" root`

11. **users**: Hiển thị danh sách các người dùng hiện đang đăng nhập vào hệ thống
12. **groups**: Hiển thị danh sách các nhóm mà 1 người dùng cụ thể thuộc về
13. **id**: Sử dụng để hiển thị thông tin về người dùng hiện tại hoặc người dùng cụ thể, bao gồm User ID (UID), Group ID (GID), và các nhóm mà người dùng thuộc về.
```
id [options] [username]
```

- Ví dụ:
  - Hiển thị thông tin về user: `id username`
  - Hiển thị UID của user: `id -u`
  - Hiển thị GID của user: `id -g`
  - Hiển thị tất cả các GID của các nhóm mà user thuộc về: `id -G`
  - Hiển thị tên thay vì số ID: `id -un hoặc id -gn hoặc id -Gn`
![image](https://github.com/user-attachments/assets/d45d741d-5bda-465f-98a7-8e4f57d05bfc)

# Các quyền hạn:
## Mỗi file luôn thuộc về một người sử dụng và một nhóm xác định
- Người tạo ra file hoặc thư mục sẽ là người sở hữu, nhóm chứa người tạo ra file hoặc thư mục sẽ là nhóm sở hữu đối với file/thư mục.
- Sự phân quyền cho phép xác định rõ các quyền mà người sử dụng có đối với một file hoặc một thư mục.

## Quyền truy cập:
1. **r** : đọc (read)
- Cho phép hiển thị nội dung của file hoặc thư mục
2. **w** : ghi (write)
- Cho phép thay đổi nội dung của file
- Cho phép thêm hoặc xóa các file trong một thư mục
3. **x** : thực thi (execute)
- Cho phép thực thi file dưới dạng một chương trình
- Cho phép chuyển đến thư mục cần truy cập

## Các nhóm user: 
### Có 3 nhóm người sử dụng đối với 1 file/ thư mục:
- **u (user)** : người sở hữu duy nhất của file
- **g (group)** : những người sử dụng thuộc nhóm chứa file
- **o (others)** : những người sử dụng khác, không phải là người sở hữu file cũng như không thuộc nhóm chứa file.
=> Mỗi nhóm người sử dụng sẽ có một tập các quyền (r, w, x) xác định.

### Lưu ý: 
- Để có thể thêm các file, cần phải có quyền « w » đối với thư mục
- Để có thể xóa, thay đổi nội dung hoặc di chuyển 1 file, người sử dụng cũng cần phải có quyền « w » đối với thư mục
- Việc xóa một file còn phụ thuộc vào quyền đối với thư mục chứa file đó
- Để bảo mật các dữ liệu, người sở hữu file thậm chí có thể bỏ cả quyền đọc « r » đối với tất cả mọi người sử dụng khác.
- Để hạn chế quá trình truy cập vào hệ thống file, người sử dụng có thể bỏ quyền thực thi (x) đối với thư mục gốc của hệ thống file.

## Các quyền ngầm định của 1 file:
### Các quyền ngầm định của 1 file khi tạo ra có thể được xác định bằng lệnh "umask"
- `umask`: Sử dụng để thiết lập quyền mặc định cho các tệp và thư mục mới được tạo. Giá trị `umask` xác định các quyền sẽ bị loại bỏ khi tệp hoặc thư mục mới được tạo
- Ví dụ:
  - umask = 022
  - Quyền mặc định cho tệp: 666 (rw-rw-rw-)
  - Quyền thực tế: 666 - 022 = 644 (rw-r--r--)
![image](https://github.com/user-attachments/assets/e83b6f07-1892-40c1-97fe-b61a225966e4)

### Thay đổi chủ sở hữu và nhóm sở hữu của tệp hoặc thư mục: chown
```
chown [tùy chọn] chủ_sở_hữu[:nhóm_sở_hữu] tệp/thư_mục
```

- Tuỳ chọn: `-R`: Thay đổi chủ sở hữu và nhóm sở hữu của thư mục và tất cả các tệp bên trong

### Thay đổi nhóm sở hữu của tệp hoặc thư mục: chgrp
```
chgrp [tùy chọn] nhóm_sở_hữu tệp/thư_mục
```
