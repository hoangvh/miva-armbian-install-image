# MIVA Armbian Build

**Debian Bookworm build cho MIVA H618**

---

## 📦 Bước 1: Tải file cài đặt

- Vào [Release](https://github.com/hoangvh/miva-armbian-build/releases) trên GitHub.
- Tải file `Armbian_install.img.xz`.

![Hình minh họa bước 1](link-to-image-step1.png)

---

## 💽 Bước 2: Ghi image vào thẻ nhớ

- Sử dụng **Balena Etcher** để cài đặt image vào thẻ nhớ.
- Chọn image vừa tải và thẻ nhớ, nhấn **Flash**.

![Hình minh họa bước 2](link-to-image-step2.png)

---

## 🗂 Bước 3: Tạo phân vùng FAT32

- Trên Windows, mở **Disk Management**.
- Chọn thẻ nhớ, tạo phân vùng **FAT32**.
- Lưu ý: phân vùng này sẽ chứa file cấu hình và image của thiết bị.

![Hình minh họa bước 3](link-to-image-step3.png)

---

## 📂 Bước 4: Copy file cấu hình và image

1. Copy **init.conf** và file **image** của thiết bị H618 vào phân vùng FAT32 vừa tạo.  
2. Chỉnh lại tên file `image_file` trong **init.conf**:
   ```ini
   image_file=Tên_file.xz  # hoặc .gz / .img
