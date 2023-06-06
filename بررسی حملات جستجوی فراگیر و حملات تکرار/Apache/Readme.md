
### کاربران  Apache نیز می توانند از طریق فایل پیکربندیApache  خود با کمی تغییر نسبت به  Nginx از قابلیت های محدودسازی بهره‌مند شوند. در آپاچی برای محدود سازی پهنای باند کلاینت باید از ماژول  mod_ratelimit  استفاده کرد.

> علاوه بر این، بجای متراکم سازی در سطح IP کلاینت،  از Throttling برای هر پاسخ HTTP  استفاده می شود.

```
<Location "/promotion">
    SetOutputFilter RATE_LIMIT
    SetEnv rate-limit 400
    SetEnv rate-initial-burst 512
</Location>
```
> مقدارهای اسنیپت بالا بر حسب  KiB/s تعریف شده اند؛ بنابراین متغیر محیطی rate limit، برای مشخص کردن سرعت اتصال KiB/s 400  است در حالی که میزان داده های اولیه burst،  KiB/s 512 است
