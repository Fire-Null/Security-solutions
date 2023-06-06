### مدیریت خطا را در آپاچی می­توان با دستور ErrorDocument در فایل .htaccess به صورت زیر  پیاده سازی نمود
```url
ErrorDocument 500 "Sorry, our script crashed. Oh dear"
ErrorDocument 500 /cgi-bin/crash-recover
ErrorDocument 500 http://error.example.com/server_error.html
ErrorDocument 404 /errors/not_found.html
ErrorDocument 401 /subscription/how_to_subscribe.html

# Directives for custom error pages
ErrorDocument 400 400.html
ErrorDocument 403 403.html
ErrorDocument 404 404.html
ErrorDocument 500 500.html
```
* در صورتی که از  VirtualHost استفاده می‌کنید، دستور ErrorDocument را در تگ VirtualHost قرار دهید:

```config
<VirtualHost>
   ...
   ErrorDocument 404 /error404.html
   ...
</VirtualHost>
```
>سینتکس استفاده از این دستور به شکل زیر است:
```config
ErrorDocument <3-digit-code> <action>
```
