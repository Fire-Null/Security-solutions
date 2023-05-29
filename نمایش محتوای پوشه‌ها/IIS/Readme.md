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

![](https://github.com/Fire-Null/Security-solutions/blob/main/%D9%86%D9%85%D8%A7%DB%8C%D8%B4%20%D9%85%D8%AD%D8%AA%D9%88%D8%A7%DB%8C%20%D9%BE%D9%88%D8%B4%D9%87%E2%80%8C%D9%87%D8%A7/IIS/image.png)
![](https://github.com/Fire-Null/Security-solutions/blob/main/%D9%86%D9%85%D8%A7%DB%8C%D8%B4%20%D9%85%D8%AD%D8%AA%D9%88%D8%A7%DB%8C%20%D9%BE%D9%88%D8%B4%D9%87%E2%80%8C%D9%87%D8%A7/IIS/image1.png)

