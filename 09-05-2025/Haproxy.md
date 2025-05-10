# 1.Tổng quan
## 1.1.HAProxy là gì ?
- HAProxy viết tắt của High Availability Proxy, là công cụ mã nguồn mở nổi tiếng ứng dụng cho giải pháp cân bằng tải TCP/HTTP cũng như giải pháp máy chủ Proxy (Proxy Server). HAProxy có thể chạy trên các mỗi trường Linux, Solaris, FreeBSD. Công dụng phổ biến nhất của HAProxy là cải thiện hiệu năng, tăng độ tin cậy của hệ thống máy chủ bằng cách phân phối khối lượng công việc trên nhiều máy chủ (như Web, App, cơ sở dữ liệu). HAProxy hiện đã và đang được sử dụng bởi nhiều website lớn như GoDaddy, GitHub, Bitbucket, Stack Overflow, Reddit, Speedtest.net, Twitter và trong nhiều sản phẩm cung cấp bởi Amazon Web Service.
## 1.2.Thuật ngữ trong HAProxy
- Có rất nhiều thuật ngữ và khái niệm được sử dụng trong HAProxy khi nối về cân bằng tải (Load balancing) và máy chủ. Ở đây, tôi sẽ tập trung vào các khái niệm thông dụng được sử dụng nhiều trong HAProxy
### 1.2.1.Access Control List (ACL)
- Access Control List (ACL) sử dụng để kiểm tra một số điều kiện và thực hiện hành động tiếp theo dựa trên kết quả kiểm tra(VD lựa chọn một server, chặn một request). Sử dụng ACL cho phép điều tiết lưu lượng mạng linh hoạt dựa trên các yếu tố khác nhau (VD: dựa theo đường dẫn, dựa theo số lượng kết nối tới backend)
### 1.2.2.Backend
- Backend là tập các server nhận các request đã được điều tiết (HAProxy điều tiết các request tới các backend). Các Backend được định nghĩa trong mục backend khi cấu hình HAProxy.
- 2 cấu hình thường được định nghĩa trong mục backend:
+ Thuật toán cân bằng tải (Round Robin, Least Connection, IP Hash)
+ Danh sách các Server, Port (Nhận, xử lý request)
- Backend có thể chứa một hoặc nhiều server. Việc thêm nhiều server vào backend sẽ cải thiện tải, hiệu năng, tăng độ tin cậy dịch vụ. Và khi một server thuộc backend không khả dụ, các server khác thuộc backend sẽ chịu tải thay cho server xảy ra vấn đề.
- Ví dụ minh họa:
- ```
  backend web-backend
   balance roundrobin
   server web1 web1.yourdomain.com:80 check
   server web2 web2.yourdomain.com:80 check

  backend blog-backend
   balance roundrobin
   mode http
   server blog1 blog1.yourdomain.com:80 check
   server blog1 blog1.yourdomain.com:80 check
  ```
- balance roundrobin chỉ định thuật toán cân bằng tải: các Request phân phối tuần tự tới các server, đây cũng là phương thức được sử dụng mặc định.
- mode http chỉ định proxy layer 7 sẽ được sử dụng
### 1.2.3.Frontend
- Frontend định nghĩa cách các request điều tiết tới backend. Các cấu hình Frontend được định nghĩa trong mục frontend khi cấu hình HAProxy.
- Các cấu hình frontend bao gồm các thành phần:
+ Tập các IP và port (VD: 10.10.10.86:80, *:443)
+ Các ACL
+ Các backend nhận, xử lý request.

