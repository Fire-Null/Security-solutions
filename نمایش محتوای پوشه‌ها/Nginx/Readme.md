#### در ***Nginx، directory listing***  توسط ***ngx_http_index_module*** مدیریت می‌شود و می‌توانید با off کردن پارامتر ***autoindex*** ، ***directory listing*** را غیرفعال کنید.

```config
server {
   # ...

   location /var/www/myhost/public {
      autoindex off;
   }
}
