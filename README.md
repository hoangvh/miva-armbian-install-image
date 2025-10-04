# Tạo thẻ SD bộ cài cho Allwiner H618 (Miva -Mira)

---
## 📦 Bước 1: Tải file cài đặt

- Vào [Release](https://github.com/hoangvh/miva-armbian-build/releases) trên GitHub.
- Tải file `installer_unofficial*.img.xz` để tạo bộ cài đặt tự động trên thẻ sd
- Tải file `miva_unofficial.img.xz` để copy firmware từ thẻ sd vào emmc trên thiết bị.

---

## 💽 Bước 2: Ghi image vào thẻ nhớ

- Sử dụng **Balena Etcher** để cài đặt image vào thẻ nhớ.
- Chọn image vừa tải và thẻ nhớ, nhấn **Flash**.

![Hình minh họa bước 2](images/balena-etcher.png)

---

## 🗂 Bước 3: Tạo phân vùng FAT32 trên Windows 10/11

- Nhấn Windows, gõ disk management để mở **Disk Management**.
- Chọn thẻ nhớ, bấm chuột phải vào phân vùng **Unallocated** chọn **New Simple Volume**... -> chọn *Next*.
  
 ![Hình minh họa bước 3](images/disk-management.png)
 
- Chọn các tham số như hình minh họa dưới -> bấm *Next* -> *Finish*.

 ![Hình minh họa bước 3](images/format_fat32.png)

- Lưu ý: phân vùng này sẽ chứa file cấu hình và image của thiết bị.

---

## 📂 Bước 4: Copy file cấu hình và image

1. Copy **init.conf** và file **firmware** của thiết bị H618 vào phân vùng FAT32 vừa tạo trên thẻ.
 ![Hình minh họa bước 4](images/sdcard.png)
2. Đặt lại giá trị `image_file` trong **init.conf** giống với tên file miva vừa copy vào:
   ```ini
   image_file=Tên_file.xz  # hoặc .gz / .img
   
## 📂 Bước 5: Cài đặt firmware vào eMMC

1. Cắm thẻ vào khe sdcard trên thiết bị H618, cấp nguồn.
2. Truy cập SSH vào thiết bị tại địa chỉ ip: 192.168.11.102 hoặc UART
3. Gõ lệnh để kiểm tra quá trình cài đặt firmware vào emmc
   ```ini
   journalctl -u sd_install.service -f
   
![Hình minh họa bước 4](images/ssh.png)
-  Nếu log thông báo `All data synced to eMMC.` là đã cài đặt xong
4. Các trạng thái đèn ERR (led màu đỏ):
- Đèn ERR nháy nhanh: đang cài đặt.
- Đèn ERR nháy chậm: cài đặt xong.
- Đèn ERR không nháy: Lỗi đèn.
- Đèn ERR không chuyển sang nháy chậm: Kiểm tra lại file miva hoặc tên file trong init.conf
5. Tắt thiết bị:
- Gõ lệnh `shutdown -h now`
- Chờ cho đèn tắt hẳn rồi rút nguồn, rút thẻ nhớ.
- Chuẩn bị bước thiết lập cài đặt lần đầu trên thiết bị
  
## 📂 Bước 6: Cài đặt ứng dụng

1. Cắm các ăng-ten kết nối 4G, wifi, dây mạng. Cấp nguồn cho thiết bị.
2. Ứng dụng (**miva/mira**) sẽ tự động cài đặt.
3. Địa chỉ IP cổng ethernet mặc định `192.168.11.102/24`.

## 📂 Một số lệnh dùng để debug:
- `docker ps`: kiểm tra tên ứng dụng miva trong docker
- `ip a`: hiển thị ip của mạng LAN - eth0 (mặc định 192.168.11.102) , module 4G - eth1 (mặc định: 192.168.0.100), wifi (nếu bật) - wlan0
- `docker exec -it -u0 miva`: truy cập vào docker container, gõ `login`, điền username/pasword để truy cập openwrt.
