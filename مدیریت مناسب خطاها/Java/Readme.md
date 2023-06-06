### رای این‌گونه از برنامه­های کاربردی می­توان یک global handler در web.xml تنظیم کرد. در اینجا نمونه­ای از تنظیمات web.xml پیشنهاد خواهد شد.  با این تنظیمات در صورت بروز هرگونه خطای تولیدشده‌ی غیرمنتظره، کاربر به صفحه­ی error.jsp منتقل خواهد شد. این صفحه می­تواند شامل پیام کلی و فاقد جزئیات مانند "خطایی رخ داده است!" باشد.

* تنظیمات web.xml :
```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://java.sun.com/xml/ns/javaee" xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd" version="3.0">
...
    <error-page>
        <exception-type>java.lang.Exception</exception-type>
        <location>/error.jsp</location>
    </error-page>
...
</web-app>
```
* محتویات error.jsp :
```jsp
<%@ page language="java" isErrorPage="true" contentType="application/json; charset=UTF-8" pageEncoding="UTF-8"%>
<%
String errorMessage = exception.getMessage();
//Log the exception via the content of the implicit variable named "exception"
//...
//We build a generic response with a JSON format because we are in a REST API app context
//We also add an HTTP response header to indicate to the client app that the response is an error
response.setHeader("X-ERROR", "true");
response.setStatus(200);
%>
{"message":"خطایی رخ داده است!"}
```
