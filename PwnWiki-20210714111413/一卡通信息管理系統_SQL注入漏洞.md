<languages />

<center>
|:-:|:-:|
|![](Check.png "Check.png")|**<translate>該漏洞已通過驗證</translate>**

* * * * *

<small><translate>本頁面的EXP/POC/Payload經測試可用，漏洞已經成功復現。</translate></small>|

</center>
<translate>

漏洞信息
--------

</translate> <translate> 此系統存在默認弱口令，以及前台sql注入。 </translate>

FOFA
----

    "Content/images/login/logo.png" && "/Content/js/core/knockout-2.2.1.js"

<translate>

弱口令
------

</translate>

    super

    1234

<translate>

SQL注入
-------

</translate>

<translate> 用戶名處存在SQL注入漏洞，使用BurpSuite插件利用（在用戶名處加入`*`）。 </translate> <https://github.com/c0ny1/sqlmap4burp-plus-plus/>

<translate>

參考
----

</translate> <https://mp.weixin.qq.com/s/zxxOWSYgzY-z8GbBxEP_TQ>