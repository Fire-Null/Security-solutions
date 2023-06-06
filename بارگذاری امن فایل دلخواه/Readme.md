
#### راهکار زیر را در خصوص بارگذاری فایل رعایت کنید:
* مطمئن شوید که امکان بارگذاری فایل به دایرکتوری­های پیش‌بینی‌نشده و حساس وجود ندارد.
* حداکثر حجم فایل بارگذاری شده تنظیم شود تا مهاجم با بارگذاری فایلهای بزرگ، سامانه را با مشکل کمبود فضا و حمله منع خدمت مواجه نکند.
* دسترسی اجرا را در دایرکتوری­ای که فایل­ها در آن بارگذاری می­شود حتماً غیرفعال کنید.
* حتماً در سمت سرور extension فایل بارگذاری شده را قبل از قرار دادن آن در دایرکتوری مربوطه چک کنید.
* اگر قرار است تنها فایل عکس بارگذاری شود، در سمت سرور با استفاده از یک کتابخانه­ امن عکس را de-compress کنید تا مطمئن شوید فایل عکس است.
* فایل­های بارگذاری شده بایستی با content-type مشخص به کاربر نمایش داده شوند.
* از بارگذاری فایل­های اجرایی از نوع  php , asp , jsp , exe و همچنین HTML, CSS, JavaScript, XML, SVG جلوگیری کنید.
* از یک blacklist  برای بلاک کردن فایل­های مخرب استفاده کنید
* یک نمونه blacklist از پسوند فایل­های خطرناک:
```php
[
  # HTML may contain cookie-stealing JavaScript and web bugs
  'html', 'htm', 'js', 'jsb', 'mhtml', 'mht', 'xhtml', 'xht',
  # PHP scripts may execute arbitrary code on the server
  'php', 'phtml', 'php3', 'php4', 'php5', 'phps',
  # Other types that may be interpreted by some servers
  'shtml', 'jhtml', 'pl', 'py', 'cgi',
  # May contain harmful executables for Windows victims
  'exe', 'scr', 'dll', 'msi', 'vbs', 'bat', 'com', 'pif', 'cmd', 'vxd', 'cpl',
]
```
* حتماً پسوند فایل­ها را قبل از قرار دادن در سرور با یک whitelist از قبل تعیین‌شده و محدود، چک کنید.
* از overwrite شدن فایل­های اپلیکیشن توسط کاربر جلوگیری کنید.
