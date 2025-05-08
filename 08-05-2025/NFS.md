# Cài đặt NFS
- Cài đặt NFS
- ```
  apt-get update -y
  apt-get install nfs-kernel-server -y
  apt-get install nfs-common -y
  ```
- ![image](https://github.com/user-attachments/assets/e10844e6-3eac-4c4e-99c4-3051c496040a)
- Sau khi cài xong bạn chạy các lệnh sau để bật kích hoạt và khởi động
- ```
  systemctl enable nfs-kernel-server
  systemctl start nfs-kernel-server
  systemctl status nfs-kernel-server
  ```
- ![image](https://github.com/user-attachments/assets/82a52dd8-137f-46a2-9911-ca283af23ed9)
