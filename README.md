# 🚀 آموزش نصب Grafana برای پنل مرزبان
| Name     | Version          |
|----------|-----------------|
| Marzban  | ✅ v0.8.4 (تست شده) |
| MySQL    | ✅               |
| MariaDB  | ✅               |
| SQLite   | ❌ Not Supported |
## 1️⃣ ساخت فولدرها و فایل داکرکامپوز
ابتدا دستور زیر را اجرا کنید تا فولدرها و فایل‌های مورد نیاز ساخته شوند:

```bash
mkdir -p /opt/stacks/grafana/data && cd /opt/stacks/grafana && sudo chown -R 472:472 data && nano compose.yaml
```

---

## 2️⃣ ایجاد فایل و ذخیره
بعد از باز شدن فایل `compose.yaml`، محتوای زیر را داخل آن قرار دهید:

```yaml
services:
  grafana:
    image: grafana/grafana-oss:latest
    container_name: grafana
    network_mode: host
    environment:
      - GF_SERVER_HTTP_PORT=2001
    volumes:
      - ./data:/var/lib/grafana
    restart: always
```

📌 **نکته:** می‌توانید به‌جای پورت `2001`، عدد دلخواه خود را قرار دهید.

---

## 3️⃣ اجرای پنل Grafana
برای اجرای پنل، از دستور زیر استفاده کنید:

```bash
docker compose up -d
```

اگر با خطا مواجه شدید، این دستور را امتحان کنید:

```bash
docker-compose up -d
```

پس از اجرا، می‌توانید با آدرس زیر وارد پنل شوید:

```
http://YourDomain.Com:2001
```

🛡️ **نام کاربری و رمز عبور پیش‌فرض:** `admin` / `admin` (بعد از ورود باید رمز جدید تنظیم کنید.)

---

## 🔧 تنظیمات MySQL در Grafana
1️⃣ به بخش `Connection` رفته و `MySQL` را انتخاب کنید، سپس روی **Add New Data Source** کلیک کنید.

2️⃣ در کادر `Host URL *` یکی از موارد زیر را وارد کنید:

```
localhost:3306
```

یا

```
127.0.0.1:3306
```

3️⃣ در کادر `Database Name`، نام دیتابیس مرزبان یعنی `marzban` را وارد کنید.

4️⃣ در کادر `Username *` مقدار `root` را قرار دهید.

5️⃣ در کادر `Password`، پسورد `root` را از داخل فایل `.env` مرزبان پیدا کنید.

6️⃣ روی **Save & Test** کلیک کنید. اگر متن سبزرنگ نمایش داده شد، تنظیمات صحیح هستند! ✅

---

## 📊 نصب داشبورد مانیتورینگ
1️⃣ به مسیر `Dashboards` بروید و روی **New** کلیک کنید، سپس **Import** را انتخاب کنید.

2️⃣ به مخزن گیت‌هاب **Marzban-Grafana** بروید و فایل **JSON** مورد نظر را کپی کنید.

3️⃣ در پنل Grafana، گزینه **Import via dashboard JSON model** را انتخاب کرده و JSON کپی شده را **Paste** کنید.

4️⃣ روی **Load** کلیک کنید و در قسمت **Data Source**، دیتابیس `MySQL` که قبلاً اضافه کردید را انتخاب کنید.

5️⃣ روی **Import** بزنید و تبریک! 🎉 پنل مانیتورینگ شما آماده است. 🚀

📌 **داشبوردهای موجود در گیت‌هاب:**
- برای **ادمین اصلی**: `Marzban-Sudo.json`
- برای **نمایندگان**: `Marzban-CS.json` (بعد از نصب، باید **ID ادمین** را از قسمت تنظیمات و بخش **Variables** تنظیم کنید تا اطلاعات به‌درستی نمایش داده شوند.)

---

## 🗑️ حذف Grafana در صورت نیاز
📌 اگر از **Dockge** استفاده می‌کنید، کافی است روی دکمه **Delete** کلیک کنید.

📌 در غیر این صورت، دستورات زیر را اجرا کنید:

```bash
docker stop grafana
docker rm grafana
rm -rf /opt/stacks/grafana
```

---

# پنل برای ادمین اصلی
![image](https://github.com/user-attachments/assets/5ea3b3f9-ae5c-4926-b0ac-31f586ea024c)

# پنل برای نمایندگان
برای پنل نماینده بعد از نصب از قسمت Settings => Variable باید ایدی اون ادمینی که میخاین اطلاعاتش رو نمایش بده رو وارد کنید که از داخل دیتابیس مرزبان قسمت ادمین ها میتونید ایدی رو پیدا کنید
![image](https://github.com/user-attachments/assets/5748c82c-b692-4622-b4b1-b16517a86c8e)

# سایراموزش ها:
https://t.me/MarzbanPro

