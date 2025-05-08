# Tìm hiểu về NFS (Network File System)

## 1. Khái niệm NFS
**NFS (Network File System)** là một giao thức lớp ứng dụng trong mô hình TCP/IP cho phép một máy tính truy cập tệp và thư mục từ một máy tính khác thông qua mạng như thể chúng nằm trên hệ thống cục bộ.

## 2. Mục đích sử dụng
- Chia sẻ tài nguyên lưu trữ (thư mục, tệp tin) giữa các máy trong mạng.
- Tạo ra một hệ thống tập tin dùng chung trong môi trường mạng (như văn phòng, trung tâm dữ liệu).
- Giúp tiết kiệm dung lượng lưu trữ cục bộ và tăng tính tập trung trong quản lý dữ liệu.

## 3. Nguyên lý hoạt động
- **Máy chủ NFS** chia sẻ một hay nhiều thư mục (gọi là **export**).
- **Máy khách NFS** sử dụng giao thức NFS để **mount** (gắn kết) thư mục đó vào hệ thống tệp của mình.
- Khi đã mount, người dùng có thể thao tác với các tệp tin như bình thường: mở, đọc, ghi, sửa,...

## 4. Cơ chế truyền thông
- NFS hoạt động trên nền tảng **RPC (Remote Procedure Call)** – gọi thủ tục từ xa.
- Máy khách gửi yêu cầu qua RPC đến máy chủ để thực hiện các thao tác như đọc, ghi, liệt kê thư mục...
- Giao thức vận hành chủ yếu qua UDP hoặc TCP.

## 5. Tính năng
- **Truy cập từ xa** như thể là truy cập cục bộ.
- **Đa người dùng** cùng truy cập.
- **Đồng bộ hóa dữ liệu** tức thời giữa client và server.
- **Hỗ trợ phân quyền truy cập**.

## 6. Ưu điểm
- Miễn phí, mã nguồn mở.
- Dễ tích hợp trong môi trường Linux/Unix.
- Quản lý tập trung dữ liệu hiệu quả.

## 7. Nhược điểm
- **Bảo mật thấp** nếu không cấu hình đúng (không mã hóa mặc định).
- **Hiệu năng phụ thuộc mạng**.
- **Không tối ưu cho môi trường Internet**, thích hợp hơn cho LAN.

## 8. Các phiên bản chính

| Phiên bản | Đặc điểm nổi bật |
|-----------|------------------|
| NFSv2     | Ra đời đầu tiên, giới hạn kích thước file 2GB, không hỗ trợ quyền truy cập chi tiết. |
| NFSv3     | Không trạng thái (stateless), hỗ trợ file lớn hơn, cải tiến hiệu năng và bảo mật. |
| NFSv4     | Có trạng thái (stateful), hỗ trợ xác thực mạnh hơn (Kerberos), hoạt động tốt hơn qua tường lửa. |

# Cài đặt NFS
- Cài đặt NFS
- ```
  sudo apt-get update -y
  sudo apt-get install nfs-kernel-server -y
  sudo apt-get install nfs-common -y
  ```
- ![image](https://github.com/user-attachments/assets/e10844e6-3eac-4c4e-99c4-3051c496040a)
- Sau khi cài xong bạn chạy các lệnh sau để bật kích hoạt và khởi động
- ```
  sudo systemctl enable nfs-kernel-server
  sudo systemctl start nfs-kernel-server
  sudo systemctl status nfs-kernel-server
  ```
- ![image](https://github.com/user-attachments/assets/82a52dd8-137f-46a2-9911-ca283af23ed9)
- ![image](https://github.com/user-attachments/assets/a17dc35f-0443-4db3-a70f-bf07695c75bd)
- Hướng dẫn kết nối
- Sử dụng 2 máy ảo:
- Máy chia sẻ file(Máy A) có ip 192.168.88.143, Thư mục cần chia sẻ: /root/lab_nfs
- Máy chia sẻ file(Máy B) có ip 192.168.88.142
- Trên máy chủ chia sẻ(A) tạo và phân quyền thư mục
- ```
  mkdir -p /root/lab_nfs
  chown nobody:nogroup /root/lab_nfs
  ```
- ![image](https://github.com/user-attachments/assets/d5c14d74-8984-435d-80b1-83e22eac447e)
- Mở cấu hình NFS
- `sudo nano /etc/exports`
- ![image](https://github.com/user-attachments/assets/519fde7f-8529-4d52-81e5-6fcc4c69adb9)
- ![image](https://github.com/user-attachments/assets/d17b282b-f77c-4d20-bcab-80bcf421f315)
- Khởi động lại dịch vụ để áp dụng cấu hình
- `sudo systemctl restart nfs-server`
- ![image](https://github.com/user-attachments/assets/fb8f91da-9627-4b1b-9c06-412995f6e1a4)
- Cấu hình NFS trên máy chủ được chia sẻ (B)
- Trên máy chủ nhận chia sẻ bạn hãy tạo thư mục để mount thư mục chia sẻ
- `sudo mkdir -p /mnt/lab_nfs`
- ![image](https://github.com/user-attachments/assets/b8e6dfc3-2922-4a15-896c-566a1de909a1)
- Tiếp theo sử dụng lệnh mount để kết nối với máy chủ NFS:
- `sudo mount 192.168.88.143:/root/lab_nfs /mnt/lab_nfs`
- Sau khi mount xong bạn hãy kiểm tra lại thư mục đã mount bằng lệnh `df -h`
- ![image](https://github.com/user-attachments/assets/5987ac2a-9b0d-4224-89cb-7cb618c190b8)
- Để ngắt kết nối nếu không sử dụng nữa, bạn sử dụng lệnh umount với cú pháp như sau. Lưu ý lệnh umount được chạy ở máy khách tức là máy chủ được chia sẻ (B). Và khi chạy lệnh bạn không được đứng trong thư mục, nếu không khi chạy umount bạn sẽ nhận được thông báo device is busy
- `sudo umount /mnt/lab_nfs`
- ![image](https://github.com/user-attachments/assets/7b056944-79a0-4dbe-a7b5-459d82cb5787)








