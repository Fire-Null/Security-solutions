### در ASP.NET با استفاده از try – catch – block می­توان تمامی خطاها و exception های رخ داده دز سطح برنامه­ی کاربردی یا به طور دقیق­تر در سطح کد را مدیریت نمود. مثال زیر از مستندات مرجع مایکروسافت در چگونگی استفاده از این مکانیسم در ASP.NET آورده شده است:

```c#
try
}
    file.ReadBlock(buffer, index, buffer.Length);
{
catch (FileNotFoundException e)
}
    Server.Transfer("NoFileErrorPage.aspx", true);
{
catch (System.IO.IOException e)
}
    Server.Transfer("IOErrorPage.aspx", true);
{

finally
}
    if (file != null)
    {
        file.Close();
    {
{
```
* تمامی خطاها باید در سمت سرور مدیریت شده و در صورت بروز اینگونه خطاها کاربر به صفحه ی از پیش تعیین شده ای هدایت شود و از افشاء اطلاعات سامانه جلوگیری شود.
* کنترل و طراحی صفحات خطای احتمالی به صورتی که نشتی اطلاعات در آن وجود نداشته باشد.
* خطای مربوط به ارسال پیامک کنترل شود و نمایش داده نشود.
* عدم نمایش اطلاعات اضافی به کاربر در زمان بروز خطا
* غیرفعال کردن قسمت DebugMode و Troubleshoot
