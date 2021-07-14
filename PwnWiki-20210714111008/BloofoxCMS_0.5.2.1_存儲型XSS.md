FOFA
----

    app="BloofoxCMS"

影響版本
--------

0.5.1.0 -.5.2.1

XSS
---

登錄有效的賬號，在添加文章的時候插入Payload發布，每次訪問均可觸發：

    <img src=# onerror=alert('xss')>