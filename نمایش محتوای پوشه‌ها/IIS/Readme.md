#### 2 روش وجود دارد که با استفاده از آنها می توانید directory listing را در IIS غیرفعال کنید: (این روشها برای IIS 10  پیشنهاد می‌شود)
* روش وجود دارد که با استفاده از آنها می توانید directory listing را در IIS غیرفعال کنید: (این روشها برای IIS 10  پیشنهاد می‌شود)

```config
  <configuration>
     <system.webServer>
         <directoryBrowse enabled="false" /> <!--this line will disable directory browsing-->
     </system.webServer>
  </configuration>
 ```
 * به IIS Manager  رفته و به دنبال گزینه Directory Browser بگردید. آن را انتخاب کنید و در گوشه سمت راست گزینه Open Feature را کلیک کنید و به تب دیگری هدایت خواهید شد.سپس Disable را انتخاب کنید.
