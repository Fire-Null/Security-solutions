* برای فعال‌سازی هدر ***X-XSS-Protection*** ، تنظیمات زیر را به فایل ***web.config*** اضافه کنید:
```config
    <system.webServer>
        ...

        <httpProtocol>
            <customHeaders>
                <add name="X-XSS-Protection" value="1; mode=block" />
            </customHeaders>
        </httpProtocol>

        ...
    </system.webServer>
```
