* برای فعال کردن هدر X-XSS-Protection در وب سرور Nginx ، خط زیر را در فایل پیکربندی خود اضافه کنید، پس از اتمام، تغییرات خود را ذخیره کرده و Nginx را مجدداً بارگذاری کنید.

```config
    add_header X-XSS-Protection "1; mode=block";
```
* فایل کانفیگ NGINX به صورت زیر است
```config
    upstream portal {
        server localhost:8080;
    }server {    
    listen 80;
        server_name portal.test;
        add_header X-XSS-Protection "1; mode=block";    location / {
            proxy_pass http://portal;
        }
    }
```
