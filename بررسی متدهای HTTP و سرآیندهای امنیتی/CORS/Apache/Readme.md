* برای افزودن مجوز CORS به هدر در Apache (یا Apache2)، خطوط زیر را در پیکربندی سرور خود (که معمولاً در فایل /etc/apache2/apache2.conf یا در فایل htaccess. قرار دارد اضافه کنید:

```config
    <Directory /var/www/my-callback-url-path>
        Order Allow,Deny
        Allow from all
        AllowOverride all
        Header add Access-Control-Allow-Headers "origin, x-requested-with, content-type, authorization"
        Header add Access-Control-Allow-Methods "GET, POST, OPTIONS"
        Header set Access-Control-Allow-Origin "https://stagegateway.eko.in"
    </Directory>
```

* بعد از اعمال تغییرات، با اجرای دستور apachectl -t بررسی کنید که آیا تغییرات صحیح است یا نه،  و آپاچی را مجدد بارگذاری نمایید (sudo service apache2 reload)
