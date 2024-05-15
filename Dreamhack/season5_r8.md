# Dreamhack CTF Season5 Round #8 Write up 

처음으로 CTF이라는 것에 참여를 해보았다. 4개 부문 중에 무엇을 할까 고민하다 가장 성공한 사람이 많아보이는 웹 분야로 도전을 해 보았다. 이름은 easy-login이다. 관리자 계정으로 들어간 다음 flag를 얻는 방식이라고 한다.  사실 아직은 아는 것이 전혀 없는 상태이기 때문에 CTF체험을 해본 것으로 의의를 두고 있다. 

파일을 열러 보니 run.sh , flag.php, login.php, index.php, dockerfile, style.css 이 있었다. 

먼저 run.sh
```bash
#!/bin/bash

export FLAG="test"
&>/dev/null /usr/sbin/apachectl -DFOREGROUND -k start
```
flag.php
```php
:wq<?php
$flag = "testflag";
?>
```
login.php
```php
<form id="redir" action="index.php" method="post">
    <?php
    $a = array();
    foreach ($_POST as $k => $v) {
        $a[$k] = $v;
    }

    $j = json_encode($a);
    echo '<input type="hidden" name="cred" value="' . base64_encode($j) . '">';
    ?>
</form>

<script type="text/javascript">
    document.getElementById('redir').submit();
</script
```
index.php
```php
<?php

function generatePassword($length) {
    $characters = '0123456789abcdef';
    $charactersLength = strlen($characters);
    $pw = '';
    for ($i = 0; $i < $length; $i++) {
        $pw .= $characters[random_int(0, $charactersLength - 1)];
    }
    return $pw;
}

function generateOTP() {
    return 'P' . str_pad(strval(random_int(0, 999999)), 6, "0", STR_PAD_LEFT);
}

$admin_pw = generatePassword(32);
$otp = generateOTP();

function login() {
    if (!isset($_POST['cred'])) {
        echo "Please login...";
        return;
    }

    if (!($cred = base64_decode($_POST['cred']))) {
        echo "Cred error";
        return;
    }

    if (!($cred = json_decode($cred, true))) {
        echo "Cred error";
        return;
    }

    if (!(isset($cred['id']) && isset($cred['pw']) && isset($cred['otp']))) {
        echo "Cred error";
        return;
    }

    if ($cred['id'] != 'admin') {
        echo "Hello," . $cred['id'];
        return;
    }
    
    if ($cred['otp'] != $GLOBALS['otp']) {
        echo "OTP fail";
        return;
    }

    if (!strcmp($cred['pw'], $GLOBALS['admin_pw'])) {
        require_once('flag.php');
        echo "Hello, admin! get the flag: " . $flag;
        return;
    }

    echo "Password fail";
    return;
}

?>

<!DOCTYPE html>
<html>
<head>
    <link rel="stylesheet" type="text/css" href="style.css">
    <title>Easy Login</title>
</head>
<body>
    <div class="login-container">
        <h2>Login as admin to get flag<h2>
        <form action="login.php" method="post">
            <div class="form-group">
                <label for="id">ID</label>
                <input type="text" name="id"></br>
            </div>
            <div class="form-group">
                <label for="pw">PW</label>
                <input type="text" name="pw"></br>
            </div>
            <div class="form-group">
                <label for="otp">OTP</label>
                <input type="text" name="otp"></br>
            </div>
            <button type="submit" class="button">Login</button>
        </form>
        <div class="message">
            <?php login(); ?>
        </div>
    </div>
</body>
</html>
```
dockerfile
```php
FROM php:7.3-apache

COPY ./deploy/run.sh /usr/sbin/
RUN chmod +x /usr/sbin/run.sh

COPY ./deploy/src /var/www/html

EXPOSE 80
CMD ["/usr/sbin/run.sh"]
```

이 코드들을 보고 처음엔 정말 아무것도 생각이 나지 않았다. 그래도 뭐라도 해봐야 할 것 같아서 유심히 들여다 봤다. run.sh라는 것을 보고 뭔가 sh파일로 만들어봐야지 라는 생각이 들어서 즉흥적으로 이런 시도를 해보았다. 
![스크린샷 2024-04-20 145723](https://github.com/hyemsnail/Dreamhack/assets/163375128/fd907b05-cbc8-4784-91bf-05ce9e78732d)

dockerfile을 보니까 apache라는 것에서 시작을 해야 할 것 같은 느낌이 들었다. (FROM이라고 되어 있어서...) 그래서 apache가 뭔지 검색을 해보았다. 
아파치라고 부르는 것이구나... 라는 것을 깨닫고 설치를 한번 해보기로 했다.
![스크린샷 2024-04-20 151006](https://github.com/hyemsnail/Dreamhack/assets/163375128/f8af5ca9-68e0-4866-88b6-93e212117cc9)

설치를 다 한 것 같으니 실행을 해보려고 했다.
![스크린샷 2024-04-20 151103](https://github.com/hyemsnail/Dreamhack/assets/163375128/8e65b5cb-804f-444a-9708-f9d948488d06)
예상치 못한 상황이 벌어졌다. Failed라니.... 혹시 업데이트를 해야되는 건가 생각이 들어서 업데이트를 해 보았다. ![스크린샷 2024-04-20 151441](https://github.com/hyemsnail/Dreamhack/assets/163375128/9511d60b-2a78-4214-8a5f-97e3a97d20fc)
다시 한번 실행을 해 보았다. ![스크린샷 2024-04-20 152134](https://github.com/hyemsnail/Dreamhack/assets/163375128/63af570d-0ffd-469d-8471-2c7c5dc9e488) ![스크린샷 2024-04-20 154116](https://github.com/hyemsnail/Dreamhack/assets/163375128/93b2b101-35fc-4166-a4ce-b7e171ee6cc9)

status apache2로 확인을 해보니 설치는 된 것 같은데...뭐가 문제일까 애초에 이 길이 맞기는 한 걸까
그리고 php로 된 파일들이 꽤 있어서 php도 왠지 설치를 해야 할 것 같은 기분이 들었다. 그래서 아래 사진에 가장 마지막 줄에 한번 해 보았다. ![스크린샷 2024-04-20 153549](https://github.com/hyemsnail/Dreamhack/assets/163375128/7a09a08f-e362-4679-9809-14b61e2669b8)
.....

여기서부터는 더 전혀 모르겠다. 관리자 계정으로 접근을 해야 하는데 애초에 가지도 못했고 가는 방법도 잘 모르겠다....점점 지치는 것 같아서 이쯤에서 멈췄다. 나중에 다른 분이 올리시는 write-up을 보고 어떻게 하나 한번 익혀보아야겠다. 










