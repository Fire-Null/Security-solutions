* برای غیرفعال کردن متدهای ناامن، ابتدا گزینه allowUnlisted="false” را تنظیم کنید که هیچ متدی مجاز نباشد. در مرحله بعد، متدهایی را که می خواهید به صراحت اجازه دهید، فهرست کنید( در این مورد، (GET.

```config
    <configuration>
    <system.webServer>
    <security>
    <requestFiltering>
        <verbs
        allowUnlisted="false"
                    >
        <add verb="GET" allowed="true" />
        </verbs>
    </requestFiltering>
    </security>
    </system.webServer>
    </configuration>
```
