# 1.Tổng quan
## 1.2.Promethues 
- Prometheus là một dự án mã nguồn mở được phát triển bởi Cloud Native Computing Foundation (CNCF), nhằm giám sát và thu thập thông tin từ hệ thống phân tán. Nó là một hệ thống giám sát và cảnh báo mạnh mẽ, được thiết kế để giám sát các ứng dụng và hạ tầng phân tán.
- Prometheus có khả năng thu thập dữ liệu từ nhiều nguồn khác nhau như các máy chủ, dịch vụ, ứng dụng, và hệ thống. Nó sử dụng mô hình dữ liệu kiểu dữ liệu thời gian (time-series data model) để lưu trữ và truy vấn thông tin giám sát. Dữ liệu được thu thập bằng cách gửi các yêu cầu HTTP GET đến các endpoint của các ứng dụng, dịch vụ hoặc hệ thống muốn giám sát.
- Một trong những đặc điểm nổi bật của Prometheus là khả năng cung cấp truy vấn linh hoạt và mạnh mẽ thông qua PromQL (Prometheus Query Language). PromQL cho phép người dùng truy vấn và phân tích dữ liệu giám sát, từ việc lọc, ánh xạ, tính toán và trực quan hóa dữ liệu.
- Prometheus cũng cung cấp khả năng cảnh báo (alerting) để thông báo về các sự cố hoặc tình trạng không mong muốn trong hệ thống. Người dùng có thể xác định các quy tắc cảnh báo dựa trên các tiêu chí và ngưỡng đã định trước, và Prometheus sẽ gửi thông báo khi các điều kiện cảnh báo được kích hoạt.
- Hơn nữa, Prometheus cũng hỗ trợ tính năng ghi log (logging), tích hợp với các công cụ và dự án khác trong môi trường Cloud Native như Kubernetes, Docker, Grafana, và nhiều hệ thống khác.Prometheus là một hệ thống giám sát và cảnh báo mã nguồn mở mạnh mẽ, linh hoạt và có khả năng mở rộng, đáp ứng nhu cầu giám sát hệ thống phân tán hiện đại. Nó được sử dụng rộng rãi trong cộng đồng công nghệ để giám sát và quản lý hiệu suất của các ứng dụng và hạ tầng.
## 1.2.Grafana
- Grafana là một ứng dụng web phân tích và trực quan hóa tương tác mã nguồn mở phổ biến được thiết kế để giám sát và trực quan hóa dữ liệu và tạo bảng điều khiển tương tác. Nó cho phép bạn truy vấn dữ liệu và xây dựng biểu đồ, biểu đồ và bảng điều khiển của dữ liệu (số liệu & nhật ký) từ nhiều nguồn dữ liệu được hỗ trợ, giúp việc diễn giải và hiểu dữ liệu dễ dàng hơn.
- Grafana cho phép bạn tạo bảng thông tin tương tác và hấp dẫn về mặt hình ảnh để trực quan hóa dữ liệu, tương tự như Tableau hoặc các đối thủ cạnh tranh của nó . Nó cho phép theo dõi thời gian thực nhiều nguồn dữ liệu khác nhau, ví dụ, để theo dõi cụm Kubernetes và hỗ trợ phân tích dữ liệu chuyên sâu, cung cấp thông tin chi tiết về hiệu suất hệ thống của bạn. Điều này có thể giúp bạn đưa ra quyết định sáng suốt hơn. Grafana cũng cho phép bạn thiết lập cảnh báo dựa trên các điều kiện được xác định trước, thông báo cho bạn về các sự cố trước khi chúng trở thành vấn đề.

