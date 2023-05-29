* برای تنظیم هدر X-Content-Type-Options در آپاچی، تنظیمات زیر را به فایل پیکربندی VirtualHost وارد کنید:
```config
    Header always set X-Content-Type-Options "nosniff"
```
