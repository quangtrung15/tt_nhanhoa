# 1.Tổng quan
## 1.2.Khái niệm
- Logical Volume Manager (LVM) : LVM là kỹ thuật quản lý việc thay đổi kích thước lưu trữ của ổ cứng. Là một phương pháp ấn định không gian ổ đĩa thành những logicalvolume khiến cho việc thay đổi kích thước của một phân vùng trở nên dễ dàng. Điều này thật dễ dàng khi bạn muốn quản lý công việc của mình tại riêng một phân vùng mà muốn mở rộng nó ra lớn hơn.
- Một số khái niệm liên quan:
+ Physical volume: là một đĩa cứng vật lý hoặc là partition
+ Volume group: là một nhóm các physical volume ( ổ đĩa ảo )
+ logical volume: là các phân vùng ảo của ổ đĩa ảo
- Một số lệnh cần thiết:
+ Lệnh fdisk : Dùng để quản lý việc phân vùng trong ổ cứng. Là một công cụ hữu dụng tron linux 
+ Lệnh mount : Dùng để gắn một phân vùng vào thư mục root để có thể sử dụng được nó
+ Lệnh dd : Dùng Sao lưu và hồi phục toàn bộ dữ liệu ổ cứng hoặc một partition và kiểm tra tốc độ đọc của kiểu lưu trữ dữ liệu trong LVM
## 1.3.Ưu điểm và Nhược điểm của LVM
- Ưu điểm :
+ Không để hệ thống bị gián đoạn hoạt động
+ Không làm hỏng dịch vụ
+ Có thể kế hợp swap
+ Có thể tạo ra các vùng dung lượng lớn nhỏ tuỳ ý.
- Nhược điểm:
+ Các bước thiết lập phức tạp và khó khăn hơn
+ Càng gắn nhiều đĩa cứng và thiết lập càng nhiều LVM thì hệ thống khởi động càng lâu.
+ Khả năng mất dữ liệu cao khi một trong số các đĩa cứng bị hỏng.
+ Windows không thể nhận ra vùng dữ liệu của LVM. Nếu Dual-boot ,Windows sẽ không thể truy cập dữ liệu trong LVM.
## 1.4.3. Những thành phần trong LVM
- HDD : là một thiết bị lưu trữ máy tính. Nó là loại bộ nhớ không thay đổi và không bị mất dữ liệu khi ta ngừng cung cấp nguồn điện cho chúng
- Partition: là các phân vùng của ổ cứng. Mỗi một ổ cứng có 4 partition. Trong đó bao gồm 2 loại là primary partition và extended partition
+ primary partition: còn được gọi là phân vùng chính, có thể khởi động và mỗi ổ cứng chỉ có tối đa 4 phân vùng này
+ extended partition: Hay còn được gọi là phân vùng mở rộng của ổ cứng
- Cách thức hoạt động các tầng của LVM:
+ Tầng đầu tiên : hard drives là tầng các disk ban đầu khi chưa chia phân vùng
+ Partitions: Sau đó ta chia các disk ra thành các phân vùng nhỏ hơn
+ Physical volume : từ một partitions ta sẽ tạo ra được một physical
+ group volume : Ta sẽ ghép nhiều physical volume thành một group volume
+ Logical volume : Ta sẽ có thể tạo ra được logical volume
# 2.Triển khai LVM
- Sử dụng LVM với Ubuntu Server 22.04 trong môi trường VMWARE với 03 ổ đĩa được thêm
- ![image](https://github.com/user-attachments/assets/31c21a25-cbab-47af-80f7-2368fc34bdf0)
- Kiểm tra các Hard Drives có trên hệ thống
- `lsblk`
- ![image](https://github.com/user-attachments/assets/f4a18507-bbf7-4e3c-a994-f7800b572884)
## 2.1.Tạo partition
- Từ sdb và sdc khởi tạo bằng cách sử dụng lệnh
- `fdisk /dev/sdb`
- ![image](https://github.com/user-attachments/assets/a5c2d323-e2bf-4a4a-b487-61dc2b81ee3b)
- Thực hiện thao tác tương tự với sdc
- Kết quả thu được 2 partition sdb1 sdc1
- ![image](https://github.com/user-attachments/assets/92923a3f-1857-46d2-a837-fe7a794770d9)
## 2.2.Tạo physical volume
- Từ sdb1 và sdc1 khởi tạo và kiểm tra:
- Khởi tạo
- `sudo pvcreate /dev/sdb1 /dev/sdc1`
- Kiểm tra
- `sudo pvs`
## 2.3.Tạo volume group
- Khởi tạo
- `vgcreate vg_anth1 /dev/sdb1 /dev/sdc1`
- Kiểm tra
- `sudo vgs`
- ![image](https://github.com/user-attachments/assets/f16c45bd-c1ee-459a-932c-a9872b084ff3)
## 2.4.Tạo logical volume
- Tạo 2 lv có tên lv-demo1 lv-demo2 từ vg vg_anth1 mỗi lv có dung lượng 1g
- ```
  lvcreate -L 1G -n lv-demo1 vg_anth1
  lvcreate -L 1G -n lv-demo2 vg_anth1
  ```
- Kiểm tra
- `sudo lvs`
- ![image](https://github.com/user-attachments/assets/55f3fb55-5b56-4b5f-b9da-7c3830ea2ef4)
## 2.5.Tạo filesystem trên logical volume
- `mkfs -t ext4 /dev/vg_anth1/lv-demo1`
- ![image](https://github.com/user-attachments/assets/7c7cfa62-46d7-48ae-aa4f-70f0cff53a65)
## 2.6.Chỉnh sửa fstab để tự động mount phân vùng
- ```
  sudo mkdir demo1
  sudo mount /dev/vg_anth1/lv-demo1 demo1
  ```
- ![image](https://github.com/user-attachments/assets/8bcaa95f-6860-49ab-b48e-98cd858735ad)
## 2.7.Mở rộng logical volume
- Cần đảm bảo vg còn dung lượng trống
- Kiểm tra
- `vgs`
- ![image](https://github.com/user-attachments/assets/a449e260-bdad-4854-b084-40a29fff030d)
- Trường hợp này dư 1.99G -> mở rộng lv với dung lượng lấy từ vg
- ![image](https://github.com/user-attachments/assets/f1c6fc53-db92-47f1-9327-2ead488fff53)
- ![image](https://github.com/user-attachments/assets/ceaf102e-9513-4678-bb73-51370d9cd589)
## 2.8.Thêm ổ cứng mở rộng logical volume
- ```
  fdisk /dev/sdd
  sudo pvcreate /dev/sdd1
  ```
- ![image](https://github.com/user-attachments/assets/c7d117c5-9999-4b94-89b7-834477173a38)
- Extend pv vừa tạo vào vg
- `vgextend vg_anth1 /dev/sdd1`
- ![image](https://github.com/user-attachments/assets/847d6bc6-b0b7-4088-ba12-078f82307540)
## 2.9.Thay thế 1 ổ cứng ra khỏi hệ thống LVM
- Di chuyển dữ liệu khỏi ổ
- `sudo pvmove /dev/sdb1`
- ![image](https://github.com/user-attachments/assets/b4def0ef-5781-4ae5-95c0-b5980624564e)
- Gỡ khỏi Volume Group
- `sudo vgreduce vg_anth1 /dev/sdb1`
- ![image](https://github.com/user-attachments/assets/a0fb3b2b-8ca0-4254-b5f5-db6df5837db3)
- Sử dụng cho mục đích khác hoặc xóa partition Volumes
- `sudo pvremove /dev/sdb1`
- ![image](https://github.com/user-attachments/assets/72be386c-5ed0-4f43-8b89-41d476c83f12)
## 2.10.Xóa logical volume, xóa volume group, xóa physical volume
- Xóa Logical Volume: Trước tiên ta phải Umount Logical Volume
- `umount /dev/vg_anth1/lv-demo1`
- Sau đó tiến hành xóa Logical Volume bằng câu lệnh sau
- `lvremove /dev/vg_anth1/lv-demo1`
- ![image](https://github.com/user-attachments/assets/143881b6-4e79-47bc-9377-0025e7bec165)
- Xóa Volume Group
- `vgremove /dev/vg-demo1`
- Xóa Physical Volume
- ```
  pvremove /dev/sdc1
  pvremove /dev/sdd1
  ```
- ![image](https://github.com/user-attachments/assets/74f2ca65-1807-4ae9-8bf0-7fbcaf4f4be5)












