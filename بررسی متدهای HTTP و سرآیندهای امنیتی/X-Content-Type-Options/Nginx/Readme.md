* برای فعال کردن هدر ***X-Content-Type-Options*** در وب سرور ***Nginx*** ، خط زیر را در فایل پیکربندی خود اضافه کنید، پس از اتمام، تغییرات خود را ذخیره کرده و ***Nginx*** را مجدداً بارگذاری کنید. 
```config
    add_header X-Content-Type-Options "nosniff"
```
* کانفیگ NGINX به صورت زیر است:
```config
    upstream portal {
        server localhost:9004;
    }server {
    listen 80;
    server_name portal.test;
    add_header X-Content-Type-Options "nosniff"   location / {
            proxy_pass http://portal;
        }
    }
```
