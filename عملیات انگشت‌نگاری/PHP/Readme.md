#### برای مخفی کردن اطلاعات نسخه PHP، باید فایل پیکربندی PHP را که معمولاً php.ini نامیده می شود، تغییر دهید که بسته به سیستم شما در مکان های مختلف یافت می شود.


1- فایل php.ini را باز کنید:
```bash
    sudo nano /etc/php/7.4/apache2/php.ini 
```
    ![](https://github.com/Fire-Null/Security-solutions/blob/main/%D8%B9%D9%85%D9%84%DB%8C%D8%A7%D8%AA%20%D8%A7%D9%86%DA%AF%D8%B4%D8%AA%E2%80%8C%D9%86%DA%AF%D8%A7%D8%B1%DB%8C/PHP/image.png)
 *  نسخه “7.4” را با نسخه PHP خود جایگزین کنید
 
 2- دستورالعمل "expose_php" را پیدا کنید. اگر وجود ندارد، آن را به فایل اضافه کنید. این دستورالعمل را به صورت زیر به روز کنید:
 ```bash
    expose_php = Off
```

3- این تنظیم، نمایش نسخه PHP را در پاسخ HTTP غیرفعال می‌کند.
    3. پس از ویرایش  و ذخیره  فایل php.ini، سرویس Apache را مجددا راه اندازی کنید تا تغییرات اعمال شوند:

```bash
    sudo systemctl restart httpd     
    sudo systemctl restart apache2 
```
