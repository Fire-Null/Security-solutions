* برای فعالسازی هدر ***X-XSS-Protection*** در آپاچی، خط زیر را به فایل پیکربندی پیش‌فرض اضافه کنید(/etc/apache2/sites-enabled/example.conf):

```config
    Header set X-XSS-Protection "1; mode=block"
```
