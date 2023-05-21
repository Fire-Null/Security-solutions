
### حذف هدر X-Powered-By 
* برای حذف ***ASP.NET*** از هدر ***X-Powered-By*** در ***IIS*** ،  تنظیمات زیر را در ***web.config*** (در نود ***system.webServer*** قرار دارد) اعمال کنید:

```asp
    <httpProtocol>
    <customHeaders>
        <remove name="X-Powered-By" />
    </customHeaders>
    </httpProtocol>
```
### حذف هدر X-AspNet-Version
* هدر ***X-AspNet-Version*** نشان می‌دهد از چه نسخه‌ای از ***ASP.NET*** استفاده می‌شود. تنظیمات زیر را داخل نود ***<system.web>***  در فایل ***web.config*** اضافه کنید:

```asp
    <httpRuntime
    enableVersionHeader="false" />
```
