# Bash Script với LAMP
- Việc viết bash script cài đặt LAMP là để tự động hóa toàn bộ quá trình cài đặt Linux, Apache, MySQL, PHP thay vì làm thủ công từng lệnh.
## Mục tiêu: Tạo 1 file script .sh để:
- Cài Apache, MySQL, PHP
- Khởi động dịch vụ
- Tải và triển khai WordPress
- Cấu hình quyền thư mục
## Triển khai
- Tạo file script: install-lamp-wordpress.sh
```
#!/bin/bash

# Cập nhật hệ thống
sudo apt update -y
sudo apt upgrade -y

# Cài Apache
sudo apt install apache2 -y
sudo systemctl enable apache2
sudo systemctl start apache2

# Cài MySQL
sudo apt install mysql-server -y
sudo systemctl enable mysql
sudo systemctl start mysql

# Cài PHP và các extension
sudo apt install php libapache2-mod-php php-mysql php-cli php-curl php-xml php-mbstring php-zip php-gd -y

# Tạo database và user cho WordPress
DB_NAME="wordpress_db"
DB_USER="wp_user"
DB_PASS="123456"

sudo mysql -e "CREATE DATABASE IF NOT EXISTS ${DB_NAME};"
sudo mysql -e "CREATE USER IF NOT EXISTS '${DB_USER}'@'localhost' IDENTIFIED BY '${DB_PASS}';"
sudo mysql -e "GRANT ALL PRIVILEGES ON ${DB_NAME}.* TO '${DB_USER}'@'localhost';"
sudo mysql -e "FLUSH PRIVILEGES;"

# Tải WordPress
cd /tmp
wget https://wordpress.org/latest.tar.gz
tar -xzf latest.tar.gz

# Copy vào thư mục web
sudo rm -rf /var/www/html/*
sudo cp -r wordpress/* /var/www/html/
sudo chown -R www-data:www-data /var/www/html
sudo chmod -R 755 /var/www/html

# Tạo file cấu hình WordPress
cd /var/www/html
sudo cp wp-config-sample.php wp-config.php

# Sửa thông tin database trong wp-config.php
sudo sed -i "s/database_name_here/${DB_NAME}/" wp-config.php
sudo sed -i "s/username_here/${DB_USER}/" wp-config.php
sudo sed -i "s/password_here/${DB_PASS}/" wp-config.php

echo "✅ LAMP và WordPress đã được cài đặt!"
echo "👉 Truy cập http://$(hostname -I | awk '{print $1}') để bắt đầu cài đặt WordPress."
```

## Cách sử dụng:
### Cấp quyền chạy
- `chmod +x install-lamp-wordpress.sh`
### Chạy script:
- `./install-lamp-wordpress.sh`
