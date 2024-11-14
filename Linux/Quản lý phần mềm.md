# Quản lý phần mềm

## Nguyên tắc quản lý phần mềm:
1. Các thành phần của 1 phần mềm:
- File thực hiện
- Các thư viện phần mềm
- Các file cấu hình
- Dữ liệu tạm thời

2. Các thao tác quản lý phần mềm
- Cài đặt phần mềm
- Gỡ bỏ phần mềm
- Cấu hình lại phần mềm
- Lấy thông tin về phần mềm

3. Cách thức quản lý:
- Độc lập
- Script cho từng phần mềm
- Quản lý bằng CSDL chung
- Công cụ quản lý chung

- Có 2 lựa chọn quản lý gói : 'dpkg' và 'rpm'. Hai hệ thống không tương thích nhưng cung cấp các tính năng giống nhau ở mức độ rộng rãi.

|High Level Tool|Low Level Tool|Family|
|---------------|--------------|------|
|zypper|rpm|SUSE|
|yum|rpm|Red Hat|

## Quản lý các gói phần mềm:
- Cả 2 hệ thống quản lý gói cung cấp 2 mức công cụ:
	+ Công cụ cấp thấp (ví dụ như `dpkg`hay `rpm`), sẽ chăm sóc các chi tiết của giải nén gói cá nhân, chạy các kịch bản, nhận được các phần mềm được cài đặt một cách chính xác
	+ Một công cụ cấp cao (ví dụ `apt-get`, `yum` hoặc `zypper`) hoạt động với các nhóm gói, tải gói từ nhà cung cấp và tìm ra các phụ thuộc
- Cài đặt một gói duy nhất có thể dẫn đến hàng chục thậm chí hàng trăm gói phụ thuộc được cài đặt

|Operation|RPM|Debian|
|---------|-----------|-----------|
|Cài đặt 1 package|rpm –i package.rpm|dpkg --install package.deb|
|Cài đặt 1 package từ repository|yum install package|apt-get install package|
|Xóa một package|rpm –e package.rpm|dpkg --remove package.deb|
|Xóa một package lấy từ repository|yum remove package|apt-get remove package|
|Update một package tới phiên bản mới hơn|rpm –U package.rpm|dpkg --install package.deb|
|Update 1 package sử dụng repository và resolving dependencies|yum update package|apt-get upgrade package|
|Update toàn bộ hệ thống|yum update|apt-get dist-upgrade|
|Hiển thị tất cả các package đã cài đặt|yum list installed|dpkg --list|
|Nhận thông tin về các package được cài đặt bao gồm các file|rpm –qil package|dpkg --listfiles package|
|Hiển thị các package có sẵn với "package" trong tên|yum list package|apt-cache search package|
|Hiển thị tất cả các package có sẵn|yum list|apt-cache dumpavail|
|Hiển thị package có chứa "file"|rpm –qf file|dpkg --search file|
