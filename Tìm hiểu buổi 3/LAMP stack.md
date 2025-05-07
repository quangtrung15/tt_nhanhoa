# Triển khai site wordpress trên LAMP stack
## 1.Cập nhật hệ thống
- Cập nhật hệ thống: `sudo apt update && sudo apt upgrade -y`
- <img src="https://github.com/user-attachments/assets/6fca6bb2-0017-46a8-8b85-425640b21b46" alt="image" width="600"/>

## 2.Cài Apache (web server)
- Cài đặt Apache: `sudo apt install apache2 -y`
- <img src="https://github.com/user-attachments/assets/2a8281dd-8885-4751-856a-7ff5e4633bba" alt="image" width="600"/>
- Kiểm tra xem cài đặt thành công chưa, mở trình duyệt truy cập: `http://<IP-của-Ubuntu>`
- <img src="https://github.com/user-attachments/assets/b9b26ec0-7e9c-49f9-a4aa-66a416cb1be3" alt="image" width="600"/>

## 3.Cài đặt MySQL
- Cài đặt MySQL: `sudo apt install mysql-server -y`  
- <img src="https://github.com/user-attachments/assets/e15c6081-8ff3-4408-9e43-095e237010f4" alt="image" width="600"/>
- Cài đặt bảo mật: `sudo mysql_secure_installation`
- <img src="https://github.com/user-attachments/assets/9e619f8e-a28d-4ea3-aca6-1be726a81cdd" alt="image" width="600"/>

## 4.Cài PHP + module cần thiết
- `sudo apt install php libapache2-mod-php php-mysql php-curl php-xml php-gd php-mbstring -y`
- <img src="https://github.com/user-attachments/assets/caa9d8a7-0a23-44cd-a05a-644af685feb2" alt="image" width="600"/>
- Kiểm tra xem PHP đã cài thành công chưa: `php -v`
- <img src="https://github.com/user-attachments/assets/b0aecd8b-23fe-4f87-80fd-f6cb30629056" alt="image" width="600"/>

## 5.Cài đặt WordPress
### 5.1.Tạo database cho WordPress
- Tạo database cho WordPress: `sudo mysql -u root -p`
- <img src="https://github.com/user-attachments/assets/c7177a0f-060f-4451-83bc-f21164e1b04a" alt="image" width="600"/>

```sql
CREATE DATABASE wordpress_db DEFAULT CHARACTER SET utf8 COLLATE utf8_unicode_ci;
CREATE USER 'wp_user'@'localhost' IDENTIFIED BY 'Trung03!';
GRANT ALL PRIVILEGES ON wordpress_db.* TO 'wp_user'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```
- <img src="https://github.com/user-attachments/assets/0e8deb1a-9ce3-433e-821f-909c29d60901" alt="image" width="600"/>
### 5.2.Tải WordPress
```bash
cd /tmp
wget https://wordpress.org/latest.tar.gz
tar -xvzf latest.tar.gz
```
- <img src="https://github.com/user-attachments/assets/89dd7480-8d32-4458-95f5-d2df02257343" alt="image" width="600"/>
### 5.3.Di chuyển vào thư mục web
```bash
sudo rm -rf /var/www/html/*
sudo mv wordpress/* /var/www/html/
```
- ![image](https://github.com/user-attachments/assets/20d9432b-57df-4acf-b2c6-50d9e08691f4)
### 5.4.Cấp quyền thư mục
```bash
sudo chown -R www-data:www-data /var/www/html
sudo chmod -R 755 /var/www/html
```
- ![image](https://github.com/user-attachments/assets/dd46c043-1a41-40e0-9a0d-9326d28729c2)
### 5.4.Tạo file cấu hình WordPress
```bash
sudo cp wp-config-sample.php wp-config.php
```
- ![image](https://github.com/user-attachments/assets/50784306-2c7b-47d4-a8c2-f568dfa5be04)
- Sửa wp-config.php: `sudo nano wp-config.php`
- ![image](https://github.com/user-attachments/assets/a4598bc7-e27d-483a-8b88-a5c38c3cb165)
### 5.5.Khởi động lại Apache
  - `sudo systemctl restart apache2`

## Kiểm thử:
- ![image](https://github.com/user-attachments/assets/20dd3ac7-27e2-4cbe-bbf2-9f2b7cc4eaec)
- ![image](https://github.com/user-attachments/assets/eb1e830c-2861-4dae-9957-1fb56a4d8deb)
- ![image](https://github.com/user-attachments/assets/86628846-4660-412c-b254-c6ce660740a8)
- ![image](https://github.com/user-attachments/assets/97858ee6-6d7d-4498-9cca-930e120ec47e)
  































