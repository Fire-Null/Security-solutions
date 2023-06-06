#### غیرفعال کردن پروتکل ضعیف ssl/tls در apache
* فایل ssl.conf را باز کنید این فایل معمولا در مسیر etc/httpd/conf.d/ قرار دارد.
* دنبال بخش SSL Protocol Support بگردید
```config
#   SSL Protocol support:# List the enable protocol levels with which clients will be able to# connect.  Disable SSLv2 access by default:SSLProtocol all -SSLv2 -SSLv3
```
* خط SSLProtocol all -SSLv2 -SSLv3 را با اضافه کردن # در ابتدای آن کامنت کنید.
* خط زیر را اضافه کنید
```config
SSLProtocol all -SSLv2 -SSLv3 -TLSv1 -TLSv1.1
```
* با دستور فوق SSL v2 و SSL v3 و TLS v1.0 و TLS v1.1 غیر فعال شده اند در ادامه به قسمت SSL Cipher Suite بروید 
```config 
#   SSL Cipher Suite:# List the ciphers that the client is permitted to negotiate.# See the mod_ssl documentation for a complete list.SSLCipherSuite HIGH:MEDIUM:!aNULL:!MD5:!SEED:!IDEA
```
* خط SSLCipherSuite HIGH:MEDIUM:!aNULL:!MD5:!SEED:!IDEA را کامنت و خط زیر را اضافه کنید
```config
SSLCipherSuite HIGH:!aNULL:!MD5:!3DES
```
* این گزینه به ما اطمینان می دهد که رمزنگاری SSL فقط با سطح حفاظت بالا انجام شود . همچنین در زیر  SSLCipherSuite HIGH:!aNULL:!MD5:!3DES خط زیر را نیز اضافه کنید
```config
SSLHonorCipherOrder on
```
* این پارامتر به ما اطمینان می دهد که از پارامترهای cipher سمت سرور استفاده شود و نه از پارامترهای سمت کلاینت.
* فایل را ذخیره کنید و آپاچی را ریستارت کنید.
* service httpd restart
