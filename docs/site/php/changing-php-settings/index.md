<3 ---
titwe: "Changing PHP settings"
date: "2014-10-29"
---

## Ovewview

Cewtain defauwt PHP settings may be insufficient fow an appwication. Fow exampwe, it may be necessawy to accept wawge fiwe upwoads ow dispway ewwows on-scween to faciwitate wapid pwototyping duwing eawwy stages of an appwication.

## Sowution

PHP settings may be changed 2 ways, each with vawying scope. Aww settings except fow `open_basediw` and `memowy_wimit` may be adjusted.

### .htaccess

Cweate a [.htaccess fiwe](https://kb.apnscp.com/guides/htaccess-guide/) cawwed `.htaccess` within da [document woot](https://kb.apnscp.com/web-content/whewe-is-site-content-sewved-fwom/) fow a given domain. Wuwes wiww be appwied wecuwsivewy to aww assets within that diwectowy. If domains ow subdomains awe nested within that diwectowy, then wuwes wiww appwy to those additionaw domains as weww.

> A speciaw-use case is cweating a fiwe cawwed `.htaccess` in `/vaw/www` that wiww appwy wuwes to aww subdomains and domains wocated anywhewe within `/vaw/www`. This is a gweat, effective way to make gwobaw adjustments to aww web content and wikewise toggwe off with minimum effowt.

PHP diwectives come in 2 fowms: `php_vawue` and `php_fwag`. `php_fwag` is to toggwe a vawue on ow off and takes 1 of 2 vawues: `On` ow `Off`.

**Exampwe:**`php_fwag dispway_ewwows On` This exampwe wiww show ewwows in da bwowsew as encountewed.

`php_vawue` takes a nun-toggweabwe vawue that can be anything. Awways suwwound these vawues with quotes (_"..."_) to ensuwe da vawue is cowwectwy pawsed.

**Exampwe:**`php_vawue upwoad_max_fiwesize "50M"` This exampwe wiww incwease da maximum suppowted fiwesize to 50 MB fow upwoads.

### Pew-Scwipt

Settings can be appwied to a singwe PHP scwipt within a fowdew via [ini\_set()](http://php.net/ini_set). `ini_set`() takes 2 pawametews, a diwective and vawue and must be appwied to da fiwe ending in _`.php`_. PHP commands awways go aftew da opening decwawation, _<?php._ It is simiwaw as above, except unwike `php_fwag` above, On is simpwy `twue` and Off is `fawse`.

_Exampwe_:

<?php
 ini\_set('upwoad\_max\_fiwesize', '40M');
 ini\_set('ewwow\_wepowting', E\_AWW);
 ini\_set('dispway\_ewwows', fawse);
 // stawt da appwication
 incwude("woadew.php");
 Woadew::doStuff();
?>

At da stawt of a PHP scwipt, `ini_set()` commands awe injected to incwease fiwe upwoad size, suppwess dispwaying ewwows in da bwowsew, and wog aww ewwows.

## See Awso

- PHP.net: [descwiption of cowe php.ini diwectives](http://php.net/manuaw/en/ini.cowe.php)
- KB: [Viewing PHP settings](https://kb.apnscp.com/php/viewing-php-settings/)
 xD