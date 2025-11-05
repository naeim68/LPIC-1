# 🧪 Lab 02 — Permissions Practical

## 🎯 هدف
تمرین مالکیت، مجوزها و بیت‌های خاص در محیط واقعی.

## سناریو و مراحل
```bash
mkdir -p /tmp/perm-lab && cd /tmp/perm-lab
touch a.sh b.txt
groupadd -f devs
useradd -M -N -s /usr/sbin/nologin tempuser 2>/dev/null || true

# مالکیت و مجوزهای پایه
chown tempuser:devs a.sh
chmod 640 b.txt
chmod 755 a.sh

# بیت‌های خاص
chmod u+s a.sh         # SUID روی فایل اجرایی
mkdir shared && chmod 1777 shared   # Sticky روی دایرکتوری عمومی

# انتقال مجوز از مرجع
chmod --reference=a.sh b.txt

# بررسی
ls -l
namei -om a.sh || true
```

## اعتبارسنجی
- `a.sh` باید `rwsr-xr-x` باشد (s روی ستون owner).  
- `shared` باید `rwxrwxrwt` داشته باشد (Sticky).

## پاکسازی
```bash
userdel -r tempuser 2>/dev/null || true
rm -rf /tmp/perm-lab
```