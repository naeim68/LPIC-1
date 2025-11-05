# 💽 Devices & Filesystems — پارتیشن، فایل‌سیستم، Swap، Mount

## Partition Tables
| نوع | ویژگی | محدودیت |
|:--|:--|:--|
| **MBR** | قدیمی، ساده | <2TB، حداکثر 4 Primary |
| **GPT** | مدرن | ≥2TB، تا 128 پارتیشن |

## انواع پارتیشن در MBR
Primary، Extended (حاوی Logical)، Logical (`/dev/sdb5` به بعد)

## شناسایی دیسک/پارتیشن
```bash
fdisk -l /dev/sda
ls /dev
ls /dev/sd*
lsblk
lsblk -f     # همراه FS/UUID
```

## فایل‌سیستم‌ها
| نوع | ویژگی |
|:--|:--|
| ext4 | پیش‌فرض سریع و پایدار |
| btrfs | snapshot/RAID نرم‌افزاری |
| vfat | سازگار با Windows |
| iso9660 | رسانه نوری |
| nfs | شبکه‌ای |
| swap | فضای مبادله |

## فرمت کردن/برچسب/UUID
```bash
mkfs -t ext4 /dev/sdb1
mkfs.ext4 /dev/sdb6
lsblk -f
tune2fs -L data /dev/sdb1        # برچسب
tune2fs -l /dev/sdb5 | grep UUID  # UUID
```

## RAM و Swap
RAM برای پردازش‌های فعال است؛ کمبود RAM با Swap جبران می‌شود.

### فایل Swap
```bash
dd if=/dev/zero of=/swapfile bs=1M count=1024
mkswap /swapfile
swapon /swapfile
swapoff /swapfile
free -h
```
ورود پایدار در fstab:
```
/swapfile none swap sw 0 0
```

### پارتیشن Swap
```bash
mkswap /dev/sdb2
swapon /dev/sdb2
swapoff /dev/sdb2
```

---

# 🧪 Lab 01 — Mount Persistence (با loop device)

## 🎯 هدف
Mount پایدار و تست `fstab` بدون نیاز به دیسک واقعی.

## مراحل
```bash
sudo mkdir -p /mnt/data1
sudo dd if=/dev/zero of=/tmp/disk.img bs=1M count=64
sudo mkfs.ext4 /tmp/disk.img
sudo blkid /tmp/disk.img
echo "/tmp/disk.img /mnt/data1 ext4 loop,defaults 0 0" | sudo tee -a /etc/fstab
sudo mount -a
mount | grep data1
```

## پاکسازی
```bash
sudo sed -i '/disk.img/d' /etc/fstab
sudo umount /mnt/data1
sudo rm -f /tmp/disk.img
```
