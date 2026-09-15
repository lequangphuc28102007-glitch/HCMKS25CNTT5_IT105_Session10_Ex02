# TỔNG HỢP BÀI TẬP SEQUENCE DIAGRAM – RIKKEI

**Ngày hoàn thành:** 15/09/2026  
--
 
## BÀI 2: TÌM LỖI VÀ SỬA SƠ ĐỒ – CHỨC NĂNG THANH TOÁN RIKKEIBANK

### 1. Mục tiêu

- Phân biệt Sync và Async
- Phát hiện lỗi Self và Return
- Hiểu hậu quả khi chọn sai loại thông điệp

### 2. Hai lỗi của thực tập sinh
+ Lỗi 1 – Bước 2: Kiểm tra định dạng thẻ

- Thực tập sinh vẽ sai: Async gửi sang một Lifeline khác (tự tạo thêm đối tượng không có trong kịch bản).
- Vì sao sai: Đây là xử lý nội bộ của chính Cổng Thanh Toán.
- Hậu quả: Thiết kế thừa đối tượng, logic bị đẩy ra ngoài, khó bảo trì.
- Loại đúng: Self (mũi tên vòng cung trên chính lifeline Cổng Thanh Toán).

+ Lỗi 2 – Bước 6: Gửi email hóa đơn

- Thực tập sinh vẽ sai: Sync sendReceiptEmail() + có Return đi kèm.
- Vì sao sai: Kịch bản quy định “không được chờ EmailServer phản hồi”.
- Hậu quả: Nếu EmailServer chậm → toàn bộ luồng thanh toán bị treo (timeout không cần thiết).
- Loại đúng: Async (mũi tên nét liền đầu hở, không có Return).