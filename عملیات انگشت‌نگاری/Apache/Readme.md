### برای پنهان کردن اطلاعات نسخه apache، فایل پیکربندی که در مسیر ***"/etc/httpd/conf/httpd.conf"*** یا ***"/etc/apache2/conf-enabled/security.conf"*** یافت می‌شود تغییر دهید:

1. فایل پیکربندی apache را باز کنید:

    `sudo nano /etc/httpd/conf/httpd.conf    ## Redhat systems
sudo nano /etc/apache2/conf-enabled/security.conf  ## Debian systems   `
2. دستورالعمل‌های ***"ServerTokens"*** و ***"ServerSignature"*** را پیدا کنید، اگر وجود ندارد به فایل اضافه کنید و به صورت زیر آپدیت کنید:
`ServerTokens Prod `

     `ServerSignature Off`

    #### دستورالعمل ***"ServerTokens Prod"*** به ***Apache*** می گوید که فقط کلمه ***"Apache"*** را بدون هیچ گونه اطلاعات نسخه نمایش دهد. دستورالعمل ***"ServerSignature Off"*** امضای سرور را در صفحات خطا غیرفعال می کند.

3. پس از ذخیره و اصلاح فایل پیکربندی، ***Apache*** را مجددا ریستارت کنید تا تغییرات اعمال شوند:
`sudo systemctl restart httpd    ## Redhat systems`

    `sudo systemctl restart apache2     ## Debian systems `
