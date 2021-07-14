<languages />

<center>
|:-:|:-:|
|![](Check.png "Check.png")|**該漏洞已通過驗證**

* * * * *

<small>本頁面的EXP/POC/Payload經測試可用，漏洞已經成功復現。</small>|

</center>
漏洞信息
--------

此系統存在默認弱口令，以及前台sql注入。

FOFA
----

    "Content/images/login/logo.png" && "/Content/js/core/knockout-2.2.1.js"

弱口令
------

    super

    1234

SQL注入
-------

用戶名處存在SQL注入漏洞，使用BurpSuite插件利用（在用戶名處加入`*`）。

<https://github.com/c0ny1/sqlmap4burp-plus-plus/>

參考
----

<https://mp.weixin.qq.com/s/zxxOWSYgzY-z8GbBxEP_TQ>