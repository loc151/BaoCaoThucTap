# Các thao tác cơ bản với WebVirtCloud
## Thay đổi password admin:
- Tài khoản và Mật khẩu mặc định là admin/admin, vì vậy bước đầu tiên ta cần phải đổi ngay mật khẩu để nâng cao bảo mật
1. Tại giao diện của **WebVirtCloud**, chọn **Admin -> Profile**:
![image](https://github.com/user-attachments/assets/51f34451-f1fe-401e-86bc-16c0e13291ca)

2. Tại **Profile**, chọn **Change Password** để tiến hành đổi mật khẩu:
![image](https://github.com/user-attachments/assets/72c44501-a808-4e8b-a9fb-72b4d51d6f7d)

3. Nhập mật khẩu hiện tại và mật khẩu mới, chọn **Change** để hoàn thành.
![image](https://github.com/user-attachments/assets/aa27ae23-273c-4a37-a3a2-67cb0afdf7a8)

4. Giao diện hiển thị mật khẩu đã được đổi thành công:
![image](https://github.com/user-attachments/assets/99ce9598-4b55-415f-966c-b087dd05ff8b)

5. Kiểm tra xem mật khẩu đã được đổi chưa: Chọn **Logout** và đăng nhập lại với mật khẩu vừa thay đổi

## Tạo User: 
1. Tại giao diện **WebVirtCloud**, chọn **Users**:
![image](https://github.com/user-attachments/assets/c50b9483-6bee-454a-a133-ba8f355ff284)

2. Chọn dấu **+** để thêm user mới:
![image](https://github.com/user-attachments/assets/bdda7df6-8874-47af-87f9-1ee8e90f36ed)

3. Tại trang **Create User**, nhập các trường dữ liệu và phân quyền cho user đó:
![image](https://github.com/user-attachments/assets/e9f063a4-7d60-4e5c-b033-c2723ef4306f)

- Các quyền có thể cấp cho user:
  - **Can change password**: Cho phép người dùng thay đổi mật khẩu.
  - **Can clone instances**: Cho phép người dùng sao chép instances.
  - **Can access console without password**: Cấp quyền truy cập bảng điều khiển mà không cần mật khẩu.
  - **Can snapshot instances**: Cho phép người dùng snapshot các instances.
  - **Can view instances**: Cho phép người dùng xem các instances.
  
- Các lựa chọn về trạng thái:
  - **Staff status**: Chỉ ra liệu người dùng có thể đăng nhập vào trang quản trị hay không.
  - **Active**: Chỉ định liệu người dùng này có nên được hoạt động hay không. Bỏ chọn mục này thay vì xóa tài khoản.
  - **Superuser status**: Chỉ ra rằng người dùng này có tất cả các quyền mà không cần chỉ định rõ ràng.

## Tạo Storage Pool: 
- Tại giao diện WebVirtCloud, chọn **Computes -> chọn compute cần cấu hình -> "👁️"**
![image](https://github.com/user-attachments/assets/f7a7538a-7495-4365-bdb5-926da643304d)

- Chọn **Storages**:
![image](https://github.com/user-attachments/assets/075a8ea5-9d26-47dc-bc1c-351599b2d184)

- Chọn đường dẫn lưu images cho VMs:
![image](https://github.com/user-attachments/assets/1a0f8233-1441-4549-b6d3-35fed5a1b8fe)

- Sau khi cài đặt xong **Pools**:
![image](https://github.com/user-attachments/assets/9c524f0c-f90d-4ca1-b896-61962e27b80f)

![image](https://github.com/user-attachments/assets/bf11abaa-7297-4d01-a395-8212fd9088ed)

## Cài đặt Network:
- Tại Compute cần cấu hình, chọn **Network -> "➕"** để thêm **Networks**:
![image](https://github.com/user-attachments/assets/a7dc5e28-ed7f-4a13-b3a9-2233ac5fba88)

- Chọn tên mạng và mode network cần cấu hình:
![image](https://github.com/user-attachments/assets/74868a11-ee9a-4ec3-8822-c08c0bc17aab)

## Gán VM cho User:
- Nếu bạn là user admin bạn có toàn quyền nhưng nếu bạn là một user thường bạn chỉ có thể sử dụng VM do superuser hay còn gọi là admin gán quyền. Và bạn chỉ có thể thao tác với chính con VM đó chứ không phải là các computes chứa VMs.
- Tại giao diện **WebVirtCloud**, chọn **User -> người dùng cần thao tác**
![image](https://github.com/user-attachments/assets/72fa4043-e8f4-43b7-a4a0-bb4793587aec)

- Chọn **Create User Instance**, chọn User và Instance (VM) cùng với các quyền mà User đó có thể thao tác với VM:
![image](https://github.com/user-attachments/assets/fa04d7ae-511a-4dde-998b-11e4fbfe79fd)

- Nhấn "Save" để lưu lại

- Đăng nhập và tài khoản **locanh** và kiểm tra xem cấu hình đã được lưu hay chưa:
![image](https://github.com/user-attachments/assets/c0f77aaf-86cd-468f-a942-94579de40f43)

## Tạo VM: 
- Để thực hiện được bước tạo VM user, cần phải là user có quyền admin:
![image](https://github.com/user-attachments/assets/1a137110-fc38-44bf-8b0f-95334a9f0260)

- Lựa chọn compute:
![image](https://github.com/user-attachments/assets/84f8e0e0-8487-493d-82b3-51d817ceac28)

- Có thể tạo VM từ Flavor có sẵn hoặc Custom:
![image](https://github.com/user-attachments/assets/ff7fc9ea-1fae-47f3-b334-aa0be277b887)

- Nếu chọn **Flavor**, chọn các thông số cần thiết:
![image](https://github.com/user-attachments/assets/189cf6f0-49c9-454d-8e2b-def030e8f651)

- Tại **Settings**, chọn chế độ boot
![image](https://github.com/user-attachments/assets/a8c921c2-7972-4bcb-9efc-8c3d658c1f68)

- Chọn **Power on -> Console**, và tiến hành cài đặt máy ảo:
![image](https://github.com/user-attachments/assets/68af4d52-51db-4084-a1c9-f2ad5d0989b7)
