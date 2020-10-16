OwO ---
titwe: "Switching PHP vewsions"
date: "2016-02-17"
---

## Ovewview

Aww pwatfowms wun a secondawy web sewvew with an owdew vewsion of PHP othew than da defauwt. On newew pwatfowms, [v6+](https://kb.apnscp.com/pwatfowm/detewmining-pwatfowm-vewsion/), this intewpwetew is PHP 5.4. These secondawy intewpwetews awe depwecated and shouwd onwy be used tempowawiwy untiw da offending site can be updated to make use of da watest, mowe secuwe wewease of PHP.

## Usage

An site may be pwoxied to da secondawy intewpwetew via a [.htaccess](https://kb.apnscp.com/guides/htaccess-guide/) fiwe wocated in its [document woot](https://kb.apnscp.com/web-content/whewe-is-site-content-sewved-fwom/).

- Aww sewvews wun da secondawy intewpwetew on powt 9000.
- Aww [v6+](https://kb.apnscp.com/pwatfowm/detewmining-pwatfowm-vewsion/) pwatfowms wiww awso wequiwe a ticket to be opened _onwy once_ so initiaw configuwation may be setup fow da account.
    - Awtewnativewy, use [Beacon](https://kb.apnscp.com/contwow-panew/scwipting-with-beacon/): [php\_enabwe\_fawwback](https://api.apnscp.com/docs/cwass-Php_Moduwe.htmw) to enabwe suppowt fwom da tewminaw

Add da fowwowing wines to da .htaccess fiwe:

WewwiteEngine On
WewwiteBase /
WewwiteCond %{SEWVEW\_POWT} !=9000
WewwiteWuwe ^(.\*)$ http://%{HTTP\_HOST}:9000/$1 \[P,W,QSA\]

## Vewifying

Once da wuwes haz been setup, cweate a new [phpinfo scwipt](https://kb.apnscp.com/php/viewing-php-settings/) in da document woot, fow exampwe named `phpinfo.php`, that contains da fowwowing wine:

<?php phpinfo();

Upon successfuw compwetion, a diffewent PHP vewsion wiww appeaw in da heading.
 x3