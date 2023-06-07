* برای فعالسازی فلگ HttpOnly در IIS، فایل web.config را باز کنید و تنظیمات زیر را اضافه کنید:
```config
<system.web> 
... 
<httpCookies httpOnlyCookies="true" requireSSL="true" /> 
... 
</system.web>
```
* برای فعالسازی فلگ secure پیشنهاد می‌شود از URL Rewrite استفاده شود و خطوط زیر را به فایل web.config اضافه کنید.

```config
<system.webServer> 
<rewrite> 
<outboundRules> 
<rule name="Use only secure cookies" preCondition="Unsecured cookie"> 
<match serverVariable="RESPONSE_SET_COOKIE" pattern=".*" negate="false" /> 
<action type="Rewrite" value="{R:0}; secure" /> 
</rule> 
<preConditions> 
<preCondition name="Unsecured cookie"> 
<add input="{RESPONSE_SET_COOKIE}" pattern="." /> 
<add input="{RESPONSE_SET_COOKIE}" pattern="; secure" negate="true" /> 
</preCondition> 
</preConditions> 
</outboundRules> 
</rewrite> 
... 
</system.webServer>
```

