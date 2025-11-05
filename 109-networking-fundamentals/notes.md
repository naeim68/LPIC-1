# 🌍 Networking Fundamentals — Ping, DNS, DHCP, NAT

## Ping
برای تست ارتباط:
```bash
ping -c 4 google.com
ping 8.8.8.8
```

## DNS (Name Resolution)
- تبدیل نام دامنه به IP
- ابزارها: `dig`, `host`, `nslookup`
```bash
dig A google.com +short
dig www.example.com ANY
```

## سرویس‌ها
| سرویس | کارکرد |
|:--|:--|
| DNS | Name Resolution |
| NAT | تبدیل آدرس‌ها برای اشتراک اینترنت |
| DHCP | تخصیص خودکار IP/Gateway/DNS |

## ابزارهای پایه شبکه
| ابزار | کاربرد | مثال |
|:--|:--|:--|
| `ip addr` | نمایش/تنظیم IP | `ip addr show` |
| `ip route` | روتینگ | `ip route` |
| `ss -tulpn` | سوکت‌ها/پورت‌ها | `ss -tulpn` |
| `traceroute` | مسیر تا مقصد | `traceroute 8.8.8.8` |
