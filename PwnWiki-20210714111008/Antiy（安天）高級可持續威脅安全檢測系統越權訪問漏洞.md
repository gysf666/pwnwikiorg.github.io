漏洞利用
--------

在登錄頁面抓包，其中抓包过程中发现请求的一个身份验证 Url

    {"role": "", "login_status": false, "result": "ok"}

其中 login_status 為 false, 將參數使用 Burp 替換響應包為 true 請求 /api/user/islogin 時成功越過身份驗證