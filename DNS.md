# 1.DNS
## 1.1.DNS là gì?
- Domain Name System (DNS) là danh bạ điện thoại của Internet. Con người truy cập thông tin trực tuyến thông qua các tên miền (domain names), như nytimes.com hoặc espn.com. Trình duyệt web (web browsers) giao tiếp với nhau thông qua các địa chỉ IP (Internet Protocol addresses). DNS thực hiện việc chuyển đổi (translate) các tên miền thành địa chỉ IP để trình duyệt có thể tải tài nguyên trên Internet.
- Mỗi thiết bị kết nối với Internet đều có một địa chỉ IP duy nhất mà các máy khác sử dụng để tìm đến thiết bị đó. DNS servers giúp con người không cần phải ghi nhớ các địa chỉ IP như 192.168.1.1 (theo chuẩn IPv4), hoặc các địa chỉ IP phức tạp hơn theo định dạng chữ và số như 2400:cb00:2048:1::c629:d7a2 (theo chuẩn IPv6).
## 1.2.Chức năng của DNS là gì?
- DNS là hệ thống quản lý (Management System) và chuyển đổi tên miền thành địa chỉ IP tương ứng. Cụ thể, DNS thực hiện các nhiệm vụ sau:
- **Chuyển đổi tên miền thành địa chỉ IP:** DNS giúp chuyển đổi tên miền dễ đọc (ví dụ: www.google.com) thành địa chỉ IP (ví dụ: 142.250.190.14) để thiết bị có thể xác định được vị trí chính xác của máy chủ trên mạng.
- **Quản lý các bản ghi DNS:** DNS lưu trữ thông tin trong các bản ghi DNS, bao gồm các loại bản ghi như A (địa chỉ IPv4), AAAA (địa chỉ IPv6), CNAME (tên miền chấp nhận mệnh đề), MX (máy chủ thư điện tử) và nhiều loại khác.
- **Phân giải ngược:** DNS cũng có khả năng phân giải ngược, chuyển đổi địa chỉ IP thành tên miền. Tuy nhiên, chức năng này ít được sử dụng hơn so với chuyển đổi tên miền thành địa chỉ IP.
- Nhờ vào DNS, người dùng có thể truy cập các trang web và dịch vụ trực tuyến mà không cần ghi nhớ các địa chỉ IP phức tạp.
## 1.3.Các loại máy chủ DNS
- **Recursive Resolver:** Gửi truy vấn thay người dùng, đệ quy hỏi các DNS khác.
- **Root Name Server:** Điểm bắt đầu của hệ thống DNS, biết các TLD server
- **TLD Name Server:** Quản lý các tên miền cấp cao như .com, .org…
- **Authoritative Name Server:** Có thông tin chính xác của tên miền cụ thể
## 1.4.Nguyên lý hoạt động của DNS
Người dùng gửi yêu cầu: Khi nhập tên miền vào trình duyệt, một yêu cầu sẽ được gửi đến Recursive DNS Server.
- **Recursive DNS Server tìm kiếm:** Recursive DNS Server thực hiện các bước tìm kiếm thông tin từ Root DNS Server đến Authoritative DNS Server.
- **Authoritative DNS Server cung cấp địa chỉ IP:** Server cuối cùng cung cấp địa chỉ IP tương ứng với tên miền.
- **Recursive DNS Server nhận địa chỉ IP:** Được cung cấp địa chỉ IP, Recursive DNS Server trả về thông tin cho trình duyệt và cập nhật bộ nhớ đệm.
- **Trình duyệt kết nối đến máy chủ web:** Trình duyệt sử dụng địa chỉ IP để kết nối đến máy chủ web và tải trang web
## 1.5.Các bản ghi DNS
- **Bản ghi loại A(Address Mapping records):** Sử dụng để chuyển đổi một domain name thành một địa chỉ IPv4.
- **Bản ghi loại AAAA(IP Version 6 Address records):** Sử dụng để chuyển đổi một domain name thành một địa chỉ IPv6.
- **Bản ghi loại NS(Name Server records):** Lưu thông tin về Name Server. Nó định danh cho một máy chủ có thẩm quyền về một zone nào đó.
- **Bản ghi loại CNAME(Canonical Name records):** Bản ghi CNAME chỉ định một tên miền cần phải được truy vấn để giải quyết truy vấn DNS ban đầu. Vì vậy các bản ghi CNAME được sử dụng để tạo các bí danh tên miền. Bản ghi CNAME thực sự hữu ích khi chúng ta muốn bí danh tên miền của chúng ta tới miền bên ngoài. Trong các trường hợp khác, chúng ta có thể xóa các bản ghi CNAME và thay thế chúng bằng các bản ghi A.
- **Bản ghi loại HINFO(Host Information records):** Hồ sơ HINFO được sử dụng để thu thập thông tin tổng quát về máy chủ. Hồ sơ ghi rõ loại CPU và hệ điều hành. Dữ liệu bản ghi HINFO cung cấp khả năng sử dụng các giao thức cụ thể của hệ điều hành khi hai máy chủ muốn liên lạc. Vì lý do an toàn, hồ sơ HINFO thường không được sử dụng trên các máy chủ công cộng.
- **Bản ghi loại SOA(Start of Authority records):** Hồ sơ ghi rõ thông tin cốt lõi về vùng DNS, bao gồm name server chính, email của quản trị viên tên miền, số sê-ri miền và một số bộ đếm hiện thời liên quan đến refresh lại zone.
- **Bản ghi loại PTR(Reverse-lookup Pointer records):** Bản ghi PTR được sử dụng để tra cứu tên miền dựa trên địa chỉ IP.
## 1.6.Lệnh kiểm tra DNS (trên Windows hoặc Linux)
- nslookup
