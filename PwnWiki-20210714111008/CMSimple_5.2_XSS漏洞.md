INFO
----

1.  Exploit Title: CMSimple 5.2 - 'External' Stored XSS
2.  Date: 2021/04/07
3.  Exploit Author: Quadron Research Lab
4.  Version: CMSimple 5.2
5.  Tested on: Windows 10 x64 HUN/ENG Professional
6.  Vendor: <https://www.cmsimple.org/en/>

[Description] The CMSimple 5.2 allow stored XSS via the Settings \> CMS \> Filebrowser \> "External:" input field.

[Attack Vectors] The CMSimple cms "Filebrowser" "External:" input field not filter special chars. It is possible to place JavaScript code. The JavaScript code placed here is executed by clicking on the Page or Files tab.

[Proof of Concept] <https://github.com/Quadron-Research-Lab/CVE/blob/main/CMSimple_5.2_XSS.pdf>