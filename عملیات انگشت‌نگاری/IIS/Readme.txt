#### رایج ترین روش جهت تغییر هدر ***Server***  در ***IIS*** استفاده از ***URL Rewrite***  است که در سطح برنامه کاربردی اعمال می­شود. جهت تغییر هدر ***Server*** کافی است در  ***web.config*** تنظیمات زیر را وارد نمایید و در قسمت ***value***، مقداری که می­خواهید در هدر مربوط به ***server*** نمایش داده شود را قرار دهید

```config
<rewrite>    
  <outboundRules rewriteBeforeCache="true">
    <rule name="Remove Server header">
          <match serverVariable="RESPONSE_Server" pattern=".+" />
      <action type="Rewrite" value="" />
    </rule>
  </outboundRules>
</rewrite>
```
* یا در ***IIS 10*** یک ویژگی جدید اضافه شده است که امکان حذف هدر ***Server*** را فراهم می کند، باید موارد زیر را به فایل ***web.config*** اضافه کنید:

```config 
<system.webServer>
<!-- Removed the Server header -->
<security>
<requestFiltering removeServerHeader="true" />
</security>
<system.webServer/>
```
