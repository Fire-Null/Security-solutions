* هدر Strict-Transport-Security را به فایل web.config اضافه کنید.
```config
    <system.webServer>
    <httpProtocol>
        <customHeaders>
        <add name="Strict-Transport-Security" value="max-age=31536000"/>
        </customHeaders>
    </httpProtocol>
    </system.webServer>
```
*  ریستارت کنید IIS را.
