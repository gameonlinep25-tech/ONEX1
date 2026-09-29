# راهنمای نصب و استقرار ONEX

## روش اول: نصب محلی (Local)

### پیش‌نیازها
- Python 3.9+
- pip
- git (اختیاری)

### مراحل

```bash
# ۱. دانلود یا استخراج پروژه
cd ONEX-main

# ۲. نصب وابستگی‌ها
pip install -r requirements.txt

# ۳. اجرای برنامه
python app.py
```

**دسترسی:** http://localhost:8000
- **نام کاربری:** admin
- **رمز:** admin

---

## روش دوم: استقرار روی Railway (توصیه‌شده)

### مراحل

#### ۱. آماده‌سازی مخزن
```bash
# اگر git استفاده می‌کنید:
git init
git add .
git commit -m "Initial ONEX setup"
git branch -M main
git remote add origin https://github.com/yourname/onex.git
git push -u origin main
```

#### ۲. وارد Railway شوید
1. [railway.app](https://railway.app) را بازکنید
2. **Sign up** یا **Login** کنید
3. **New Project** کلیک کنید

#### ۳. استقرار
1. **Deploy from GitHub** انتخاب کنید
2. **Authorize Railway** کنید
3. مخزن ONEX را انتخاب کنید
4. Railway خودکار نصب می‌کند

#### ۴. متغیرهای محیطی
در تنظیمات پروژه اضافه کنید:
```
PORT=8000
RAILWAY_VOLUME_MOUNT_PATH=/data
```

#### ۵. دسترسی
1. روی **Deployments** کلیک کنید
2. **View Logs** برای بررسی
3. دامنه Railway استفاده کنید یا دامنه سفارشی اضافه کنید

---

## روش سوم: Docker

### Dockerfile
```dockerfile
FROM python:3.9-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
EXPOSE 8000
CMD ["python", "app.py"]
```

### اجرا
```bash
docker build -t onex:1.3.9 .
docker run -p 8000:8000 -v data:/data onex:1.3.9
```

---

## روش چهارم: VPS (Ubuntu/Debian)

### پیش‌نیازها
```bash
sudo apt update
sudo apt install python3 python3-pip python3-venv
```

### نصب
```bash
# دانلود و استخراج
unzip onex-v1.3.9-clean.zip
cd ONEX-main

# ایجاد محیط مجازی
python3 -m venv venv
source venv/bin/activate

# نصب وابستگی‌ها
pip install -r requirements.txt
```

### اجرا با Systemd
```bash
sudo nano /etc/systemd/system/onex.service
```

محتوا:
```ini
[Unit]
Description=ONEX VPN Panel
After=network.target

[Service]
Type=simple
User=youruser
WorkingDirectory=/path/to/ONEX-main
ExecStart=/path/to/ONEX-main/venv/bin/python app.py
Restart=on-failure
RestartSec=10s

[Install]
WantedBy=multi-user.target
```

فعال‌سازی:
```bash
sudo systemctl daemon-reload
sudo systemctl enable onex
sudo systemctl start onex
```

---

## Nginx Reverse Proxy

```nginx
server {
    listen 80;
    server_name your-domain.com;

    location / {
        proxy_pass http://localhost:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

---

## HTTPS با Cloudflare

1. دامنه را به Cloudflare منتقل کنید
2. **SSL/TLS** → **Full** انتخاب کنید
3. **DNS** را به Railway اشاره دهید
4. HTTPS خودکار فعال می‌شود

---

## تنظیم بروزرسانی خودکار

### Railway Webhook
1. در پنل → **تنظیمات** → **بروزرسانی**
2. **GitHub Webhook URL** کپی کنید
3. در GitHub → Settings → Webhooks
4. اضافه کنید

### مدیریت داده‌ها

#### پشتیبان‌گیری
1. در پنل → **تنظیمات** → **پشتیبان‌گیری**
2. **دانلود تمام اطلاعات** کلیک کنید
3. فایل `backup.json` دانلود می‌شود

#### بازیابی
1. **پشتیبان‌گیری** → **آپلود**
2. فایل backup را انتخاب کنید
3. تایید کنید

---

## حل مشکلات نصب

### Error: Python version
```bash
python3 --version  # باید ۳.۹ یا بالاتر باشد
```

### Error: pip modules
```bash
pip install --upgrade pip
pip install -r requirements.txt --force-reinstall
```

### Port in use
```bash
lsof -i :8000  # چه فرآیندی؟
kill -9 <PID>
```

### Database locked
```bash
rm data/pixonpanel_state.json  # حذف و شروع مجدد
```

---

## چک‌لیست نصب

- [ ] Python 3.9+ نصب شده
- [ ] وابستگی‌ها نصب شدند
- [ ] پورت ۸۰۰۰ آزاد است
- [ ] پنل در http://localhost:8000 دسترس‌پذیر است
- [ ] ادمین وارد شده است
- [ ] رمز پیش‌فرض تغییر کرد
- [ ] Nginx/Proxy پیکربندی شد
- [ ] SSL/HTTPS فعال است
- [ ] ربات تلگرام پیکربندی شد (اختیاری)
- [ ] پشتیبان‌گیری روی Railway فعال است

---

**شروع شده‌اید! 🎉**
