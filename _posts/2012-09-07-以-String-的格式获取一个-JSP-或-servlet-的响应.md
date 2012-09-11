---
layout: default
title: 以 String 的格式获取一个 JSP 或 servlet 的响应
---

一个思路是，发一个 http 请求给 jsp, 然后输出结果。但这样做不太优雅 —— 如果在同一个 web app 里面，需要再建一个 http connection 给自己，并且把参数重新再传给 jsp. 所以有了另一种思路。  
  
**目标**  
目标就是用一个 web container 生成 output 来替换掉 servlet 的 output. 而 container 输出 jsp 时用的是 `HttpServletResponse.getWriter()`，这样一来，你就能直接用它直接输出想要的 String 了。  
  
**代码** 
<pre> 
import java.io.CharArrayWriter;  
import java.io.IOException;  
import java.io.PrintWriter;  
  
import javax.servlet.http.HttpServletResponse;  
import javax.servlet.http.HttpServletResponseWrapper;  
  
public class CharArrayWriterResponse extends HttpServletResponseWrapper {  
  
  private final CharArrayWriter charArray = new CharArrayWriter();  
  
  public CharArrayWriterResponse(HttpServletResponse response) {  
	super(response);  
  }  

  @Override  
  public PrintWriter getWriter() throws IOException {  
    return new PrintWriter(charArray);  
  }  
  
  public String getOutput() {  
    return charArray.toString();  
  }  
} 



import java.io.IOException;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@SuppressWarnings("serial")
public class ServletUsingCustomResponse extends HttpServlet {

  @Override
  protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    String template = req.getParameter("tmpl");

    CharArrayWriterResponse customResponse = new CharArrayWriterResponse(resp);
    req.getRequestDispatcher(template).forward(req, customResponse);

    System.out.println(String.format("The output of %s is %s", template, customResponse.getOutput()));
  }
}


</pre>
