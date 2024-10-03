# Snapshot (trong ESXi): là 1 bản sao của tệp đĩa máy ảo (VMDK) tại 1 thời điểm nhất định. Nó ghi lại trạng thái của máy ảo, bao gồm cả bộ nhớ, các tệp đĩa và các thiết lập cấu hình:

## Lợi ích của Snapshot:
1. **Phục hồi nhanh chóng**: Giúp khôi phục máy ảo về trạng thái trước đó nếu xảy ra sự cố
2. **Thử nghiệm và phát triển**: Dễ dàng thử nghiệm các cấu hình mới mà không lo mất dữ liệu
3. **Tiết kiệm thời gian**: Tránh phải cài đặt lại máy ảo từ đầu khi gặp lỗi

## Lưu ý khi sử dụng snapshot: 
1. **Không nên giữ snapshot quá lâu**: Snapshot có thể chiếm nhiều dung lượng lưu trữ và ảnh hưởng đến hiệu suất
2. **Sử dụng snapshot cho các mục đích ngắn hạn**: Không nên sử dụng snapshot như 1 giải pháp sao lưu dài hạn

