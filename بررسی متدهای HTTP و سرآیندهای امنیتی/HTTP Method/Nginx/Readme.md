#### متدهای امن مورداستفاده در سامانه متدهای GET، HEAD و POST می‌باشد. متدهای دیگر مانند TRACE، DELETE، PATCH و... ناامن هستند. تنظیم زیر اجازه استفاده از متدهای GET،POST و HEAD را می‌دهد و دیگر متدهای را exclude می‌کند.

* فایل nginx.conf را تغییر داده و تنظیمات زیر را اضافه کنید

```config

add_header Allow "GET, POST, HEAD" always;
if ( $request_method !~ ^(GET|POST|HEAD)$ ) {
return 405; 
}

```
