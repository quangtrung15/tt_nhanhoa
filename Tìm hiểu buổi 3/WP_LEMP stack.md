# LEMP là gì ?
- Các thành phần cấu thành LEMP stack cũng gần tương tự với LAMP, chỉ khác là Apache sẽ được thay thế bởi nginx. Nginx được đọc là "engine-x", giải thích cho chữ E trong "LEPM", nginx cũng là một ứng dụng HTTP proxy nhưng không có được danh tiếng ấn tượng như Apache, tuy nhiên, nó có ưu điểm là cho phép xử lý tốc độ tải cao hơn đối với các HTTP request.
- L - Linux	Hệ điều hành nền tảng (Ubuntu, CentOS, Debian...)
- E – Nginx (đọc là “Engine-X”)	Web server thay cho Apache
- M - MySQL / MariaDB	Hệ quản trị cơ sở dữ liệu – lưu trữ dữ liệu cho website
- P - PHP	Ngôn ngữ lập trình để xử lý logic phía server

# Triển khai site wordpress trên LEMP stack
## 1.Cập nhật hệ thống:
- `sudo apt update && sudo apt upgrade -y`
- ![image](https://github.com/user-attachments/assets/41b44e3c-61de-4165-bdfc-17dc2b4d2f5f)
## 2.Cài đặt Nginx
- `sudo apt install nginx -y`
- ![image](https://github.com/user-attachments/assets/057f0737-9beb-4f4b-9a70-0ac425e85830)
- Kiểm tra cài đặt xem thành công chưa, mở trình duyệt truy cập: http://<IP-của-Ubuntu>
- ![image](https://github.com/user-attachments/assets/206249c0-dc8d-43ff-9a43-4e608ab7a474)
## 3.Cài đặt MySQL
- ```
  sudo apt install mysql-server -y
  sudo mysql_secure_installation
  ```
- ![image](https://github.com/user-attachments/assets/9b7bad96-503d-4374-95de-45c94e69576b)
## 3.Cài PHP và các module cần thiết
- `sudo apt install php-fpm php-mysql php-curl php-gd php-mbstring php-xml php-xmlrpc php-soap php-intl php-zip -y`
- ![image](https://github.com/user-attachments/assets/baa12f4a-d12b-4818-b507-308b89258259)
## 4.Tạo cơ sở dữ liệu cho WordPress
- Đăng nhập MySQL:
- `sudo mysql`
- ![image](https://github.com/user-attachments/assets/d858dc9e-1aef-4c10-a21d-f1b085ce005c)
- ```
  CREATE DATABASE wordpress DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
  CREATE USER 'wordpressuser'@'localhost' IDENTIFIED BY 'Trung03!'; 
  GRANT ALL PRIVILEGES ON wordpress.* TO 'wordpressuser'@'localhost';
  FLUSH PRIVILEGES;
  EXIT;
  ```
- ![image](https://github.com/user-attachments/assets/66820ae7-8c15-49be-ac32-6dd81b1e726b)
## 5.Tải và cấu hình WordPress
- Tải WordPress:
- ```
  cd /tmp
  curl -O https://wordpress.org/latest.tar.gz
  tar -xvzf latest.tar.gz
  ```
- ![image](https://github.com/user-attachments/assets/6f5bb7c9-1db8-4a33-9d3e-9af59e7527f1)
- Di chuyển đến thư mục web:
- ```
  sudo mkdir -p /var/www/wordpress
  sudo cp -a wordpress/. /var/www/wordpress
  ```
- ![image](https://github.com/user-attachments/assets/ff05756a-d5bc-4565-b5e1-5147e27d776b)
- ```
  sudo chown -R www-data:www-data /var/www/wordpress
  sudo find /var/www/wordpress -type d -exec chmod 755 {} \;
  sudo find /var/www/wordpress -type f -exec chmod 644 {} \;
  ```
- ![image](https://github.com/user-attachments/assets/b53a14b5-c129-42b8-af16-152460b275d9)
## 6.Cấu hình Nginx
- Tạo file cấu hình Nginx:
- `sudo nano /etc/nginx/sites-available/wordpress`
- Nội dung cấu hình:
- ```
  server {
    listen 80;
    server_name your_domain_or_ip;

    root /var/www/wordpress;
    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php?$args;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php8.1-fpm.sock;  # kiểm tra đúng phiên bản
    }

    location ~ /\.ht {
        deny all;
    }
  }
  ```
` ![image](https://github.com/user-attachments/assets/a570f193-22e3-4032-be04-f66a97085c7f)
- Kiểm tra đúng socket php bằng:
- `sudo find /run/php/ -name "php*-fpm.sock"`
- ![image](https://github.com/user-attachments/assets/650e6605-fcbe-4f04-94ce-b3dfa7d1aa0d)
## 7.Bật cấu hình:
- ```
  sudo ln -s /etc/nginx/sites-available/wordpress /etc/nginx/sites-enabled/
  sudo nginx -t
  sudo systemctl reload nginx
  ```
- ![image](https://github.com/user-attachments/assets/d158de1b-8e18-4bbf-a30f-932e1e2bec19)
## 8.Hoàn tất cài đặt WordPress
- Truy cập:
- `http://your_domain_or_ip`
- ![image](https://github.com/user-attachments/assets/99eb760e-7c7e-46fc-930b-cad7a833a45b)
- ![image](https://github.com/user-attachments/assets/b283aaf4-7e73-4d10-80ee-aff4eec2a777)
- ![image](https://github.com/user-attachments/assets/f0f412ce-8f66-4f14-a069-d1d7da87bda2)
- ![image](https://github.com/user-attachments/assets/4aee755c-39ae-4b61-a0dd-8a5d86b92fe1)



















