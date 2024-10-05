# Hướng Dẫn Di Chuyển Datastore của Máy Ảo Trên ESXi

Di chuyển một máy ảo từ datastore này sang datastore khác trên cùng một ESXi host có thể được thực hiện thông qua giao diện web của ESXi. Dưới đây là hướng dẫn chi tiết để thực hiện điều này.

## Bước 1: Đăng Nhập vào Giao Diện Web của ESXi
1. **Mở Trình Duyệt Web**:
   - Mở trình duyệt web và nhập địa chỉ IP của ESXi host để truy cập giao diện quản lý web.
2. **Đăng Nhập**:
   - Nhập tên người dùng và mật khẩu để đăng nhập vào giao diện web của ESXi.

## Bước 2: Tắt Máy Ảo
1. **Chọn Máy Ảo**:
   - Trong giao diện chính của ESXi, chọn tab **Virtual Machines**.

2. **Tắt Máy Ảo**:
   - Nhấp chuột phải vào máy ảo cần di chuyển và chọn **Power** > **Power Off**. Đợi máy ảo tắt hoàn toàn.
![image](https://github.com/user-attachments/assets/fd8e6dc1-0006-40f5-bca8-e84b6902a7ae)

## Bước 3: Di Chuyển Datastore
1. **Truy Cập Menu Storage**:
   - Trong giao diện chính, chọn tab **Storage** để xem danh sách các datastore hiện có.

2. **Chọn Datastore Nguồn**:
   - Chọn datastore hiện tại nơi máy ảo đang được lưu trữ.

3. **Chọn Thư Mục Máy Ảo**:
   - Trong datastore nguồn, chọn thư mục chứa máy ảo cần di chuyển.
![image](https://github.com/user-attachments/assets/e76ad0bd-8257-4fc7-8fd3-761e5007f377)

4. **Di Chuyển File Máy Ảo**:
   - Nhấp chuột phải vào thư mục hoặc các tệp của máy ảo và chọn **Move** hoặc **Copy**. Chọn datastore đích mà bạn muốn di chuyển máy ảo đến.
![image](https://github.com/user-attachments/assets/52f9e151-40ec-46b8-88c7-20b46814fb38)


5. **Xác Nhận Di Chuyển và theo dõi tiến trình hoàn thành**:
   - Xác nhận việc di chuyển hoặc sao chép các tệp của máy ảo sang datastore mới.

![image](https://github.com/user-attachments/assets/2e99335b-3028-443f-8678-416b6590d7b4)

![image](https://github.com/user-attachments/assets/3d074544-5694-4c21-b4cd-3aaf47202e6b)

## Bước 4: Đăng Ký Lại Máy Ảo

1. **Truy Cập Datastore Mới**:
   - Quay lại tab **Storage** và chọn datastore mới nơi máy ảo đã được di chuyển.

2. **Đăng Ký Máy Ảo**:
   - Vào thư mục chứa máy ảo mới trên datastore, nhấp chuột phải vào tệp cấu hình máy ảo (`.vmx`) và chọn **Register VM**.

![image](https://github.com/user-attachments/assets/f9436f18-3109-41ea-aac3-41a3c5d8f269)


## Bước 5: Bật Máy Ảo

1. **Bật Máy Ảo**:
   - Quay lại tab **Virtual Machines**, chọn máy ảo đã di chuyển, nhấp chuột phải và chọn **Power** > **Power On** để bật máy ảo.
   - Lúc này, ESXi sẽ hiển thị VM đã bị di chuyển hoặc sao chép, chọn `I Moved It` để tiếp tục
![image](https://github.com/user-attachments/assets/8b3d4cef-c275-4263-a5b9-e21cff660b34)

---

Với các bước trên, bạn đã hoàn thành việc di chuyển một máy ảo từ datastore này sang datastore khác trên cùng một ESXi host mà không cần sử dụng vCenter.
