# Quản trị viên Linux sử dụng `at` để lên lịch các công việc một lần. Các công việc định kỳ được lên lịch tốt hơn với `cron`. Hai phần tiếp theo sẽ thảo luận về cả hai công cụ.

## A. Lệnh `at`:
```
at [times]
```

### 1. Lên lịch thực hiện 1 lệch vào 1 thời điểm cụ thể:


# Cron

Cron là một dịch vụ quản lý thời gian trong hệ thống Unix và Linux, cho phép lên lịch cho việc thực hiện các tác vụ tự động vào các thời điểm cụ thể hoặc theo lịch trình định kỳ. Dịch vụ cron sử dụng một tệp cấu hình được gọi là "crontab" để định rõ các tác vụ cần thực hiện và thời gian chúng sẽ được thực hiện.

`crontab` là một công cụ dòng lệnh được sử dụng trong hệ điều hành Unix và Linux để quản lý và chỉnh sửa crontab của người dùng. Crontab là một tệp cấu hình chứa các tác vụ được lên lịch để thực hiện tự động vào các thời điểm cụ thể.

Dưới đây là một số chức năng cơ bản của `crontab`:

1. **Xem crontab hiện tại**: Sử dụng lệnh `crontab -l` để xem nội dung của crontab hiện tại của người dùng.

2. **Chỉnh sửa crontab**: Sử dụng lệnh `crontab -e` để mở crontab hiện tại trong trình soạn thảo mặc định và chỉnh sửa nội dung của nó.

3. **Xóa crontab**: Sử dụng lệnh `crontab -r` để xóa toàn bộ crontab của người dùng.

4. **Nhập crontab từ tệp**: Sử dụng lệnh `crontab file` để nhập crontab từ một tệp cụ thể. Điều này sẽ ghi đè crontab hiện tại của người dùng.

5. **In ra định dạng crontab**: Sử dụng lệnh `crontab -l > file` để ghi ra crontab hiện tại vào một tệp cụ thể.

6. **Tùy chọn khác**: Ngoài các tùy chọn cơ bản, `crontab` cũng hỗ trợ các tùy chọn khác như `-u` để chỉ định người dùng cụ thể.

Với `crontab`, người dùng có thể lên lịch cho các tác vụ như sao lưu dữ liệu, chạy các tác vụ hằng ngày, hàng tuần hoặc hàng tháng, và thực hiện các công việc định kỳ khác mà không cần can thiệp thủ công. Điều này giúp tự động hóa các quy trình hệ thống và làm giảm công sức của người quản trị hệ thống.

## Thời gian trong crontab

Trong crontab, thời gian được thiết lập sử dụng năm cột đại diện cho phút, giờ, ngày trong tháng, tháng và ngày trong tuần. Mỗi cột này có các giá trị được phân tách bằng dấu cách hoặc ký tự tab.

Dưới đây là cách thiết lập thời gian trong crontab:

1. **Phút (Minute)**: Cột đầu tiên trong crontab đại diện cho phút. Các giá trị có thể từ 0 đến 59 hoặc sử dụng dấu sao (*) để chỉ định mọi giá trị phút.

2. **Giờ (Hour)**: Cột thứ hai đại diện cho giờ. Các giá trị có thể từ 0 đến 23 hoặc sử dụng dấu sao (*) để chỉ định mọi giá trị giờ.

3. **Ngày trong tháng (Day of Month)**: Cột thứ ba đại diện cho ngày trong tháng. Các giá trị có thể từ 1 đến 31 hoặc sử dụng dấu sao (*) để chỉ định mọi giá trị ngày trong tháng.

4. **Tháng (Month)**: Cột thứ tư đại diện cho tháng. Các giá trị có thể từ 1 đến 12 hoặc sử dụng dấu sao (*) để chỉ định mọi giá trị tháng.

5. **Ngày trong tuần (Day of Week)**: Cột cuối cùng đại diện cho ngày trong tuần, với 0 đại diện cho Chủ nhật và các giá trị từ 1 đến 6 đại diện cho thứ Hai đến thứ Bảy. Bạn cũng có thể sử dụng dấu sao (*) để chỉ định mọi giá trị ngày trong tuần.

Ví dụ, để lên lịch cho một tác vụ chạy vào mỗi ngày lúc 2 giờ sáng, bạn có thể sử dụng:

```
0 2 * * * command_to_execute
```

Trong đó:
- "0" đại diện cho phút 0.
- "2" đại diện cho giờ 2 sáng.
- Dấu sao (*) được sử dụng cho các cột còn lại để chỉ định mọi giá trị phù hợp.
- "command_to_execute" là lệnh hoặc tác vụ mà bạn muốn thực hiện.


## Ví dụ

```sh
crontab -e
```

![](./images/Sceenshot_8.png)


Sử dụng `crontab -l` để xem nội dung các crontab 

```sh
ngocnd@web02:~$ crontab -l
# Edit this file to introduce tasks to be run by cron.
#
# Each task to run has to be defined through a single line
# indicating with different fields when the task will be run
# and what command to run for the task
#
# To define the time you can provide concrete values for
# minute (m), hour (h), day of month (dom), month (mon),
# and day of week (dow) or use '*' in these fields (for 'any').
#
# Notice that tasks will be started based on the cron's system
# daemon's notion of time and timezones.
#
# Output of the crontab jobs (including errors) is sent through
# email to the user the crontab file belongs to (unless redirected).
#
# For example, you can run a backup of all your user accounts
# at 5 a.m every week with:
# 0 5 * * 1 tar -zcf /var/backups/home.tgz /home/
#
# For more information see the manual pages of crontab(5) and cron(8)
#
# m h  dom mon dow   command

0 3 * * 1 /path/to/weekly_report.sh


# Moi gio, ghi nhat ky he thong vao tep syslog.log
@hourly /usr/sbin/syslogd -n > /var/log/syslog.log

# Moi thang vao ngay 1 luc 0 gio, chay lenh cleanup de don dep he thong

0 0 1 * * /usr/local/bin/cleanup
```
