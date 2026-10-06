USE demo;

-- Procedure 1: Lấy user theo ID
DELIMITER $$
CREATE PROCEDURE get_user_by_id(IN user_id INT)
BEGIN
    SELECT users.name, users.email, users.country
    FROM users
    WHERE users.id = user_id;
END$$ DELIMITER ;  -- Procedure 2: Thêm mới user DELIMITER $$
CREATE PROCEDURE insert_user(
    IN user_name VARCHAR(50),
Dưới đây là tổng hợp chi tiết bài thực hành **"Gọi MySQL Stored Procedures từ JDBC"** theo đúng các bước bạn đã chuẩn bị, cùng với đoạn script tự động hóa hoàn chỉnh dành cho AI Agent hoặc Terminal.

---

## 📌 Bảng tóm tắt các thay đổi trong dự án

| Thành phần | Tệp tin / Công cụ | Thao tác thực hiện |
| :--- | :--- | :--- |
| **Database** | MySQL Workbench / Terminal | Tạo 2 thủ tục: `get_user_by_id` và `insert_user`. |
| **DAO Interface** | `IUserDAO.java` | Khai báo phương thức `getUserById(int id)` và `insertUserStore(User user)`. |
| **DAO Impl** | `UserDAO.java` | Thực thi 2 phương thức trên bằng `CallableStatement` (`{CALL ...}`). |
| **Controller** | `UserServlet.java` | Chuyển đổi gọi hàm trong `showEditForm()` và `insertUser()`. |

---

## 💻 Chi tiết các đoạn mã thực thi

### 1. MySQL Stored Procedures

```sql
USE demo;

-- Procedure 1: Lấy User theo ID
DELIMITER $$
DROP PROCEDURE IF EXISTS get_user_by_id$$
CREATE PROCEDURE get_user_by_id(IN user_id INT)
BEGIN
    SELECT users.name, users.email, users.country
    FROM users
    WHERE users.id = user_id;
END$$
DELIMITER ;

-- Procedure 2: Thêm mới User
DELIMITER $$
DROP PROCEDURE IF EXISTS insert_user$$
CREATE PROCEDURE insert_user(
    IN user_name VARCHAR(50),
    IN user_email VARCHAR(50),
    IN user_country VARCHAR(50)
)
BEGIN
    INSERT INTO users(name, email, country)
    VALUES(user_name, user_email, user_country);
END$$
DELIMITER ;
