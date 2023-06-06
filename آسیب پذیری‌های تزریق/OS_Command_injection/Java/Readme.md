>در تکه کد زیر ورودی کاربر به دسترسی کنترل نمی‌شود
```java
@Runtime@getRuntime().exec('rm -fr /your-important-dir/')
```
> و می‌توان از دستورات سیستم عامل استفاده کرد.

```java
package org.t246osslab.easybuggy.vulnerabilities;

import java.io.IOException;
import java.util.Locale;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import ognl.Ognl;
import ognl.OgnlContext;
import ognl.OgnlException;

import org.apache.commons.lang.StringUtils;
import org.apache.commons.lang.math.NumberUtils;
import org.t246osslab.easybuggy.core.servlets.AbstractServlet;

@SuppressWarnings(&quotserial&quot)
@WebServlet(urlPatterns = { &quot/ognleijc&quot })
public class OGNLExpressionInjectionServlet extends AbstractServlet {

    @Override
    protected void service(HttpServletRequest req, HttpServletResponse res) throws ServletException, IOException {

        Locale locale = req.getLocale();
        StringBuilder bodyHtml = new StringBuilder();
        Object value = null;
        String errMessage = &quot"
        OgnlContext ctx = new OgnlContext();
        String expression = req.getParameter(&quotexpression&quot);
        if (!StringUtils.isBlank(expression)) {
            try {
                Object expr = Ognl.parseexpression.replaceAll(&quotMath\\.&quot, &quot@Math@&quot));
                value = Ognl.getValue(expr, ctx);
            } catch (OgnlException e) {
                if (e.getReason() != null) {
                    errMessage = e.getReason().getMessage();
                }
                log.debug(&quotOgnlException occurs: &quot, e);
            } catch (Exception e) {
                log.debug(&quotException occurs: &quot, e);
            } catch (Error e) {
                log.debug(&quotError occurs: &quot, e);
            }
        }

        bodyHtml.append(&quot<form action=\&quotognleijc\&quot method=\&quotpost\&quot>&quot);
        bodyHtml.append(getMsg(&quotmsg.enter.math.expression&quot, locale));
        bodyHtml.append(&quot<br><br>&quot);
        if (expression == null) {
            bodyHtml.append(&quot<input type=\&quottext\&quot name=\&quotexpression\&quot size=\&quot80\&quot maxlength=\&quot300\&quot>&quot);
        } else {
            bodyHtml.append(&quot<input type=\&quottext\&quot name=\&quotexpression\&quot size=\&quot80\&quot maxlength=\&quot300\&quot value=\&quot&quot
                    + encodeForHTML(expression) + &quot\&quot>&quot);
        }
        bodyHtml.append(&quot = &quot);
        if (value != null && NumberUtils.isNumber(value.toString())) {
            bodyHtml.append(value);
        }
        bodyHtml.append(&quot<br><br>&quot);
        bodyHtml.append(&quot<input type=\&quotsubmit\&quot value=\&quot&quot + getMsg(&quotlabel.calculate&quot, locale) + &quot\&quot>&quot);
        bodyHtml.append(&quot<br><br>&quot);
        if (value == null && expression != null) {
            bodyHtml.append(getErrMsg(&quotmsg.invalid.expression&quot, new String[] { errMessage }, locale));
        }
        bodyHtml.append(getInfoMsg(&quotmsg.note.commandinjection&quot, locale));
        bodyHtml.append(&quot</form>&quot);

        responseToClient(req, res, getMsg(&quottitle.commandinjection.page&quot, locale), bodyHtml.toString());
    }
}
```

> در تکه کد زیر ورودی کاربر بدون هیچ کنترلی به run.exec پاس داده می‌شود.
```java
package org.joychou.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

import javax.servlet.http.HttpServletRequest;
import java.io.BufferedInputStream;
import java.io.BufferedReader;
import java.io.InputStreamReader;

/**
 * @author  JoyChou (joychou@joychou.org)
 * @date    2018.05.24
 * @desc    Java code execute
 * @fix     过滤造成命令执行的参数
 */

@Controller
@RequestMapping(&quot/rce&quot)
public class Rce {

    @RequestMapping(&quot/exec&quot)
    @ResponseBody
    public String CommandExec(HttpServletRequest request) {
        String cmd = request.getParameter(&quotcmd&quot).toString();
        Runtime run = Runtime.getRuntime();
        String lineStr = &quot"

        try {
            Process p = run.exec(cmd);
            BufferedInputStream in = new BufferedInputStream(p.getInputStream());
            BufferedReader inBr = new BufferedReader(new InputStreamReader(in));
            String tmpStr;

            while ((tmpStr = inBr.readLine()) != null) {
                lineStr += tmpStr + &quot\n"
                System.out.println(tmpStr);
            }

            if (p.waitFor() != 0) {
                if (p.exitValue() == 1)
                    return &quotcommand exec failed"
            }

            inBr.close();
            in.close();
        } catch (Exception e) {
            e.printStackTrace();
            return &quotExcept"
        }
        return lineStr;
    }
}
```
> می‌توان برای ورودی‌های کاربر whitelist تعریف کرد تا هر دستوری قابلیت اجرا نداشته باشد.