# 2.Triển khai Promethues và Grafana
## 2.1.Promethues
### 2.1.1.Cài đặt Promethues
- Bước 1 — Cập nhật các gói hệ thống
- `sudo apt update`
- ![image](https://github.com/user-attachments/assets/42e4b7bb-0f13-4835-9707-96d77ee96ba9)
- Bước 2 — Tạo Người dùng Hệ thống cho Prometheus
- ```
  sudo groupadd --system prometheus 
  sudo useradd -s /sbin/nologin --system -g prometheus prometheus
  ```
- ![image](https://github.com/user-attachments/assets/42bafcf3-5c40-40e7-b2d8-fdaf9eff50bb)
- Bước 3 — Tạo thư mục cho Prometheus
- ```
  sudo mkdir /etc/prometheus 
  sudo mkdir /var/lib/prometheus
  ```
- ![image](https://github.com/user-attachments/assets/eeffe8ee-4e7b-4310-af64-76c3c5670517)
- Bước 4 — Tải xuống Prometheus và giải nén tập tin
- `wget https://github.com/prometheus/prometheus/releases/download/v2.47.0/prometheus-2.47.0.linux-amd64.tar.gz`
- ![image](https://github.com/user-attachments/assets/08d9f9e2-ff30-4105-abf6-347ac489d767)
- Giải nén nội dung của tệp đã tải xuống:
- `tar vxf prometheus*.tar.gz`
- ![image](https://github.com/user-attachments/assets/e1c6ade2-9f01-47c4-8a36-dd6ac7ab4822)
- Bước 5- Điều hướng đến Thư mục Prometheus
- `cd prometheus*/`
- ![image](https://github.com/user-attachments/assets/d871d7d4-1fe4-4d67-a112-f9a2a3ef4d0a)
### 2.1.2.Cấu hình Prometheus trên Ubuntu 22.04
- Bước 1 — Di chuyển các tệp nhị phân và đặt chủ sở hữu
- ```
  sudo mv prometheus /usr/local/bin 
  sudo mv promtool /usr/local/bin 
  sudo chown prometheus:prometheus /usr/local/bin/prometheus 
  sudo chown prometheus:prometheus /usr/local/bin/promtool
  ```
- ![image](https://github.com/user-attachments/assets/37843465-206b-4b43-8970-97f27cdd64da)
- Bước 2 — Di chuyển các tệp cấu hình và đặt chủ sở hữu
- ```
  sudo mv consoles /etc/prometheus 
  sudo mv console_libraries /etc/prometheus 
  sudo mv prometheus.yml /etc/prometheus
  ```
- ![image](https://github.com/user-attachments/assets/4aee961e-8bc9-483e-bedc-2a76b375df8e)
- ```
  sudo chown prometheus:prometheus /etc/prometheus 
  sudo chown -R prometheus:prometheus /etc/prometheus/consoles 
  sudo chown -R prometheus:prometheus /etc/prometheus/console_libraries 
  sudo chown -R prometheus:prometheus /var/lib/prometheus
  ```
- ![image](https://github.com/user-attachments/assets/df58fd1a-43c8-40d2-a630-b482fdca812a)
- Tệp này prometheus.ymllà tệp cấu hình Prometheus chính
- `sudo nano /etc/prometheus/prometheus.yml`
- ![image](https://github.com/user-attachments/assets/76196777-cae5-47a1-87f2-26bb5fa0989b)
- ![image](https://github.com/user-attachments/assets/7ad9c628-1137-4a6c-adc7-c970191bab5d)
- Bước 3 — Tạo dịch vụ Prometheus Systemd
- Cần tạo một tệp dịch vụ hệ thống cho Prometheus
- `sudo nano /etc/systemd/system/prometheus.service`
- ![image](https://github.com/user-attachments/assets/5c0cb24f-2f13-49d0-b1ae-6cee64881bc8)
- Bao gồm các thiết lập này vào tệp, lưu và thoát:
- ```
  [Unit]
  Description=Prometheus
  Wants=network-online.target
  After=network-online.target

  [Service]
  User=prometheus
  Group=prometheus
  Type=simple
  ExecStart=/usr/local/bin/prometheus \
      --config.file /etc/prometheus/prometheus.yml \
      --storage.tsdb.path /var/lib/prometheus/ \
      --web.console.templates=/etc/prometheus/consoles \
      --web.console.libraries=/etc/prometheus/console_libraries
  
  [Install]
  WantedBy=multi-user.target
  ```
- ![image](https://github.com/user-attachments/assets/0e2c612f-5715-4acc-b207-499104d9313b)
- Bước 4 — Tải lại Systemd
- `sudo systemctl daemon-reload`
- ![image](https://github.com/user-attachments/assets/41289108-f878-481c-b079-5841adcd1bad)
- Bước 5 — Khởi động dịch vụ Prometheus
- ```
  sudo systemctl enable prometheus
  sudo systemctl start prometheus
  ```
- ![image](https://github.com/user-attachments/assets/2785626a-e277-4ad1-bf1f-1c288e053544)
- Bước 6 — Kiểm tra trạng thái Prometheus
- `sudo systemctl status prometheus`
- ![image](https://github.com/user-attachments/assets/6a10dc3a-a305-4909-970d-b3f815cab968)
- ![image](https://github.com/user-attachments/assets/996ce730-efe1-4b3c-9159-8267ec5d95be)
- Truy cập Giao diện Web Prometheus
- Prometheus chạy trên cổng 9090 theo mặc định nên bạn cần cho phép cổng 9090 trên tường lửa của mình. Thực hiện bằng lệnh:
- `sudo ufw allow 9090/tcp`
- ![image](https://github.com/user-attachments/assets/e090e7e3-ea98-45ed-ab6b-280fd80d2eb8)
- Khi Prometheus chạy thành công, bạn có thể truy cập nó thông qua trình duyệt web bằng cách sử dụng localhost:9090 hoặc <ip_address>:9090
- ![image](https://github.com/user-attachments/assets/abfca9f7-5f30-4731-bc50-f57c07e3cdb0)
### 2.1.3.Cài đặt và cấu hình Node Exporter
- Tạo người dùng hệ thống cho Node Exporter bằng lệnh sau
- ```
  sudo useradd \ 
    --system \ 
    --no-create-home \ 
    --shell /bin/false node_exporter
  ```
- ![image](https://github.com/user-attachments/assets/4100eafb-62f4-435f-a8ba-4e3d4f853627)
- Tải xuống và cài đặt Node Exporter
- `wget https://github.com/prometheus/node_exporter/releases/download/v1.6.1/node_exporter-1.6.1.linux-amd64.tar.gz`
- ![image](https://github.com/user-attachments/assets/ed6abacb-cc57-44ae-aa50-d9690cf73027)
- Trích xuất Node Exporter
- `tar -xvf node_exporter-1.6.1.linux-amd64.tar.gz`
- ![image](https://github.com/user-attachments/assets/5f9b4704-98c0-465d-95ef-e209b5a2b156)
- Di chuyển tệp nhị phân Node Exporter tới /usr/local/bin/:
- `sudo mv node_exporter-1.6.1.linux-amd64/node_exporter /usr/local/bin/`
- Tạo dịch vụ systemd cho Node Exporter
- `sudo nano /etc/systemd/system/node_exporter.service`
- ![image](https://github.com/user-attachments/assets/7d35f67d-58f2-4f08-823f-8a1ee5af8473)
- Kích hoạt và khởi động Node Exporter
- `sudo systemctl enable node_exporter`
- ![image](https://github.com/user-attachments/assets/fab8f18e-51e3-4544-a9b1-d7926fcddd0d)
- `sudo systemctl start node_exporter`
- ![image](https://github.com/user-attachments/assets/585cb71b-5c17-4554-b11f-721a7416308e)
- Kiểm tra trạng thái
- `sudo systemctl status node_exporter`
- ![image](https://github.com/user-attachments/assets/7abf5a3c-d7d2-40e2-ad78-e465d8df175c)
- Thêm Node Exporter làm mục tiêu trong Prometheus
- `sudo nano /etc/prometheus/prometheus.yml`
- Thêm cấu hình công việc sau cho Node Exporter
- ```
  - job_name: 'node_export'
    static_configs:
      - targets: ["localhost:9100"]
  ```
- ![image](https://github.com/user-attachments/assets/c09560db-de53-4000-8b2d-be5a9c0d52f9)
- Tải lại cấu hình Prometheus
- `promtool check config /etc/prometheus/prometheus.yml`
- Cấu hình tường lửa
- `sudo ufw allow 9100/tcp`
- Truy cập:
- `http://192.168.88.142:9100/metrics`
### 2.1.4.Nguồn tài liệu tham khảo: 
- https://medium.com/@ranjith_99360/how-to-install-prometheus-on-ubuntu-22-04-e036e0e101cc
- https://medium.com/@vishnurajlegna/2023-effortless-setup-of-prometheus-node-exporter-and-grafana-on-aws-ec2-ubuntu-22-04-f65d62dd39aa

## 2.2.Grafana
### 2.2.1.Cài đặt Grafana
- Bước 1 - Cập nhật và nâng cấp
- `sudo apt update -y && sudo apt upgrade -y`
- ![image](https://github.com/user-attachments/assets/a759aa5a-c63c-4adb-966b-83f283e96451)
- Bước 2 - Cài đặt các gói cần thiết
- `sudo apt install -y apt-transport-https software-properties-common wget`
- ![image](https://github.com/user-attachments/assets/003bd6f4-d80a-4fc5-a5ab-d7e0f7108ac3)
- Bước 3 - Thêm khóa Grafana GPG
- ```
  sudo mkdir -p /etc/apt/keyrings/
  wget -q -O - https://apt.grafana.com/gpg.key | gpg --dearmor | sudo tee /etc/apt/keyrings/grafana.gpg > /dev/null
  ```
- ![image](https://github.com/user-attachments/assets/972e209c-4e8a-44f8-91bb-bb293e4be4cd)
- Bước 4 - Thêm kho lưu trữ Grafana APT
- `echo "deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://apt.grafana.com stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list`
- ![image](https://github.com/user-attachments/assets/c4a99c02-93e6-41ba-9b8e-19631d7ef94f)
- Sau khi thêm kho lưu trữ vào hệ thống, hãy cập nhật chỉ mục gói để bao gồm thông tin từ kho lưu trữ mới được thêm vào bằng cách sử dụng:
- `sudo apt update`
- Bước 5 - Cài đặt Grafana
- `sudo apt install grafana`
- ![image](https://github.com/user-attachments/assets/a9fefd2d-f38d-4127-ab5a-a071c11b64fb)
- Bước 6 - Khởi động dịch vụ Grafana
- Sau khi quá trình cài đặt Grafana hoàn tất, bạn có thể xác minh phiên bản bằng cách sử dụng:
- `sudo grafana-server -v`
- ![image](https://github.com/user-attachments/assets/9bca64f3-c9c4-4e8f-9c61-6878c90e4be6)
- Tiếp theo, hãy khởi động dịch vụ Grafana và cho phép nó tự động khởi động khi khởi động lại hệ thống bằng các lệnh sau:
- ```
  sudo systemctl start grafana-server
  sudo systemctl enable grafana-server
  ```
- ![image](https://github.com/user-attachments/assets/30c95331-62a5-40d0-9d84-bd7d40df9fb2)
- Bước 7 - Xác minh rằng dịch vụ Grafana đang chạy
- `sudo systemctl status grafana-server`
- ![image](https://github.com/user-attachments/assets/2849d280-d069-4fba-ace3-5d9a04db7638)
- ![image](https://github.com/user-attachments/assets/27aed3b9-423c-451d-80d6-820abe54e09a)
- Bước 8 - Mở cổng trong tường lửa
- Cổng 3000 là cổng mặc định của Grafana cho giao diện web của nó. Để cho phép truy cập bên ngoài vào Grafana, bạn phải bật tường lửa và mở cổng 3000. Để thực hiện việc này, hãy thực hiện các lệnh sau trong terminal của bạn:
- ```
  sudo ufw enable 
  sudo ufw allow ssh
  sudo ufw allow 3000/tcp
  ```
- ![image](https://github.com/user-attachments/assets/60a292a9-ef1a-4945-9228-7c1c29199049)
- Bước 9 - Truy cập vào giao diện web Grafana
- `http://your_server_IP:3000`
- ![image](https://github.com/user-attachments/assets/e3e3c01c-5998-47de-9eeb-88f39881c97e)
- Tên người dùng: admin
- Mật khẩu: admin
- Sau khi đăng nhập thay đổi mật khẩu
- ![image](https://github.com/user-attachments/assets/f6bf74f6-ce26-462a-b94b-735d3e4be509)
- ![image](https://github.com/user-attachments/assets/69e562dd-15cb-49d7-a739-7a8d198941f1)
### 2.2.2.Tài liệu tham khảo
- https://www.cherryservers.com/blog/install-grafana-ubuntu#what-is-grafana

## 2.3.Cài đặt Prometheus MySQL Exporter
- Bước 1: Thêm người dùng và nhóm hệ thống Prometheus
- ```
  sudo groupadd --system prometheus
  sudo useradd -s /sbin/nologin --system -g prometheus prometheus
  ```
- Bước 2: Cài đặt Prometheus MySQL Exporter
- `curl -s https://api.github.com/repos/prometheus/mysqld_exporter/releases/latest   | grep browser_download_url | grep linux-amd64 |  cut -d '"' -f 4 | wget -qi `
- ![image](https://github.com/user-attachments/assets/94253a7c-2fba-420f-beef-4cfd579293d7)
- Giải nén file sau khi tải xuống
- `tar xvf mysqld_exporter-*.linux-amd64.tar.gz`
- ![image](https://github.com/user-attachments/assets/263fea11-9a09-4c7d-8a6f-9f524b172450)
- Cung cấp các bit thực thi cho tệp đã giải nén và di chuyển nó đến thư mục /usr/local/bin
- `cd mysqld_exporter-*.linux-amd64/`
- ![image](https://github.com/user-attachments/assets/d9994611-a84a-41f8-8de5-4b329fa0a857)
- Cài đặt sạch bằng cách xóa tarball và thư mục giải nén
- ```
  chmod +x mysqld_exporter
  sudo mv mysqld_exporter /usr/local/bin
  ```
- ![image](https://github.com/user-attachments/assets/2dd15abc-7f5a-4a85-b88a-f43f142c749a)
- Kiểm tra phiên bản phần mềm đã cài đặt
- `mysqld_exporter --version`
- ![image](https://github.com/user-attachments/assets/401b9228-528f-4f52-82ce-25c58c7b1329)
- Bước 3: Tạo người dùng cơ sở dữ liệu xuất khẩu Prometheus
- Đăng nhập vào shell máy chủ MySQL với tư cách là người dùng root
- `mysql -u root -p`
- ![image](https://github.com/user-attachments/assets/93f22ed5-499b-4fba-958a-3829667bf4cf)
- Người dùng phải có  PROCESS, SELECT, REPLICATION CLIENT quyền
- ```
  CREATE USER 'mysqld_exporter'@'localhost' IDENTIFIED BY 'StrongPassword' WITH MAX_USER_CONNECTIONS 2;
  GRANT PROCESS, REPLICATION CLIENT, SELECT ON *.* TO 'mysqld_exporter'@'localhost';
  FLUSH PRIVILEGES;
  EXIT
  ```
- Bước 4: Cấu hình thông tin xác thực cơ sở dữ liệu
- Tạo tệp thông tin xác thực cơ sở dữ liệu
- `sudo nano /etc/.mysqld_exporter.cnf`
- ![image](https://github.com/user-attachments/assets/0208ba5c-5594-4f9c-9c13-28157e652fc3)
- Thêm tên người dùng và mật khẩu chính xác để tạo người dùng
- ```
  [client]
  user=mysqld_exporter
  password=StrongPassword
  ```
- ![image](https://github.com/user-attachments/assets/9b6f2c34-2f48-4cf3-8784-68f51453848b)
- Thiết lập quyền sở hữu:
- `sudo chown root:prometheus /etc/.mysqld_exporter.cnf`
- ![image](https://github.com/user-attachments/assets/b6b58ed6-b3ff-4f2e-8c34-d4aa88060bcd)
- Bước 5: Tạo file đơn vị systemd (Dành cho hệ thống Systemd)
- Tạo một tệp dịch vụ mới
- `sudo nano /etc/systemd/system/mysql_exporter.service`
- ![image](https://github.com/user-attachments/assets/1abf9990-4365-4594-85cf-1cd27a190e64)
- Thêm nội dung sau
- ```
  [Unit]
  Description=Prometheus MySQL Exporter
  After=network.target
  User=prometheus
  Group=prometheus
  
  [Service]
  Type=simple
  Restart=always
  ExecStart=/usr/local/bin/mysqld_exporter \
  --config.my-cnf /etc/.mysqld_exporter.cnf \
  --web.listen-address=0.0.0.0:9104
  
  [Install]
  WantedBy=multi-user.target
  ```
- ![image](https://github.com/user-attachments/assets/8847cb04-d28d-4de6-bf47-4e90fe679297)
- Khi hoàn tất, hãy tải lại systemd và khởi động  mysql_exporter dịch vụ
- ```
  sudo systemctl daemon-reload
  sudo systemctl enable mysql_exporter
  sudo systemctl start mysql_exporter
  ```
- ![image](https://github.com/user-attachments/assets/86fe9f6a-3666-4f93-adc6-e54be76419ce)
- ![image](https://github.com/user-attachments/assets/08e5f04c-9a3a-45aa-a6ad-c28849a66163)
### Tài liệu tham khảo 
- https://computingforgeeks.com/install-and-configure-prometheus-mysql-exporter-on-ubuntu-centos/

## 2.4.Monitor Linux Server
- Có thể monitor server Linux thông qua metric của node_exporter
- Bảng các metric phổ biến để monitor
- CPU Metrics

| Metric | Ý nghĩa |
|--------|---------|
| `node_cpu_seconds_total` | Tổng thời gian CPU dành cho từng trạng thái (`user`, `system`, `idle`, v.v.) |
| `rate(node_cpu_seconds_total{mode!="idle"}[5m])` | Tỷ lệ sử dụng CPU trung bình trong 5 phút (loại trừ trạng thái `idle`) |
| `node_load1`, `node_load5`, `node_load15` | Load average trong 1, 5 và 15 phút |

- Memory Metrics

| Metric | Ý nghĩa |
|--------|---------|
| `node_memory_MemTotal_bytes` | Tổng dung lượng RAM |
| `node_memory_MemAvailable_bytes` | RAM khả dụng (free + cached + buffers) |
| `node_memory_MemFree_bytes` | RAM còn trống thực sự |
| `node_memory_Buffers_bytes` | RAM dùng làm buffer |
| `node_memory_Cached_bytes` | RAM dùng làm cache |
| `node_memory_SwapTotal_bytes` | Tổng dung lượng swap |
| `node_memory_SwapFree_bytes` | Swap còn trống |

- Disk Metrics

| Metric | Ý nghĩa |
|--------|---------|
| `node_filesystem_size_bytes` | Tổng dung lượng ổ đĩa |
| `node_filesystem_avail_bytes` | Dung lượng ổ đĩa còn trống |
| `node_disk_read_bytes_total` | Tổng số byte đã đọc từ đĩa |
| `node_disk_written_bytes_total` | Tổng số byte đã ghi vào đĩa |

- Network Metrics

| Metric | Ý nghĩa |
|--------|---------|
| `node_network_receive_bytes_total` | Tổng số byte đã nhận qua mạng |
| `node_network_transmit_bytes_total` | Tổng số byte đã gửi đi qua mạng |
| `node_network_receive_errs_total` | Tổng lỗi nhận |
| `node_network_transmit_errs_total` | Tổng lỗi gửi |

- System Metrics

| Metric | Ý nghĩa |
|--------|---------|
| `node_time_seconds` | Thời gian hệ thống hiện tại (Unix timestamp) |
| `node_boot_time_seconds` | Thời gian hệ thống được khởi động |
| `node_uname_info` | Thông tin nhân hệ điều hành |

- ![image](https://github.com/user-attachments/assets/faeb25c4-330f-4c9e-9f14-b1b02997e807)

## 2.5.Monitor MySQL
- MySQL Exporter Metrics

- Connection & Threads

| Metric | Ý nghĩa |
|--------|---------|
| `mysql_global_status_threads_connected` | Số lượng kết nối hiện tại |
| `mysql_global_status_threads_running` | Số lượng thread đang chạy |
| `mysql_global_status_max_used_connections` | Số kết nối cao nhất từng được sử dụng |
| `mysql_global_variables_max_connections` | Giới hạn số kết nối tối đa |

- Query & Operations

| Metric | Ý nghĩa |
|--------|---------|
| `mysql_global_status_questions` | Tổng số truy vấn client đã gửi |
| `mysql_global_status_queries` | Tổng số truy vấn được server xử lý |
| `mysql_global_status_slow_queries` | Tổng số truy vấn chậm |
| `mysql_global_status_handler_read_rnd_next` | Số lượng đọc toàn bộ bảng (dấu hiệu thiếu index) |

- InnoDB

| Metric | Ý nghĩa |
|--------|---------|
| `mysql_global_status_innodb_buffer_pool_reads` | Số lần đọc từ disk (cache miss) |
| `mysql_global_status_innodb_buffer_pool_read_requests` | Tổng yêu cầu đọc (cache hit + miss) |
| `mysql_global_status_innodb_data_reads` | Số block đọc từ InnoDB |
| `mysql_global_status_innodb_data_writes` | Số block ghi vào InnoDB |

- Replication (nếu dùng master-slave)

| Metric | Ý nghĩa |
|--------|---------|
| `mysql_slave_status_slave_io_running` | Trạng thái IO thread |
| `mysql_slave_status_slave_sql_running` | Trạng thái SQL thread |
| `mysql_slave_status_seconds_behind_master` | Độ trễ so với master (giây) |

- Others

| Metric | Ý nghĩa |
|--------|---------|
| `mysql_up` | Trạng thái MySQL (1 là OK, 0 là down) |
| `mysql_global_status_uptime` | Thời gian uptime MySQL (giây) |






















  












