* برای تنظیم ***Content-Security-Policy*** در آپاچی،  کد زیر را به فایل پیکربندی موجود در ***VirtualHost*** خود اضافه کنید:

```config
    Header always set Content-Security-Policy "default-src 'self';"

    Header always set Content-Security-Policy "default-src 'self'; font-src *;img-src * data:; script-src *; style-src *;"
```
* تغییرات را ذخیره و سپس سرویس آپاچی را برای اعمال تغییرات ریستارت کنید.
