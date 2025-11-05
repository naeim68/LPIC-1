# 🧪 Lab 01 — Mount Persistence

## 🎯 هدف
نصب فایل‌سیستم به‌صورت پایدار با `/etc/fstab` و اعتبارسنجی پس از mount.

## گام‌ها
```bash
lsblk -f
sudo mkdir -p /mnt/data
sudo mount /dev/sdb5 /mnt/data

# با UUID در fstab
UUID=<YOUR-UUID>  /mnt/data  ext4  defaults  0  2

sudo mount -a
df -h | grep /mnt/data
```
## نکته
برای آزمایش بدون دیسک واقعی از loop device استفاده کن (سناریوی فایل img در notes).