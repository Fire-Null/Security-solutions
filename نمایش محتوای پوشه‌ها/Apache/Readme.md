#### می‌توانید برای غیرفعال کردن کامل directory listing،   -Indexes را به دایرکتیو Options  در فایل پیکربندی آپاچی اضافه کنید، یا همان گزینه -Indexes را به پیکربندی Directory اضافه کنید تا این ویژگی در هر دایرکتوری غیرفعال شود.

* فایل پیکربندی آپاچی را باز کنید
```bash 
  $ sudo vi /etc/apache2/other/mysite.conf
 ```
 * Indexes  را به دستورالعمل Options دایرکتوری موردنظر اضافه کنید.

```config
  <Directory /var/www/mysite>
      Options -Indexes
  </Directory>
```
* برای اعمال تغییرات، آپاچی را ریستارت کنید.

#### می‌توان با استفاده از .htaccess ، نیز directory listing را غیرفعال کرد:
* فایل htaccess. را در دایرکتوری که می‌خواهید directory listing را غیرفعال کنید، باز کنید.

```bash
  $sudo vi /var/www/mysite/.htaccess
```
* -Indexes  را به دستورالعمل Options در فایل .htaccess اضافه کنید

```Options -Indexes```
