* خط زیر را به بلوک سرور اضافه کنید، پس از اتمام، تغییرات خود را ذخیره کنید و Nginx را مجددا بارگذاری کنید.
```bash 
    add_header Strict-Transport-Security "max-age=31536000; includeSubDomains"
```

* فایل پیکربندی Nginx باید به صورت زیر قفل شود.
```config
    upstream portal {
        server localhost:8080;
    }server {
    listen 80;
    server_name portal.test;
    add_header Strict-Transport-Security "max-age=31536000";   location / {
            proxy_pass http://portal;
        }
    }
```
