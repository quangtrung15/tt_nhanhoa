# 1.DNS
## 1.1.DNS là gì?
DNS (Domain Name System) là hệ thống phân giải tên miền, giúp chuyển đổi tên miền thành địa chỉ IP để truy cập trang web. Nhờ DNS, người dùng không cần nhớ địa chỉ IP phức tạp mà chỉ cần nhập tên miền. Hệ thống này giúp quản lý mạng hiệu quả, tăng tính bảo mật và cải thiện tốc độ truy cập internet.
## 1.2.Chức năng của DNS là gì?
DNS là hệ thống quản lý (Management System) và chuyển đổi tên miền thành địa chỉ IP tương ứng. Cụ thể, DNS thực hiện các nhiệm vụ sau:

- **Chuyển đổi tên miền thành địa chỉ IP:** DNS giúp chuyển đổi tên miền dễ đọc (ví dụ: www.google.com) thành địa chỉ IP (ví dụ: 142.250.190.14) để thiết bị có thể xác định được vị trí chính xác của máy chủ trên mạng.

- **Quản lý các bản ghi DNS:** DNS lưu trữ thông tin trong các bản ghi DNS, bao gồm các loại bản ghi như A (địa chỉ IPv4), AAAA (địa chỉ IPv6), CNAME (tên miền chấp nhận mệnh đề), MX (máy chủ thư điện tử) và nhiều loại khác.

- **Phân giải ngược:** DNS cũng có khả năng phân giải ngược, chuyển đổi địa chỉ IP thành tên miền. Tuy nhiên, chức năng này ít được sử dụng hơn so với chuyển đổi tên miền thành địa chỉ IP.

Nhờ vào DNS, người dùng có thể truy cập các trang web và dịch vụ trực tuyến mà không cần ghi nhớ các địa chỉ IP phức tạp.
## 1.3.Nguyên lý hoạt động của DNS
Người dùng gửi yêu cầu: Khi nhập tên miền vào trình duyệt, một yêu cầu sẽ được gửi đến Recursive DNS Server.

- **Recursive DNS Server tìm kiếm:** Recursive DNS Server thực hiện các bước tìm kiếm thông tin từ Root DNS Server đến Authoritative DNS Server.

- **Authoritative DNS Server cung cấp địa chỉ IP:** Server cuối cùng cung cấp địa chỉ IP tương ứng với tên miền.

- **Recursive DNS Server nhận địa chỉ IP:** Được cung cấp địa chỉ IP, Recursive DNS Server trả về thông tin cho trình duyệt và cập nhật bộ nhớ đệm.

- **Trình duyệt kết nối đến máy chủ web:** Trình duyệt sử dụng địa chỉ IP để kết nối đến máy chủ web và tải trang web.
