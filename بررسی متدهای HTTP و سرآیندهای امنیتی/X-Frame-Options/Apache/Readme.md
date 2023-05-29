* برای فعال کردن این هدر در آپاچی کافی است خط زیر را به فایل پیکربندی آپاچی(/etc/apache2/sites-enabled/example.conf) اضافه کنید.
```config
    header always set X-Frame-Options "sameorigin"
```
* سپس سرویس آپاچی را برای اعمال تغییرات ریستارت کنید

