# Với Window Server
## Triển khai site demo1 html baic trên Web Server IIS
- Cài đặt Web Server trên Server Manager
- Tạo thư mục và file index.html
- Vào Tools > Internet Information Services (IIS) Manager
- Vào Sites > Add Website...
- Đặt tên trang(Site name) và chọn đường dẫn đến thư mục chứa trang index.html
- Cấu hình DNS
- Chọn Default Document > chọn index.html làm trang mặc định
- Khởi động web
- Kết quả:
- <img src="https://github.com/user-attachments/assets/8d1ebe2a-e9dc-40b7-9511-f4366891902e" alt="image" width="550"/>
## Triển khai site demo2 ASP classic trên Web Server IIS
- Cài đặt ASP trên Web Server(IIS)
- Tạo thư mục và tạo file default.asp
- Vào Tools > Internet Information Services (IIS) Manager
- Vào Sites > Add Website...
- Đặt tên trang(Site name) và chọn đường dẫn đến thư mục chứa trang default.asp
- Cấu hình DNS
- Kết quả:
- <img src="https://github.com/user-attachments/assets/8006d034-b6e4-4c2b-b3ac-873086341921" alt="image" width="550"/>
## Triển khai site demo4 .php trên Web Server IIS
### Bước 1: Cài IIS và CGI
- Mở Server Manager → Add Roles and Features
- Server Roles: Chọn Web Server (IIS)
- Features: Tick thêm CGI (để PHP hoạt động qua FastCGI)
### Bước 2: Cài PHP
- Truy cập: https://windows.php.net/download
- Tải bản PHP phù hợp (khuyên dùng Non Thread Safe x64 nếu chạy với FastCGI).
- Giải nén vào thư mục, ví dụ: C:\PHP.
- Đổi tên file php.ini-development → php.ini
### Bước 3: Cấu hình IIS để chạy PHP
#### 3.1. Thêm PHP vào IIS:
- Mở IIS Manager (inetmgr).
- Chọn Handler Mappings > Add Module Mapping:
- Request path: *.php
- Module: FastCgiModule
- Executable: C:\PHP\php-cgi.exe (hoặc đường dẫn đến file php-cgi.exe)
- Name: PHP_via_FastCGI
- OK > Yes khi được hỏi.
### 3.2. Tạo site demo PHP
- Tạo thư mục: C:\inetpub\phpdemo4
- Thêm file demo4.php
- Cấu hình DNS
- Khởi động web
- Kết quả:
- <img src="https://github.com/user-attachments/assets/08ea5179-e655-42ae-9b59-aaa92ae33b28" alt="image" width="550"/>.






