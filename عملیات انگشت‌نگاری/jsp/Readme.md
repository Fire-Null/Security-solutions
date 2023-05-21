
###  به‌عنوان مثال اگر صفحه­ی سامانه home.jsp نام داشته باشد، اعمال تنظیمات زیر در web.xml پسوند jsp را حذف خواهد نمود:

```xml
    <servlet>
        <servlet-name>home</servlet-name>
        <jsp-file>/home.jsp</jsp-file>
    </servlet>
    <servlet-mapping>
        <servlet-name>login</servlet-name>
        <url-pattern>/login</url-pattern>
    </servlet-mapping>
```
