* برای تنظیم csp در iis، کد زیر را به فایل web.config اضافه کنید

```config
    <system.webServer>
    <httpProtocol>
        <customHeaders>
        <add name=”Content-Security-Policy” value=”default-src 'self'; img-src*” />
        </customHeaders>
    </httpProtocol>
    </system.webServer>
```
