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
- Tạo database cho WordPress: `sudo mysql -u root -p`
- <img src="https://github.com/user-attachments/assets/c7177a0f-060f-4451-83bc-f21164e1b04a" alt="image" width="600"/>
- `CREATE DATABASE wordpress_db DEFAULT CHARACTER SET utf8 COLLATE utf8_unicode_ci;
CREATE USER 'wp_user'@'localhost' IDENTIFIED BY 'Trung03!'; 
GRANT ALL PRIVILEGES ON wordpress_db.* TO 'wp_user'@'localhost';
FLUSH PRIVILEGES;
EXIT;
- ```bash
  CREATE DATABASE wordpress_db DEFAULT CHARACTER SET utf8 COLLATE utf8_unicode_ci;
CREATE USER 'wp_user'@'localhost' IDENTIFIED BY 'Trung03!'; 
GRANT ALL PRIVILEGES ON wordpress_db.* TO 'wp_user'@'localhost';
FLUSH PRIVILEGES;
EXIT;
  
- ![image](https://github.com/user-attachments/assets/0e8deb1a-9ce3-433e-821f-909c29d60901)















