# Triển khai LVM
- Sử dụng LVM với Ubuntu Server 22.04 trong môi trường VMWARE với 03 ổ đĩa được thêm
- ![image](https://github.com/user-attachments/assets/31c21a25-cbab-47af-80f7-2368fc34bdf0)
- Kiểm tra các Hard Drives có trên hệ thống
- `lsblk`
- ![image](https://github.com/user-attachments/assets/f4a18507-bbf7-4e3c-a994-f7800b572884)
- Tạo partition
- Từ sdb và sdc khởi tạo bằng cách sử dụng lệnh
- `fdisk /dev/sdb`
- ![image](https://github.com/user-attachments/assets/a5c2d323-e2bf-4a4a-b487-61dc2b81ee3b)
- Thực hiện thao tác tương tự với sdc
- Kết quả thu được 2 partition sdb1 sdc1
- ![image](https://github.com/user-attachments/assets/92923a3f-1857-46d2-a837-fe7a794770d9)
## Tạo physical volume
- Từ sdb1 và sdc1 khởi tạo và kiểm tra:
- Khởi tạo
- `sudo pvcreate /dev/sdb1 /dev/sdc1`
- Kiểm tra
- `sudo pvs`
## Tạo volume group
- Khởi tạo
- `vgcreate vg_anth1 /dev/sdb1 /dev/sdc1`
- Kiểm tra
- `sudo vgs`
- ![image](https://github.com/user-attachments/assets/f16c45bd-c1ee-459a-932c-a9872b084ff3)
## Tạo logical volume
- Tạo 2 lv có tên lv-demo1 lv-demo2 từ vg vg_anth1 mỗi lv có dung lượng 1g
- ```
  lvcreate -L 1G -n lv-demo1 vg_anth1
  lvcreate -L 1G -n lv-demo2 vg_anth1
  ```
- Kiểm tra
- `sudo lvs`
- ![image](https://github.com/user-attachments/assets/55f3fb55-5b56-4b5f-b9da-7c3830ea2ef4)
## Tạo filesystem trên logical volume
- `mkfs -t ext4 /dev/vg_anth1/lv-demo1`
- ![image](https://github.com/user-attachments/assets/7c7cfa62-46d7-48ae-aa4f-70f0cff53a65)
## Chỉnh sửa fstab để tự động mount phân vùng
- ```
  sudo mkdir demo1
  sudo mount /dev/vg_anth1/lv-demo1 demo1
  ```
- ![image](https://github.com/user-attachments/assets/8bcaa95f-6860-49ab-b48e-98cd858735ad)
## Mở rộng logical volume
- Cần đảm bảo vg còn dung lượng trống
- Kiểm tra
- `vgs`
- ![image](https://github.com/user-attachments/assets/a449e260-bdad-4854-b084-40a29fff030d)
- Trường hợp này dư 1.99G -> mở rộng lv với dung lượng lấy từ vg
- ![image](https://github.com/user-attachments/assets/f1c6fc53-db92-47f1-9327-2ead488fff53)










