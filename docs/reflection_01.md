1. Khó khăn khi cài Docker/DBeaver và cách bạn xử lý?
Tôi không có khó khăn gi khi cài Docker/DBeaver.

2. Vì sao chọn data type như vậy cho tiền tệ / thời gian / ID? Cho 1 ví dụ cụ thể.
- Lý do chọn NUMERIC/DECIMAL cho tiền tệ
	- Nếu chọn INT: Có thể phù hợp với các loại tiền tệ không có giá trị thập phân như VND, nhưng sẽ không phù hợp với các loại tiền tệ có giá trị thập phân như USD (ví dụ 19.99 USD).
	- Nếu chọn FLOAT: FLOAT dễ tạo ra sai số với các giá trị thập phân.
	=> NUMERIC/DECIMAL là sự lựa chọn hợp lý khi loại dữ liệu này có khả năng lưu trữ và xử lý các giá trị thập phân với độ chính xác cao.
- Lý do chọn TIMESTAMP cho thời gian: Đảm bảo độ chính xác về mặt thời gian.
- Lý do chọn INT cho ID: ID sử dụng số nguyên => INT là loại dữ liệu phù hợp.

3. Mối quan hệ 1:N giữa customers và orders? Vẽ/kể 1 ví dụ 1 customers có N orders
1 customer có thể có nhiều order. Ví dụ:
- Ngày 15/09/2026: Anh Nguyễn Văn A đặt mua chiếc Iphone 17 Pro Max -> Đơn hàng này sẽ được tính là 1 order.
- Ngày 16/09/2026: Anh Nguyễn Văn A đặt mua ốp cho chiếc Iphone 17 Pro Max -> Đơn hàng này sẽ được tính là 1 order khác.
Như vậy, chỉ trong 2 ngày 15/09/2026 và 16/09/2026 anh Nguyễn Văn A đã có 2 order.

4. Nếu schema cần sửa sau này (thêm cột, đổi FK) thì xử lý thế nào (ALTER vs Tạo lại)?
TRƯỜNG HỢP 1: DATABASE CHƯA CÓ DỮ LIỆU, CHƯA ĐI VÀO HOẠT ĐỘNG, MỚI CHỈ NẰM Ở DẠNG ERD
- Trong trường hợp này, nếu việc tạo lại database có thể giúp cho quá trình vận hành sau này đơn giản, dễ nâng cấp hơn thì nên tạo lại, còn nếu chỉ thêm/sửa những yếu tố đơn giản thì có thể ALTER.
TRƯỜNG HỢP 2: DATABASE ĐÃ CÓ DỮ LIỆU VÀ ĐANG HOẠT ĐỘNG
- Việc phải thay đổi/nâng cấp database trong quá trình vận hành hệ thống là không thể tránh khỏi, phương án là kết hợp song song giữa ALTER và Tạo lại, trong đó ALTER để giải quyết các vấn đề cần đáp ứng trước mắt, còn 1 phần nguồn lực sẽ được chia ra để nghiên cứu kiến trúc database mới.
GIẢI PHÁP HIỆN TẠI
Chọn phương án của trường hợp 1, lúc này database mới chỉ ở dạng schema, chưa có dữ liệu, nếu việc tạo lại giúp cho quá trình vận hành sau này trở nên đơn giản hơn thì sẽ ưu tiên chọn phương án tạo lại.
