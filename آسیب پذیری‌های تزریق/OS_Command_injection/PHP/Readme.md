
### تکه کد زیر آدرس کاربر را دریافت و به دستور ping ‌می‌دهد.

```php
<html>
<head>
    <title>Command Injection</title>
</head>
<body>
<form action=&quot&quot method=&quotget&quot>
    Ping address: <input type=&quottext&quot name=&quotaddr&quot>
    <input type=&quotsubmit&quot>
</form>
</body>
</html>
<?php
#Excute Command
echo shell_exec(&quotping &quot.$_GET['addr']);
?>
```
>می‌توانیم در ورودی علاوه بر آدرس با استفاده از جداکننده‌هایی مانند ; و یا && دستورات دیگر مورد نظر خود را وارد و اجرا کنیم.

### در نمونه دیگر خروجی دستور به صورت مستقیم به کاربر نشان داده نمی‌شود.
```php
<html>
<head>
    <title>Command Injection</title>
</head>
<body>
<form action=&quot&quot method=&quotget&quot>
    Ping address: <input type=&quottext&quot name=&quotaddr&quot>
    <input type=&quotsubmit&quot>
</form>
</body>
</html>
<?php
#Excute Command
shell_exec(&quotping &quot.$_GET['addr']);
?>
```
>در این مورد می‌توانیم با استفاده از دستور های ایجاد کننده تاخیر مانند sleep آسیب‌پذیری را شناسایی کنیم.

### در زبان php می‌توانیم با استفاده از تابع escapeshellcmd از ورود دستورات دیگر جلوگیری می‌کنیم.
```php
<html>
<head>
    <title>Command Injection</title>
</head>
<body>
<form action=&quot&quot method=&quotget&quot>
    Ping address: <input type=&quottext&quot name=&quotaddr&quot>
    <input type=&quotsubmit&quot>
</form>
</body>
</html>
<?php
#Excute Command
echo shell_exec(escapeshellcmd(&quotping &quot.$_GET['addr']));
?>
```

> روش دیگر جلوگیری، تعریف نوع ورودی کاربر است. به این صورت که اگر مانند مثال بالا کاربر باید ip خود را وارد اپلیکیشن کند. ما باید نوع ورودی کاربر را بررسی و در صورت صحیح بودن آن را به تابع مورد نظر پاس دهیم.
```php
<?php
function isAllowed($cmd){
    // If the ip is matched, return true
    if(filter_var($cmd, FILTER_VALIDATE_IP)) {
        return true;
    }

    return false;
}
#Excute Command
if (isAllowed($_GET['addr'])) {
    echo shell_exec(&quotping &quot.$_GET['addr']);
}
?>
````
