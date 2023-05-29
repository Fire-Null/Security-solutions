* برای این کار کافیست کد زیر را پس از تگ <system.webServer> در فایل web.config اضافه کنید:
```config
    <system.webServer>
        <httpProtocol>
            <customHeaders>
                <add name="X-Frame-Options" value="sameorigin" />
            </customHeaders>
        </httpProtocol>
    </system.webServer>
```
