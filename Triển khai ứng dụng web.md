# Với Window Server
## Triển khai site demo1 html baic trên Web Server IIS
- Cài đặt Web Server trên Server Manager
- ![image](https://github.com/user-attachments/assets/1aee1bd1-d35f-4878-805c-d42a7101e39a)
- ![image](https://github.com/user-attachments/assets/4bebda0c-0f1e-490e-9d24-58799d6cc579)
- ![image](https://github.com/user-attachments/assets/89b0aebc-0b6a-46d3-821a-2eedb0678166)
- ![image](https://github.com/user-attachments/assets/cd83276d-3a30-413d-b392-5493e5f23579)
- ![image](https://github.com/user-attachments/assets/106c0558-b0fd-4aea-a5de-782972df6c5d)
- ![image](https://github.com/user-attachments/assets/c0f5a900-bac2-40c4-839f-b5044702c901)
- ![image](https://github.com/user-attachments/assets/147034e1-25b2-4180-9c0f-4878dc213948)
- ![image](https://github.com/user-attachments/assets/6f3c5cba-6483-42ac-b8bf-8efa57eb8a44)
- Tạo thư mục và file index.html
- ![image](https://github.com/user-attachments/assets/5d9431dc-2d86-4354-a83a-ed5402b48964)
- Vào Tools > Internet Information Services (IIS) Manager
- ![image](https://github.com/user-attachments/assets/11961992-e381-4eea-84cc-85d25740ac20)
- Vào Sites > Add Website...
- ![image](https://github.com/user-attachments/assets/fb116233-3e5c-4903-a0ca-ce9585c993eb)
- Đặt tên trang(Site name) và chọn đường dẫn đến thư mục chứa trang index.html
- ![image](https://github.com/user-attachments/assets/6efecd30-36e7-47a8-ae58-c48e0cb6786d)
- Chọn Default Document > chọn index.html làm trang mặc định
- ![image](https://github.com/user-attachments/assets/4cc91a28-dab5-4e0d-af8f-8ce4d383a918)
- ![image](https://github.com/user-attachments/assets/bd73f06f-7240-4fdb-8423-88d617ccbc89)
- Cấu hình DNS
- ![image](https://github.com/user-attachments/assets/e84619df-133f-4410-8c01-5fb1aec23c8f)
- Khởi động web
- ![image](https://github.com/user-attachments/assets/29e84e5c-5f84-43d6-ad57-9ffe2014f59b)
- Kết quả:
- <img src="https://github.com/user-attachments/assets/8d1ebe2a-e9dc-40b7-9511-f4366891902e" alt="image" width="550"/>
## Triển khai site demo2 ASP classic trên Web Server IIS
- Cài đặt ASP trên Web Server(IIS)
- ![image](https://github.com/user-attachments/assets/fdac2eb6-62de-44e3-864a-bde976158523)
- Tạo thư mục và tạo file default.asp
- ![image](https://github.com/user-attachments/assets/26f20db8-af8a-4571-a4f3-7c3fd67e8bab)
- Vào Tools > Internet Information Services (IIS) Manager
- ![image](https://github.com/user-attachments/assets/11961992-e381-4eea-84cc-85d25740ac20)
- Vào Sites > Add Website...
- Đặt tên trang(Site name) và chọn đường dẫn đến thư mục chứa trang default.asp
- ![image](https://github.com/user-attachments/assets/1e29694d-194e-4e78-b30a-a8360de97879)
- Cấu hình DNS
- Kết quả:
- <img src="https://github.com/user-attachments/assets/8006d034-b6e4-4c2b-b3ac-873086341921" alt="image" width="550"/>
## Triển khai site demo4 .php trên Web Server IIS
### Bước 1: Cài CGI
- Features: Tick thêm CGI (để PHP hoạt động qua FastCGI)
- ![image](https://github.com/user-attachments/assets/dad534a4-b207-420d-a3f9-ea9bbe979b24)
### Bước 2: Cài PHP
- Truy cập: https://windows.php.net/download
- Tải bản PHP phù hợp (khuyên dùng Non Thread Safe x64 nếu chạy với FastCGI).
- ![image](https://github.com/user-attachments/assets/a5c46c03-b63a-44ec-86d4-89cb6d7b557e)
- Giải nén vào thư mục, ví dụ: C:\PHP.
- Đổi tên file php.ini-development → php.ini
### Bước 3: Cấu hình IIS để chạy PHP
#### 3.1. Thêm PHP vào IIS:
- Mở IIS Manager (inetmgr).
- Chọn Handler Mappings > Add Module Mapping:
- ![image](https://github.com/user-attachments/assets/b3663e91-4159-4813-8bab-93db659c1b5c)
- Request path: *.php
- Module: FastCgiModule
- Executable: C:\PHP\php-cgi.exe (hoặc đường dẫn đến file php-cgi.exe)
- Name: PHP_via_FastCGI
- OK > Yes khi được hỏi.
- ![image](https://github.com/user-attachments/assets/e22d0dde-8df5-46a2-88ef-d98b9d95fbff)
### 3.2. Tạo site demo PHP
- Tạo thư mục: C:\inetpub\phpdemo4
- Thêm file demo4.php
- ![image](https://github.com/user-attachments/assets/0246f578-0917-47e4-9cd0-86e134698d90)
- Cấu hình DNS
- Khởi động web
- Kết quả:
- <img src="https://github.com/user-attachments/assets/08ea5179-e655-42ae-9b59-aaa92ae33b28" alt="image" width="550"/>.
