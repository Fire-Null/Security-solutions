* خط زیر را به بلاک ***server***  تان اضافه کنید، بعد از اتمام، تغییرات ذخیره شده و ***NGINX*** مجددا بارگذاری شود:

```config
    add_header Content-Security-Policy "default-src 'self';" always;
```
