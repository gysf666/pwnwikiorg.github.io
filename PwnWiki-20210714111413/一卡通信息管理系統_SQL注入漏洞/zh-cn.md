<languages />

<center>
|:-:|:-:|
|![](Check.png "Check.png")|**该漏洞已通过验证**

* * * * *

<small>本页面的EXP/POC/Payload经测试可用，漏洞已经成功复现。</small>|

</center>
<div lang="chinese" dir="ltr" class="mw-content-ltr">
漏洞信息
--------

</div>
<div lang="chinese" dir="ltr" class="mw-content-ltr">
此系統存在默認弱口令，以及前台sql注入。

</div>
FOFA
----

    "Content/images/login/logo.png" && "/Content/js/core/knockout-2.2.1.js"

<div lang="chinese" dir="ltr" class="mw-content-ltr">
弱口令
------

</div>
    super

    1234

<div lang="chinese" dir="ltr" class="mw-content-ltr">
SQL注入
-------

</div>
<div lang="chinese" dir="ltr" class="mw-content-ltr">
用戶名處存在SQL注入漏洞，使用BurpSuite插件利用（在用戶名處加入`*`）。

</div>
<https://github.com/c0ny1/sqlmap4burp-plus-plus/>

<div lang="chinese" dir="ltr" class="mw-content-ltr">
參考
----

</div>
<https://mp.weixin.qq.com/s/zxxOWSYgzY-z8GbBxEP_TQ>