* برای فعال کردن هدر X-Frame-Options در وب سرور Nginx خود، خط زیر را در فایل پیکربندی خود اضافه کنید، پس از پایان کار، تغییرات خود را ذخیره کرده و Nginx را مجدداً بارگذاری کنید.

```config
    add_header X-Frame-Options "DENY";
```
* کانفیگ NGINX به صورت زیر است
```config
    upstream portal {
        server localhost:9004;
    }server {   
    listen 80;
    server_name portal.test;
    add_header X-Frame-Options "DENY";   location / {
            proxy_pass http://portal;
        }
    }
```
