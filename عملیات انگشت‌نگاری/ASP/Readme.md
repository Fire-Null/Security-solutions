
### در صورت استفاده از ماژول URL Rewrite از تنظیمات زیر در web.config استفاده کنید:

```config
    <system.webServer>
        <rewrite>
            <rules>
                <rule name="RewriteASPX">
                    <match url="(.*)" />
                    <conditions logicalGrouping="MatchAll">
                        <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="true" />
                        <add input="{REQUEST_FILENAME}" matchType="IsDirectory" negate="true" />
                    </conditions>
                    <action type="Rewrite" url="{R:1}.aspx" />
                </rule>
            </rules>
        </rewrite>
    </system.webServer>
```
* در صورت عدم استفاده از ماژول URL Rewrite می­توان در global.ascx کد زیر را قرار داد:

```aspx
    void Application_BeginRequest(object sender, EventArgs e)
    {
    String fullOrigionalpath = Request.Url.ToString();
    String[] sElements = fullOrigionalpath.Split('/');
    String[] sFilePath = sElements[sElements.Length - 1].Split('.');

    if (!fullOrigionalpath.Contains(".aspx") && sFilePath.Length == 1)
    {
        if (!string.IsNullOrEmpty(sFilePath[0].Trim()))
                   Context.RewritePath(sFilePath[0] + ".aspx");
   }
}
```
