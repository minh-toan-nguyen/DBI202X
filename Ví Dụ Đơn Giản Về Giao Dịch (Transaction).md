### Ví Dụ Đơn Giản Về Giao Dịch (Transaction)

Trong hướng dẫn này, chúng ta sẽ xem một ví dụ đơn giản về giao dịch (transaction). Có hai điều cần lưu ý ngay từ đầu:

1. Những điều tôi sẽ chỉ cho bạn trong phần này chỉ áp dụng cho engine hỗ trợ giao dịch như InnoDB. MyISAM, một engine khác của MySQL, không hỗ trợ giao dịch.
2. Tôi sẽ trình bày thông tin theo cách đơn giản nhất có thể để bạn dễ hiểu và áp dụng.

### Tạo Bảng và Dữ Liệu Mẫu

Đầu tiên, tôi đã tạo một bảng tên là "books". Bạn có thể tạo bất kỳ bảng nào với các cột và dữ liệu tuỳ ý. Dưới đây là cách tạo bảng và thêm dữ liệu mẫu:

```sql
CREATE TABLE books (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255)
);

INSERT INTO books (name) VALUES ('The Journey'), ('The Mountain');
```

### Bắt Đầu Sử Dụng Giao Dịch

Khi sử dụng engine hỗ trợ giao dịch, mỗi lệnh thay đổi dữ liệu sẽ tự động chạy trong một giao dịch. Tuy nhiên, bạn có thể tắt tính năng auto commit để kiểm soát việc commit (cam kết) hoặc rollback (hoàn tác) thủ công.

**Tắt Auto Commit:**
```sql
SET autocommit = 0;
```

**Thêm Dữ Liệu và Kiểm Tra:**
```sql
INSERT INTO books (name) VALUES ('The Universe');

SELECT * FROM books;
```
Bạn sẽ thấy dữ liệu mới đã được thêm vào, nhưng thay đổi này chưa thực sự được cam kết vào cơ sở dữ liệu.

### Commit và Rollback

**Commit:**
```sql
COMMIT;
```
Khi bạn thực hiện lệnh COMMIT, tất cả các thay đổi kể từ lần commit cuối cùng sẽ được áp dụng vĩnh viễn vào cơ sở dữ liệu.

**Rollback:**
```sql
ROLLBACK;
```
Lệnh ROLLBACK sẽ hoàn tác tất cả các thay đổi kể từ lần commit cuối cùng.

### Ví Dụ Thực Tế

**Thêm và Xóa Dữ Liệu Sau Khi Tắt Auto Commit:**
```sql
-- Thêm dữ liệu mới
INSERT INTO books (name) VALUES ('The Universe');

-- Xóa dữ liệu
DELETE FROM books WHERE id = 1;

-- Thay đổi dữ liệu
UPDATE books SET name = 'The Mountain Version 2' WHERE id = 2;

-- Kiểm tra dữ liệu hiện tại
SELECT * FROM books;
```

**Rollback để Hoàn Tác Thay Đổi:**
```sql
ROLLBACK;

-- Kiểm tra lại dữ liệu sau khi rollback
SELECT * FROM books;
```
Bạn sẽ thấy rằng các thay đổi đã bị hoàn tác và dữ liệu quay trở lại trạng thái ban đầu.

### Kết Luận

Khi bạn tắt auto commit, bất kỳ thay đổi nào bạn thực hiện trên dữ liệu sẽ không thực sự áp dụng cho đến khi bạn thực hiện lệnh COMMIT. Nếu bạn muốn hoàn tác các thay đổi, bạn có thể sử dụng lệnh ROLLBACK. Điều này rất hữu ích trong việc đảm bảo tính nhất quán và an toàn dữ liệu trong các ứng dụng thực tế.

Hãy thử thực hành với các lệnh này để hiểu rõ hơn về cách chúng hoạt động. Trong các video tiếp theo, chúng ta sẽ tìm hiểu thêm về các ứng dụng phức tạp hơn của giao dịch. Hẹn gặp lại và chúc bạn lập trình vui vẻ!
