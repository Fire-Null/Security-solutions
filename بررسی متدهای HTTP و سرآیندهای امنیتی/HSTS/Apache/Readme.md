
### برای فعال کردن HSTS در سرور آپاچی، مراحل زیر را دنبال کنید:
1- فایل <Apache>/conf/httpd.conf را باز کنید.
2- Header module را uncomment کنید
``` bash 
    LoadModule headers_module modules/mod_headers.so
```
3- تنظیمات هدر HSTS را به بخش VirtualHost اضافه کنید
```bash
    <VirtualHost www.example.com:80>
    Header always set Strict-Transport-Security "max-age=63072000; includeSubdomains; preload"
    </VirtualHost>
```
4- آپاچی را ریستارت کنید
