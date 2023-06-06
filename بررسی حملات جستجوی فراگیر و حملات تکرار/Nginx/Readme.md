
### اگر از Nginx به عنوان وب سرور استفاده می کنید و می خواهید محدود سازی نرخ بر اساس سرور را پیاده کنید، می توانید از ماژول   ngx_http_limit_req_module بهره گیرید. این کار را می توانید مستقیما از طریق فایل پیکربندی Nginx  تان انجام دهید.
> قبل از پیکربندی Nginx، باید url ورود به سیستم خود را بدانید. بسته به برنامه کاربردی که استفاده می کنید، دسترسی به ورود به صورت زیر باشد:

```
    /api/login for an API
    /wp-login for Wordpress
    /admin/login for a backend access
    /user/login for a frontend access
```

#### در تنظیمات زیر، بخش ورود با حداکثر 1 درخواست در 1 ثانیه برای هر کلاینت تنظیم شده است که آدرس بخش ورود را مشخص کرده(/admin/login) و rate limit بر روی آن ایجاد می‌کند 

```config
    limit_req_zone $binary_remote_addr zone=login:10m rate=1r/s;

    server {   
        server_name example.com;
        root /var/www/html/;

        #limit connection per ip
        limit_conn perip 10;

        #protect /admin/login
        location ~/admin/login {
            limit_req zone=login; #use login limit_req_zone
            limit_req_status 444; #return 444 when limiting
        }

        location / {
            #other none rate limited requests    
        }
    }
```
