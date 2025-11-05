# 👤 Users & Groups — مدیریت کاربران، گروه‌ها و فایل‌های سیستمی

## فایل‌های کلیدی
- `/etc/passwd`, `/etc/shadow`, `/etc/group`, `/etc/gshadow`

نمونه‌ی `/etc/passwd`:
```bash
naeim:x:1002:1002::/home/naeim:/bin/bash
```

## دستورات پایه
| دستور | توضیح |
|:--|:--|
| `sudo -i` | ورود به محیط root |
| `passwd [username]` | تغییر پسورد |
| `whoami` | نمایش کاربر فعلی |

## گروه‌ها و کاربران
```bash
groupadd IT
groupadd web
groupadd developer

useradd -d /home/farhad -m -g IT -G web,developer -c "farhad yousefi" -s /bin/bash farhad
passwd farhad
```

## مدیریت حساب
```bash
usermod -L farhad   # قفل کردن
usermod -U farhad   # باز کردن
userdel -r farhad   # حذف کامل
```

## Shadowing
```bash
pwunconv   # غیرفعال کردن shadow
pwconv     # فعال‌سازی shadow
grpunconv  # غیرفعال کردن gshadow
grpconv    # فعال‌سازی gshadow
```

## پسورد هش‌شده
```bash
useradd -d /home/naeim -m -g developer -G IT,web -p $(mkpasswd -m sha-512 "linux") -s /bin/bash naeim
```
