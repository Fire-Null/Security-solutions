* برای فعالسازی هدر ***X-Content-Type-Options*** در iis، کد زیر را به ***web.config*** اضافه کنید

```config
    <configuration>
        <system.webServer>
            <httpProtocol>
                <customHeaders>
                <add name="X-Content-Type-Options" value="nosniff" />
                    
                </customHeaders>
            </httpProtocol>
        </system.webServer>
    </configuration>
```
