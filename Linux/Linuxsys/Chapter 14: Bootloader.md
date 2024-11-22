# Bootloader

Bootloader trong Linux là một chương trình được sử dụng để khởi động hệ điều hành Linux hoặc một hệ điều hành khác trên một máy tính. Nó thường được lưu trữ trong một vùng nhớ không gian đầu của ổ đĩa cứng (ví dụ: Master Boot Record - MBR) hoặc trong một phân vùng khởi động đặc biệt trên đĩa.

Các bootloader phổ biến nhất trong hệ thống Linux bao gồm:

1. **GRUB (GRand Unified Bootloader)**: Là bootloader phổ biến nhất trong hệ thống Linux. GRUB hỗ trợ nhiều hệ điều hành và cấu hình linh hoạt. Nó cung cấp giao diện dòng lệnh để chọn và khởi động các hệ điều hành khác nhau hoặc các môi trường khác nhau (như single-user mode, rescue mode).

2. **LILO (LInux LOader)**: Trước khi GRUB trở nên phổ biến, LILO là bootloader tiêu biểu cho Linux. Tuy nhiên, hiện nay nó ít được sử dụng hơn so với GRUB. LILO cũng hỗ trợ khởi động nhiều hệ điều hành và có cấu hình thông qua một tệp cấu hình.

3. **Syslinux**: Là một bootloader nhẹ, phổ biến trong môi trường như máy tính cá nhân, máy chủ và thiết bị nhúng. Nó thường được sử dụng để khởi động từ ổ đĩa USB hoặc qua mạng.

Công việc chính của bootloader là tải hệ điều hành từ ổ đĩa cứng vào bộ nhớ và chuyển quyền điều khiển cho hệ điều hành. Ngoài ra, bootloader cũng cung cấp các tùy chọn cấu hình, như chọn phiên bản hệ điều hành để khởi động, cài đặt thời gian chờ, và thậm chí khả năng sửa lỗi và phục hồi hệ thống.

## BIOS

BIOS là viết tắt của Basic Input/Output System, là một phần quan trọng của hệ thống máy tính được lưu trữ trên một chip ROM (Read-Only Memory) trên bo mạch chủ (motherboard). BIOS chịu trách nhiệm khởi động và khởi tạo phần cứng của máy tính khi nó được bật.

Công việc chính của BIOS bao gồm:

1. **Kiểm tra Power on self test (POST)**: BIOS thực hiện một loạt các kiểm tra tự động khi máy tính được bật để đảm bảo rằng các thành phần phần cứng như bộ nhớ, bàn phím, chuột, ổ đĩa, và các thành phần khác hoạt động đúng cách.

2. **Khởi động hệ thống**: Sau khi hoàn thành kiểm tra POST, BIOS tìm và khởi động bootloader từ ổ đĩa cứng hoặc thiết bị khởi động được chỉ định (ví dụ: ổ đĩa cứng, ổ đĩa USB, CD-ROM).

3. **Cấu hình hệ thống**: BIOS chứa các thông số cấu hình của hệ thống như thứ tự khởi động, các thiết bị phần cứng được nhận diện, và các cài đặt khác mà người dùng có thể điều chỉnh thông qua giao diện cấu hình BIOS.

4. **Thực hiện các chức năng cơ bản của hệ thống**: BIOS cung cấp các chức năng cơ bản cho hệ thống như đọc và ghi dữ liệu vào ổ đĩa, gửi dữ liệu đến màn hình, và quản lý thiết bị phần cứng.

Mặc dù BIOS đã được thay thế bởi UEFI (Unified Extensible Firmware Interface) trên nhiều hệ thống hiện đại, nhưng nó vẫn là một phần quan trọng của quá trình khởi động của máy tính truyền thống.
