#### برشماری یا حدس حساب کاربری زمانی اتفاق می‌افتد که مهاجم تلاش می‌کند با استفاده از حملات Brute-force ، حساب کاربری معتبر در سامانه را حدس بزند. این مورد در صفحه ورود، فراموشی رمز عبور، ثبت‌نام و... اتفاق می‌افتد.
در این روش مهاجم به دنبال بررسی کردن تفاوت پاسخی است که سرور در مقابل درخواست او می‌دهد. زمانی که مهاجم نام‌کاربری و رمز ورود نامعتبری را وارد می‌کند، سرور پاسخی را ارسال می‌کند و می‌گوید که کاربر مربوطه وجود ندارد.( The user does not exist)مهاجم متوجه می‌شود که مشکل رمز عبور نیست، بلکه این نام کاربری است که در سامانه وجود ندارد.
از طرف دیگر اگر مهاجم یک نام کاربری معتبر را با یک رمز عبور نامعتبر وارد کند، سرور پاسخ دیگری را نشان می‌دهد و می‌گوید رمزعبور وارد شده برای نام کاربری مربوطه صحیح نیست(The password is incorect)، که این مشخص می‌کند که نام کاربری مورد تایید سرور است. پس مهاجم متوجه می‎‌شود که سرور چگونه به ورودی معتبر و نامعتبر پاسخ می‌دهد و می‌تواند نام‌های کاربری معتبر را به دست آورد.
یک روش موثر برای جلوگیری از این مشکل این است که سرور یک پاسخ ثابت را برای هر دو حالت داشته باشد به این شکل که “نام کاربری یا رمز ورود نادرست است(The username and/or password are incorrect)”.در این صورت نفوذگر نمی‌تواند استدلال کند که نام کاربری نادرست بوده یا خیر.
صفحه فراموشی رمز نیز می‌تواند در برابر این نوع حمله آسیب‌پذیر باشد.به طور معمول، هنگامی که یک کاربر رمز عبور خود را فراموش می‌کند، یک نام کاربری را در این قسمت وارد می کند و سیستم تنظیم مجدد رمز ورود، یک ایمیل برای ایجاد پسورد جدید ارسال می‌کند.
در این حالت یک سامانه آسیب‌پذیر مشخص می‌کند که آن نام کاربری در سیستم وجود دارد یا خیر.(The username does not exist)
برای رفع این مشکل نیز باید پاسخ ثابتی در سرور مشخص شود که به سادگی به کاربر بگوید که اگر نام کاربری معتبر باشد، سیستم یک ایمیل بازگردانی به آدرس وارد شده ارسال می‌کند.
عدم مدیریت خطا در احراز هویت به‌راحتی به مهاجم اجازه­ی برشماری کاربران یک سامانه را می­دهد.


* در اعلام بروز خطا در فرآیند احراز هویت، هرگز اطلاعاتی در مورد نوع و علت خطای رخ‌داده به کاربر نمایش ندهید. در اغلب موارد نمایش یک جمله­­ی کلی مانند "خطایی رخ‌داده است" کفایت می­کند.
* به‌عنوان‌مثال در قسمت ورود به سامانه اگر نام کاربری درست واردشده اما گذرواژه اشتباه وارد شده است، نباید این موضوع با جزئیات به کاربر اعلام شود و در خطای نمایش داده شده باید از عباراتی مانند "نام کاربری یا گذرواژه اشتباه وارد شده است" استفاده شود. همچنین در بروز خطاهای مختلف سعی کنید تا از یک عبارت ثابت در نمایش خطا استفاده کنید، این موضوع مانع از حدس زدن نوع خطای رخ داده توسط نفوذگر می­شود.

> مثال­هایی از مدیریت خطای نامناسب:
    * گذرواژه اشتباه است
    * نام کاربری اشتباه است
    * حساب کاربری غیرفعال شده است
>مثال مدیریت مناسب خطا:
    * نام کاربری یا گذرواژه اشتباه وارد شده است
    * در مکانیزم احراز هویت، پس از ارسال درخواست ورود به سامانه، چه در صورتی که کاربر مورد نظر موجود نبوده و چه در صورتی که گذرواژه به اشتباه وارد شده باشد، سامانه بایستی یک خطای ساده حاکی از بروز خطا در احراز هویت نمایش دهد و تفاوتی بین دو حالت مذکور از دید کاربر مشهود نباشد.
    * اطمینان حاصل کنید که اپلیکیشن در پاسخ به نام اکانت ، پسورد  یا سایر اعتبارهای کاربر، پیامهای خطای عمومی برمیگرداند. 