## 1.2.Các loại cân bằng tải
### 1.2.1.Không có cân bằng tải
- Kiến trúc đơn giản nhất khi triển khai ứng dụng Web
- ![image](https://github.com/user-attachments/assets/c851225f-840f-4447-a0f2-f19c360758b9)
- Trong ví dụ, người dùng sẽ kết nối trực tiếp tới Webserver (https://blog.cloud365.vn/), và không sử dụng dịch vụ cân bằng tải. Nếu web server xảy ra vấn đề, người dùng sẽ không thể kết nối tới Web được nữa. Và nếu trong trường hợp nhiều người cùng truy cập, webserver có thể không đáp ứng được các request, dẫn đến trải nhiệm sử dụng sẽ giảm xuống.
### 1.2.2.Layer 4 Load Balancing
- Cách đơn giản nhất để cân bằng tải các request tới nhiều server là sử dụng cân bằng tải mức layer 4 TCP (Tầng giao vận - transport layer). Phương pháp sẽ điều hướng các request dựa trên IP và Port. Theo ví dụ, nếu request tới địa chỉ https://blog.cloud365.vn/ thì request sẽ được điều hướng tới backend web-backend để xử lý.
- Lưu ý:
+ Hai máy chủ web cần phục vụ nội dung giống nhau. Nếu không, người dùng sẽ nhận thông tin không thống nhất (Tùy theo thuật toán cân bằng tải).
+ Nên sử dụng chung database giữ 2 web server.
- ![image](https://github.com/user-attachments/assets/1329bb82-9d92-463e-9e89-fdb6eb72b744)
### 1.2.3.Layer 7 Load Balancing
- Phương pháp phức tạp hơn, cân bằng tải sử dụng tại tầng layer 7 mức request (Tầng ứng dụng - Application layer). Sử dụng bộ cần bằng tại layer 7 sẽ điều hướng request tới các backend khác nhau dựa trên nội dung của request.
- Chế độ này cho phép bạn có thể triển khai nhiều web server khác nhau trên cùng 1 domain.
- ![image](https://github.com/user-attachments/assets/d71214c5-d095-465c-8640-4f18aa57fb7b)
- Trong hình, nếu người dùng gửi request tới ‘https://blog.cloud365.vn/’, haproxy sẽ điều hướng request tới 1, còn khi người dùng request tới https://blog.cloud365.vn/about/ haproxy sẽ điều hường request tới web-2-backend
## 1.3.Các thuật toán cân bằng tải
- Thuật toán cân bằng tải được sử dụng nhắm định nghĩa các request được điều hướng tới các server nằm trong backend trong quá trình load balancing. HAProxy cung cấp một số thuật toán mặc định:
+ roundrobin: các request sẽ được chuyển đến server theo lượt. Đây là thuật toán mặc định được sử dụng cho HAProxy
+ leastconn: các request sẽ được chuyển đến server nào có ít kết nối đến nó nhất
+ source: các request được chuyển đến server bằng các hash của IP người dùng. Phương pháp này giúp người dùng đảm bảo luôn kết nối tới một server
### 1.3.1.Sticky Sessions
- Một số ứng dụng yêu cầu người dùng phải giữ kết nối tới cùng một server thuộc backend, để giữ kết nối giữa client với một backend server bạn có thể sử dụng tùy chọn sticky sessions, xem thêm tại link dưới.
### 1.3.2.Health Check
- HAProxy sử dụng health check để phát hiện các backend server sẵn sàng xử lý request. Kỹ thuật này sẽ tránh việc loại bỏ server khỏi backend thủ công khi backend server không sẵn sàng. health check sẽ cố gắnh thiết lập kết nối TCP tới server để kiểm tra backend server có sẵn sàng xử lý request.
- Nếu health check không thể kết nối tới server, nó sẽ tự động loại bỏ server khởi backend, các traffic tới sẽ không được forward tới server cho đến khi nó có thể thực hiện được health check. Nếu tất cả server thuộc backend đều xảy vấn đề, dịch vụ sẽ trở trên không khả dụ (trả lại status code 500) cho đến khi 1 server thuộc backend từ trạng thái không khả dụ chuyển sang trạng thái sẵn sàng.
## 1.4.Tài liệu tham khảo 
- https://blog.cloud365.vn/linux/tong-quan-haproxy/
# 2.Triển khai
- Triển khai HAProxy, KeepAlived, Apache2 trên cả 2 VM
- Cài đặt trên 2 máy
- `sudo apt-get install apache2 keepalived haproxy`
- Chỉnh sửa nội dung file index.html của từng máy để test cân bằng tải
- ![image](https://github.com/user-attachments/assets/827cb6fd-37b9-4040-95cf-4ec69ea94f73)
- ![image](https://github.com/user-attachments/assets/9a4e3960-4dba-4b31-9e96-09d2ceafcb69)
- Cấu hình keepalived
- File config của Keepalived sẽ được lưu ở /etc/keepalived/keepalived.conf
- Thực hiện sửa file cấu hình trên từng máy
- Trên máy VM 1
- `nano /etc/keepalived/keepalived.conf`
- Nội dung file:
- ```
  global_defs {
    router_id test1                            #khai báo route_id của keepalived
  }
  vrrp_script chk_haproxy {
    script "killall -0 haproxy"
    interval 2
    weight 2
  }
  vrrp_instance VI_1 {
    virtual_router_id 51
    advert_int 1
    priority 100
    state MASTER
    interface ens33                            #thông tin tên interface của server, bạn dùng lệnh `ifconfig` để xem và điền cho đúng
    virtual_ipaddress {
      192.168.88.151 dev ens33           		#Khai báo Virtual IP (VIP) cho interface tương ứng
    }
   authentication {
       auth_type PASS
       auth_pass 123456                    #Password này phải khai báo giống nhau giữa các server keepalived
       }
    track_script {
      chk_haproxy
    }
  }
  ```
- Trên máy VM2
- `nano /etc/keepalived/keepalived.conf`
- ```
  global_defs {
    router_id test2
  }
  vrrp_script chk_haproxy {
    script "killall -0 haproxy"
    interval 2
    weight 2
  }
  vrrp_instance VI_1 {
    virtual_router_id 51
    advert_int 1
    priority 99
    state BACKUP
    interface ens33
    virtual_ipaddress {
      192.168.88.151 dev ens33
    }
  authentication {
          auth_type PASS
          auth_pass 123456
          }
  track_script {
      chk_haproxy
      }
    }
  ```
- Khởi động lại keepalived để apply
- `systemctl restart keepalived`
- Chú ý: Khai báo với test1 state là MASTER , priority 100 Khác với test2 state BACKUP và priority 99
- Kiểm tra
- Truy cập IP VIP để kiểm tra http://192.168.88.151
- ![image](https://github.com/user-attachments/assets/4e447309-e0a6-4c86-994e-c233475e468f)
- ![image](https://github.com/user-attachments/assets/1e67e321-b786-4919-aa29-74342b6b5b36)
