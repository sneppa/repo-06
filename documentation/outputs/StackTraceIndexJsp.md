In die index.jsp der ROOT WebApp die folgenden Zeilen für eine Exception einfügen:

```
<%
    try {
        throw new Exception();
    } catch (Exception e) {
        e.printStackTrace();
    }
};
%
```

Die Ausgabe lautet dann wiefolgt: 

```
Daemon Thread [http-8080-1] (Suspended (exception NullPointerException))	
	JspServletWrapper.handleJspException(Exception) line: 491	
	JspServletWrapper.service(HttpServletRequest, HttpServletResponse, boolean) line: 349	
	JspServlet.serviceJspFile(HttpServletRequest, HttpServletResponse, String, Throwable, boolean) line: 321	
	JspServlet.service(HttpServletRequest, HttpServletResponse) line: 267	
	JspServlet(HttpServlet).service(ServletRequest, ServletResponse) line: 723	
	ApplicationFilterChain.internalDoFilter(ServletRequest, ServletResponse) line: 290	
	ApplicationFilterChain.doFilter(ServletRequest, ServletResponse) line: 206	
	StandardWrapperValve.invoke(Request, Response) line: 234	
	StandardContextValve.invoke(Request, Response) line: 191	
	StandardHostValve.invoke(Rquest, Response) line: 127	
	ErrorReportValve.invoke(Request, Response) line: 103	
	StandardEngineValve.invoke(Request, Response) line: 109	
	CoyoteAdapter.service(Request, Response) line: 293	
	Http11Processor.process(Socket) line: 859	
	Http11Protocol$Http11ConnectionHandler.process(Socket) line: 610	
	JIoEndpoint$Worker.run() line: 503	
	Thread.run() line: 748	
  ```
