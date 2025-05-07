# LEMP là gì ?
- Các thành phần cấu thành LEMP stack cũng gần tương tự với LAMP, chỉ khác là Apache sẽ được thay thế bởi nginx. Nginx được đọc là "engine-x", giải thích cho chữ E trong "LEPM", nginx cũng là một ứng dụng HTTP proxy nhưng không có được danh tiếng ấn tượng như Apache, tuy nhiên, nó có ưu điểm là cho phép xử lý tốc độ tải cao hơn đối với các HTTP request.
- L - Linux	Hệ điều hành nền tảng (Ubuntu, CentOS, Debian...)
- E – Nginx (đọc là “Engine-X”)	Web server thay cho Apache
- M - MySQL / MariaDB	Hệ quản trị cơ sở dữ liệu – lưu trữ dữ liệu cho website
- P - PHP	Ngôn ngữ lập trình để xử lý logic phía server

# Triển khai site wordpress trên LEMP stack
## 1.Cập nhật hệ thống:
- `sudo apt update`
## 2.Cài đặt Nginx
- `sudo apt install nginx -y`
- ![image](https://github.com/user-attachments/assets/e0d39b20-a05b-41d3-b430-0739cbeb11dd)
- Kiểm tra cài đặt xem thành công chưa, mở trình duyệt truy cập: http://<IP-của-Ubuntu>
- ![image](https://github.com/user-attachments/assets/dfd7c80c-372c-4304-96c2-fc6014f0913b)
## 3.Cài PHP và các module cần thiết
- `sudo apt install php-fpm php-mysql -y`
- ![image](https://github.com/user-attachments/assets/0901214f-bd73-4640-915b-be7a967adc82)
- Kiểm tra PHP-FPM: `sudo systemctl status php7.*-fpm`

## 4.Cấu hình Nginx để xử lý PHP
- `sudo nano /etc/nginx/sites-available/wordpress`
- 





