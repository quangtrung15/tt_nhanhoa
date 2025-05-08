# 1.Tổng quan
## 1.2.Promethues 
- Prometheus là một dự án mã nguồn mở được phát triển bởi Cloud Native Computing Foundation (CNCF), nhằm giám sát và thu thập thông tin từ hệ thống phân tán. Nó là một hệ thống giám sát và cảnh báo mạnh mẽ, được thiết kế để giám sát các ứng dụng và hạ tầng phân tán.
- Prometheus có khả năng thu thập dữ liệu từ nhiều nguồn khác nhau như các máy chủ, dịch vụ, ứng dụng, và hệ thống. Nó sử dụng mô hình dữ liệu kiểu dữ liệu thời gian (time-series data model) để lưu trữ và truy vấn thông tin giám sát. Dữ liệu được thu thập bằng cách gửi các yêu cầu HTTP GET đến các endpoint của các ứng dụng, dịch vụ hoặc hệ thống muốn giám sát.
- Một trong những đặc điểm nổi bật của Prometheus là khả năng cung cấp truy vấn linh hoạt và mạnh mẽ thông qua PromQL (Prometheus Query Language). PromQL cho phép người dùng truy vấn và phân tích dữ liệu giám sát, từ việc lọc, ánh xạ, tính toán và trực quan hóa dữ liệu.
- Prometheus cũng cung cấp khả năng cảnh báo (alerting) để thông báo về các sự cố hoặc tình trạng không mong muốn trong hệ thống. Người dùng có thể xác định các quy tắc cảnh báo dựa trên các tiêu chí và ngưỡng đã định trước, và Prometheus sẽ gửi thông báo khi các điều kiện cảnh báo được kích hoạt.
- Hơn nữa, Prometheus cũng hỗ trợ tính năng ghi log (logging), tích hợp với các công cụ và dự án khác trong môi trường Cloud Native như Kubernetes, Docker, Grafana, và nhiều hệ thống khác.Prometheus là một hệ thống giám sát và cảnh báo mã nguồn mở mạnh mẽ, linh hoạt và có khả năng mở rộng, đáp ứng nhu cầu giám sát hệ thống phân tán hiện đại. Nó được sử dụng rộng rãi trong cộng đồng công nghệ để giám sát và quản lý hiệu suất của các ứng dụng và hạ tầng.
## 1.2.Grafana

# 2.Triển khai Promethues và Grafana
## 2.1.1.Cài đặt Promethues
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
## 2.1.2.Cấu hình Prometheus trên Ubuntu 22.04
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









