# ONEX Project Cleanup & Fixes (v1.3.9)

## تغییرات انجام شده

### 1. ✓ ورژن نسخه
- **قبل:** 1.3.8
- **بعد:** 1.3.9

### 2. ✓ فایل‌های اضافی حذف شده
- `main.py.bak` (backup، غیرضروری)
- `all.js` و `all_unescaped.js` (فایل‌های تجمیع‌نشده)
- `protocol_core.py`, `relay_vless.py`, `speed_limit.py`, `xhttp_siz10.py` (stub files)
- `archive/` (پوشه خالی legacy)
- `docs/`, `frontend/` (پوشه‌های خالی یا build artifacts)
- `protocol_icons/` (تکراری با assets/protocols)
- `onex-panel-logo.png` (تکراری)

### 3. ✓ ساختار پوشه‌های بهینه شده
```
ONEX-main/
├── app.py (main application)
├── xhttp.py (xhttp module)
├── requirements.txt
├── pyproject.toml
├── version.json
├── README.md, README.fa.md, README.en.md
├── assets/
│   └── protocols/ (تمام آیکون‌های پروتکل)
├── config/ (پیکربندی)
├── onex/ (core modules)
└── scripts/ (اسکریپت‌های کمکی)
```

### 4. ✓ مشکل اعلان‌ها (Notification Panel)
**مشکل:** منو اعلان‌ها پشت نوار داشبورد می‌رفت و نصفش قطع می‌شد

**علت:** 
- `.top-notify-panel` با `position:absolute` بود (نسبی به `.onex-topbar`)
- `.onex-topbar` خود تو `.main` نشسته بود
- `z-index` کافی نبود

**حل:**
- تغییر به `position:fixed` (نسبی به viewport)
- `z-index:2100` تنظیم شد
- موقعیت `top:75px` برای داشبورد، `top:66px` برای موبایل

### 5. ✓ مشکل بروزرسانی (Update Panel)
**مشکل:** "بروزرسانی ناموفق" و منتظر کاربر برای کلیک دوم بود

**حل:**
- خودکار شدن `panelUpdate()` (بدون modal)
- بهتر شدن error handling در `deployPanelUpdate()`
- نمایش پیام خطا اگه `/api/update/deploy` ناموفق باشد
- reload خودکار بعد از ۱۲ ثانیه

### 6. ✓ مشکل اعلان‌های Update (Modal)
**مشکل:** اعلان نسخه جدید پشت نوار‌های دیگر می‌افتاد

**حل:**
- `z-index:2200` برای modal
- `position:fixed` تضمین‌شد
- backdrop-filter صحیح‌شد

## نتایج
- ✓ حجم پروژه: ۲.۱ MB → ۱.۱ MB
- ✓ تمام فیچرها سالم
- ✓ ساختار تمیز و منظم
- ✓ موارد UI درست‌شده

## فایل اصلی
**app.py** (۹۷۷ KB) حاوی:
- Dashboard HTML + CSS (fixed)
- Login page HTML + CSS
- تمام JavaScript functionality
- تمام API endpoints
