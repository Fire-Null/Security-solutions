* برای فعال کردن هدر CORS در وب سرور Nginx ، خط زیر را در فایل پیکربندی خود اضافه کنید، پس از اتمام، تغییرات را ذخیره کرده و Nginx را مجددا بارگذاری ک

```config
    add_header 'Access-Control-Allow-Origin' 'https://foo.example' always;
    add_header 'Access-Control-Allow-Methods' 'GET, POST, OPTIONS' always;
    add_header 'Access-Control-Allow-Headers' 'DNT,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type,Range' always;
```
* کانفیگ nginx به صورت زیر است:
```config

    upstream portal {
        server localhost:9004;
    }server {
        listen 80;
    server_name portal.test;
    add_header 'Access-Control-Allow-Origin' 'https://foo.example' always;
    add_header 'Access-Control-Allow-Methods' 'GET, POST, OPTIONS' always;
    add_header 'Access-Control-Allow-Headers' 'DNT,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type,Range' always;location / {
            proxy_pass http://portal;
        }
    }

```

* فایل پیکربندی زیر cors را فعال میکند

```config 
    location /my-callback-url-path {
        if ($request_method = 'OPTIONS') {
            add_header 'Access-Control-Allow-Origin' 'https://stagegateway.eko.in';
            add_header 'Access-Control-Allow-Methods' 'POST, OPTIONS';
            add_header 'Access-Control-Allow-Headers' 'X-Requested-With,Content-Type,Authorization';
            add_header 'Access-Control-Max-Age' 1728000;
            add_header 'Content-Type' 'text/plain; charset=utf-8';
            add_header 'Content-Length' 0;
            return 204;
        }
        if ($request_method = 'POST') {
            add_header 'Access-Control-Allow-Origin' 'https://stagegateway.eko.in';
            add_header 'Access-Control-Allow-Methods' 'GET, POST, OPTIONS';
            add_header 'Access-Control-Allow-Headers' 'X-Requested-With,Content-Type,Authorization';
            add_header 'Access-Control-Expose-Headers' 'Content-Length,Content-Range';
        }
    }

```
