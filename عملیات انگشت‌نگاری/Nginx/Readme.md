* درصورت عدم استفاده از ماژول­های ***nginx*** می­توان برای حذف نسخه ***nginx*** و نام سیستم عامل از سرایند ***server***
 از تنظیمات زیر در ***nginx*** استفاده نمایید:

```config
http {
server_tokens off;
}
```
* در صورت استفاده از ***nginx-exteras*** از تنظیمات زیر در ***nginx.conf*** استفاده کنید:
```config
http {
    # Basic Settings
    more_set_headers 'Server: ';
```

### ngx_security_headers
* می­توان با استفاده  ماژول ***ng_security_headers*** با اضافه کردن تنظیمات زیر در ***nginx.conf*** می­توان هدر ***server*** را حذف نمود:
```config
load_module modules/ngx_http_security_headers_module.so;

http {
    ...
    security_headers on;
    ...
}
```
### nginx-module-headers-more
* می­توان با استفاده  ماژول ***nginx-module-headers-more*** با اضافه کردن تنظیمات زیر در ***nginx.conf*** می­توان هدر ***server*** را حذف نمود:
```config
load_module modules/ngx_http_headers_more_filter_module.so;

http {
    ...
    more_clear_headers Server;
    ...
}
```
### modesecurity
* در صورت استفاده از ***modesecurity***  از تنظیمات زیر در ***modsecurity.conf*** استفاده کنید(به‌جای مقدار ***server*** مقدار دلخواه خود را که می­خواهید در ***header***نمایش  داده شود را قرار دهید):
```config
SecServerSignature server
```
