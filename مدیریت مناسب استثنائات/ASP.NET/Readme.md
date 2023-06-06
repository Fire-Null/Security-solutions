### مهاجم می‌تواند اطلاعات زیر را بدست می‌آورد:
1- نسخه ASP.NET

2- مسیر فیزیکی فایل فایلهای موقتی ASP.NET

3- اطلاعاتی مربوط به استثنائات ایجاد شده و احتمالا کد منبع ، کوئری sql
> این اطلاعات ممکن است به مهاجم کمک کند تا اطلاعات بیشتری کسب کرده و به طور بالقوه روی توسعه حملات بیشتر بر روی سیستم هدف متمرکز شود. برای جلوگیری از نشت اطلاعات با استفاده از صفحات خطای سفارشی، تغییرات زیر را بر روی web.config اعمال کنید:

```config 
<System.Web>
<customErrors mode=”On” defaultsRedirect=”~/error/GeneralError.aspx”>
       <error statusCode=”403” redirect=”~/error/Forbidden.aspx”>
       <error statusCode=”404” redirect=”~/erroe/PageNotFound.aspx”>
       <error statusCode=”500” redirect=”~/error/InternalError.aspx”>
</System.Web>
```
