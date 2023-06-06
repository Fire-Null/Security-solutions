### غیرفعال کردن پروتکل ضعیف ssl/tls در nginx
##### پیاده‌سازی SSL به معنای ایمن بودن سایت شما نیست. نسخه‌های منسوخ SSL مانند TLS 1.0، TLS 1.1 ضعیف شناخته می‌شوند و این پروتکل‌ها به آسیب‌پذیری‌های SSL و TLS مانند POODLE، BEAST و CRIME تمایل دارند.
###### متداول‌ترین مرورگرهای وب مانند کروم، فایرفاکس، safari و edge دیگر از TLS 1.0 و TLS 1.1 پشتیبانی نمی‌کنند.
* برای پیاده‌سازی TLS 1.2 و TLS 1.3، باید دو فایل config را ویرایش کنیم:
* * /etc/nginx/nginx.conf
* * /etc/nginx/sites-available/default
* خط زیر را در فایل nginx.conf بیابید
```bash
ssl_protocols TLSv1 TLSv1.1 TLSv1.2; # Dropping SSLv3, ref: POODLE
```
* و TLS نسخه 1 و 1.1 را حذف کنید و TLS 1.3 را اضافه کنید
```bash
ssl_protocols TLSv1.2 TLSv1.3; # Dropping SSLv3, ref: POODLE
```
* با این حال، پروتکل‌های منسوخ شده نیز ممکن است در فایل‌های پیکربندی بلوک سرور Nginx شما وجود داشته باشد. فایل‌های پیکربندی بلوک در دایرکتوری /etc/nginx/sites-available/ قرار دارند.

> با این حال، پروتکل‌های منسوخ شده نیز ممکن است در فایل‌های پیکربندی بلوک سرور Nginx شما وجود داشته باشد. فایل‌های پیکربندی بلوک در دایرکتوری /etc/nginx/sites-available/ قرار دارند. خط زیر را پیدا کنید:
```bash
ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
```
* مانند قبل، پروتکل TLSv1 و TLSv1.1 را حذف کرده و TLSv1.3 را اضافه کنید.
```bash 
ssl_protocols TLSv1.2 TLSv1.3;
```
#### غیرفعال کردن Cipherهای ضعیف در nginx
##### Cipher suiteهای ضعیف ممکن است منجر به آسیب‌پذیری شوند، و به عنوان راهکار امن، باید مطمئن شویم که فقط cipherهای قوی مجاز هستند.
* موارد زیر را به بلوک سرور در فایل ssl.conf اضافه کنید
```bash 
ssl_ciphers "EECDH+ECDSA+AESGCM EECDH+aRSA+AESGCM EECDH+ECDSA+SHA384 EECDH+ECDSA+SHA256 EECDH+aRSA+SHA384 EECDH+aRSA+SHA256 EECDH+aRSA+RC4 EECDH EDH+aRSA HIGH !RC4 !aNULL !eNULL !LOW !3DES !MD5 !EXP !PSK !SRP !DSS";
```
