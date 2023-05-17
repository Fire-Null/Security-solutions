#### برای پنهان کردن اطلاعات نسخه apache، فایل پیکربندی که در مسیر ***"/etc/httpd/conf/httpd.conf"*** یا ***"/etc/apache2/conf-enabled/security.conf"*** یافت می‌شود تغییر دهید:


1. فایل پیکربندی ***apache*** را باز کنید:                                          
  
```bash
    sudo nano /etc/httpd/conf/httpd.conf    ## Redhat systems
```
  ![](https://github.com/Fire-Null/Security-solutions/blob/main/%D8%B9%D9%85%D9%84%DB%8C%D8%A7%D8%AA%20%D8%A7%D9%86%DA%AF%D8%B4%D8%AA%E2%80%8C%D9%86%DA%AF%D8%A7%D8%B1%DB%8C/Apache/red-path.png)
```bash
  sudo nano /etc/apache2/conf-enabled/security.conf  ## Debian systems
```
  ![](https://github.com/Fire-Null/Security-solutions/blob/main/%D8%B9%D9%85%D9%84%DB%8C%D8%A7%D8%AA%20%D8%A7%D9%86%DA%AF%D8%B4%D8%AA%E2%80%8C%D9%86%DA%AF%D8%A7%D8%B1%DB%8C/Apache/deb-path.png)

2. دستورالعمل‌های ***"ServerTokens"*** و ***"ServerSignature"*** را پیدا کنید، اگر وجود ندارد به فایل اضافه کنید و به صورت زیر آپدیت کنید:

```bahs 
    ServerTokens Prod
    ServerSignature Off
```
  ![](https://github.com/Fire-Null/Security-solutions/blob/main/%D8%B9%D9%85%D9%84%DB%8C%D8%A7%D8%AA%20%D8%A7%D9%86%DA%AF%D8%B4%D8%AA%E2%80%8C%D9%86%DA%AF%D8%A7%D8%B1%DB%8C/Apache/edit.png)
> دستورالعمل "ServerTokens Prod" به Apache می گوید که فقط کلمه "Apache" را بدون هیچ گونه اطلاعات نسخه نمایش دهد. دستورالعمل "ServerSignature Off" امضای سرور را در صفحات خطا غیرفعال می کند.

3. پس از ذخیره و اصلاح فایل پیکربندی، Apache را مجددا ریستارت کنید تا تغییرات اعمال شوند

```bash
    sudo systemctl restart httpd    ## Redhat systems
    sudo systemctl restart apache2     ## Debian systems 
```
