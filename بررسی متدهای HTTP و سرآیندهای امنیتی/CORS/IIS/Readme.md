* تنظیمات زیر را به فایل web.config خود اضافه کنید
* ```config
*   <system.webServer>
      <httpProtocol>
          <customHeaders>
              <add name="Access-Control-Allow-Origin" value="*" />
              <add name="Access-Control-Allow-Methods" value="GET,POST,OPTIONS" />
              <add name="Access-Control-Allow-Headers" value="Content-Type, soapaction" />
          </customHeaders>
      </httpProtocol>
  </system.webServer>
 ```
