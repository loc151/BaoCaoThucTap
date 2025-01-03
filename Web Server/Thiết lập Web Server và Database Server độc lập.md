
# **Hướng dẫn thiết lập Web Server và Database Server độc lập**

## **Mục tiêu**
Thiết lập:
- **Web Server**: Chạy Nginx + PHP để hiển thị nội dung web và truy vấn dữ liệu.
- **Database Server**: Chạy MySQL/MariaDB để lưu trữ dữ liệu và phục vụ các truy vấn từ Web Server.

---

## **1. Yêu cầu hệ thống**
- Hai máy chủ:
  - **Web Server**: IP `172.16.2.197`
  - **Database Server**: IP `172.16.2.95`
- Hệ điều hành: Ubuntu 20.04 hoặc tương đương.
- Quyền truy cập root hoặc sudo.

---

## **2. Thiết lập Web Server**

### **2.1 Cài đặt Nginx**
Trên Web Server:
```
sudo apt update
sudo apt install nginx -y
```

Khởi động và bật Nginx khi khởi động:
```
sudo systemctl start nginx
sudo systemctl enable nginx
```

### **2.2 Cài đặt PHP**
Cài đặt PHP và các module cần thiết:
```
sudo apt install php-fpm php-mysql -y
```

Kiểm tra PHP đã được cài đặt:
```
php -v
```

### **2.3 Cấu hình Nginx**
Tạo file cấu hình Nginx cho trang web:
```
sudo nano /etc/nginx/sites-available/testsite
```

Thêm nội dung sau:
```
server {
    listen 80;
    server_name 172.16.2.197;

    root /var/www/html;
    index index.php;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock; # Thay đổi phiên bản PHP nếu khác
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }

    location ~ /\.ht {
        deny all;
    }
}
```

Kích hoạt cấu hình:
```
sudo ln -s /etc/nginx/sites-available/testsite /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl restart nginx
```

### **2.4 Tạo file PHP kiểm tra**
Tạo file PHP để hiển thị nội dung từ cơ sở dữ liệu:
```
sudo nano /var/www/html/db_test.php
```

Thêm nội dung:
```php
<?php
$servername = "172.16.2.95"; // IP của Database Server
$username = "testuser";         // User MySQL
$password = "password";         // Mật khẩu
$dbname = "testdb";             // Tên database

// Kết nối Database
$conn = new mysqli($servername, $username, $password, $dbname);

if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}
echo "Connected successfully to Database<br>";

$sql = "SELECT id, name, email FROM users";
$result = $conn->query($sql);

if ($result->num_rows > 0) {
    while($row = $result->fetch_assoc()) {
        echo "ID: " . $row["id"] . " - Name: " . $row["name"] . " - Email: " . $row["email"] . "<br>";
    }
} else {
    echo "No results found";
}

$conn->close();
?>
```

---

## **3. Thiết lập Database Server**

### **3.1 Cài đặt MySQL**
Trên Database Server:
```
sudo apt update
sudo apt install mysql-server -y
```

Khởi động và bật MySQL khi khởi động:
```
sudo systemctl start mysql
sudo systemctl enable mysql
```

### **3.2 Tạo database và bảng mẫu**
Đăng nhập vào MySQL:
```
sudo mysql -u root -p
```

Tạo database và bảng:
```
CREATE DATABASE testdb;
USE testdb;

CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    email VARCHAR(100) NOT NULL UNIQUE
);

INSERT INTO users (name, email) VALUES
('Alice', 'alice@example.com'),
('Bob', 'bob@example.com'),
('Charlie', 'charlie@example.com');
```

Kiểm tra dữ liệu:
```
SELECT * FROM users;
```

### **3.3 Cấp quyền cho Web Server**
Tạo user `testuser` và cấp quyền truy cập từ Web Server:
```
CREATE USER 'testuser'@'192.168.122.253' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON testdb.* TO 'testuser'@'192.168.122.253';
FLUSH PRIVILEGES;
```

---

## **4. Kiểm tra hệ thống**

### **4.1 Truy cập Web Server**
Mở trình duyệt và truy cập:
```
http://172.16.2.227/
```

### **4.2 Kết quả mong đợi**
Nếu mọi thứ hoạt động, bạn sẽ thấy:
```
Connected successfully to Database
ID: 1 - Name: Alice - Email: alice@example.com
ID: 2 - Name: Bob - Email: bob@example.com
ID: 3 - Name: Charlie - Email: charlie@example.com
```

---

## **5. Xử lý lỗi**
- **502 Bad Gateway**: Kiểm tra PHP-FPM có đang chạy không:
```
sudo systemctl status php7.4-fpm
```
Nếu chưa chạy, khởi động lại:
```
sudo systemctl restart php7.4-fpm
```

- **Kết nối MySQL thất bại**: Kiểm tra quyền truy cập của `testuser` và cấu hình firewall.

---

**Hướng dẫn hoàn tất.**

![Command Prompt](https://github.com/cuongnvvietis/NhanHoa/blob/main/Docs/Picture/WebServer/Screenshot_224.png)