```java
package org.joychou.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

import javax.servlet.http.HttpServletRequest;
import java.io.BufferedInputStream;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.Arrays;

/**
 * @author  JoyChou (joychou@joychou.org)
 * @fix     RezaDuty 
 */

@Controller
@RequestMapping(&quot/rce&quot)
public class Rce {

    @RequestMapping(&quot/exec&quot)
    @ResponseBody
    public String CommandExec(HttpServletRequest request) {
    	
    	
    	String lineStr = &quot"
        String cmd = request.getParameter(&quotcmd&quot).toString();
        if(WhiteCommand(cmd)) {
	        Runtime run = Runtime.getRuntime();
	        
	
	        try {
	            Process p = run.exec(cmd);
	            BufferedInputStream in = new BufferedInputStream(p.getInputStream());
	            BufferedReader inBr = new BufferedReader(new InputStreamReader(in));
	            String tmpStr;
	
	            while ((tmpStr = inBr.readLine()) != null) {
	                lineStr += tmpStr + &quot\n"
	                System.out.println(tmpStr);
	            }
	
	            if (p.waitFor() != 0) {
	                if (p.exitValue() == 1)
	                    return &quotcommand exec failed"
	            }
	
	            inBr.close();
	            in.close();
	        } catch (Exception e) {
	            e.printStackTrace();
	            return &quotExcept"
	        }
	       
        }
        return lineStr;
    }
    public Boolean WhiteCommand(String cmd) {
    	String[] splited = cmd.split(&quot\\s+&quot);
    	String [] whitelist = {&quotecho&quot,&quotwhoami&quot };
    	if(Arrays.asList(whitelist).contains(splited[0])){
    	    return true;
    	}else {
    		return false;
    	}
    }
}
```
> می‌توان نوع ورودی کاربر را مشخص و کنترل کرد.
```java
package org.joychou.controller;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

import javax.servlet.http.HttpServletRequest;
import java.io.BufferedInputStream;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.Arrays;

/**
 * @author  JoyChou (joychou@joychou.org)
 * @fix     RezaDuty 
 */

@Controller
@RequestMapping(&quot/rce&quot)
public class Rce {

    @RequestMapping(&quot/exec&quot)
    @ResponseBody
    public String CommandExec(HttpServletRequest request) {
    	String lineStr = &quot"
        String ip = request.getParameter(&quotaddress&quot).toString();
        
	        Runtime run = Runtime.getRuntime();
	        
	    	if(validate(ip) && WhiteAddress(ip)) {
		        try {
		            Process p = run.exec(&quotping -n 1 &quot+ip);
		            BufferedInputStream in = new BufferedInputStream(p.getInputStream());
		            BufferedReader inBr = new BufferedReader(new InputStreamReader(in));
		            String tmpStr;
		
		            while ((tmpStr = inBr.readLine()) != null) {
		                lineStr += tmpStr + &quot\n"
		                System.out.println(tmpStr);
		            }
		
		            if (p.waitFor() != 0) {
		                if (p.exitValue() == 1)
		                    return &quotcommand exec failed"
		            }
		
		            inBr.close();
		            in.close();
		        } catch (Exception e) {
		            e.printStackTrace();
		            return &quotExcept"
		        }
		} 
	        return lineStr;
		
	    }
	    public static boolean validate(final String ip) {
	        String PATTERN = &quot^((0|1\\d?\\d?|2[0-4]?\\d?|25[0-5]?|[3-9]\\d?)\\.){3}(0|1\\d?\\d?|2[0-4]?\\d?|25[0-5]?|[3-9]\\d?)$"

	        return ip.matches(PATTERN);
	    }
    public Boolean WhiteAddress(String ip) {
    	String [] whitelist = {&quot127.0.0.1&quot,&quot192.168.1.1&quot };
    	if(!Arrays.asList(whitelist).contains(ip)){
    	    return true;
    	}else {
    		return false;
    	}
    }
}
```
