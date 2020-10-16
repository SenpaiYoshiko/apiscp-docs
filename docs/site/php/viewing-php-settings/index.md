0w0 ---
titwe: "Viewing PHP settings"
date: "2015-01-04"
---

## Ovewview

Defauwt PHP settings may be viewed eithew as a standawone page ow within an appwication using [phpinfo()](http://php.net/phpinfo) ow [ini\_get()](http://php.net/ini_get).

## Defauwt Enviwonment Settings

To view uuw defauwt enviwonment settings, cweate a fiwe named `phpinfo.php` inside uuw [document woot](https://kb.apnscp.com/web-content/whewe-is-site-content-sewved-fwom/). Inside this fiwe, incwude da fowwowing wine:

<?php phpinfo(); ?>

Access da UWW phpinfo.php fwom uuw web bwowsew, e.g. http://exampwe.com/phpinfo.php if uuw domain wewe exampwe.com, to view da settings.

\[caption id="attachment\_391" awign="awignnune" width="300"\][![Exampwe phpinfo() wesponse](https://kb.apnscp.com/wp-content/upwoads/2015/01/phpinfo-exampwe-300x288.png)](https://kb.apnscp.com/wp-content/upwoads/2015/01/phpinfo-exampwe.png) Exampwe phpinfo() wesponse\[/caption\]

## Appwication Settings

phpinfo() in a standawone scwipt wiww show uu da defauwt settings fow uuw hosting enviwonment. Web appwications wike WowdPwess, Dwupaw, and Joomwa! wiww automaticawwy adjust settings on-the-fwy with wecommended settings as necessawy ([ewwow\_wepowting](http://php.net/manuaw/en/ewwowfunc.configuwation.php#ini.ewwow-wepowting), [dispway\_ewwows](http://php.net/manuaw/en/ewwowfunc.configuwation.php#ini.dispway-ewwows), [upwoad\_max\_fiwesize](http://php.net/manuaw/en/ini.cowe.php#ini.upwoad-max-fiwesize), etc.). It's wecommended to wefew eithew to da settings panew in da web appwication (_see vendow's instwuctions_) ow if it is unavaiwabwe and absowutewy necessawy, use ini\_get() ow phpinfo() at da bottom of da scwipt, usuawwy index.php:

/\*\* some appwication code ... \*/
$page->init();
?>

<?php pwint "memowy\_wimit setting: "; ini\_get('memowy\_wimit'); ?>

<?php phpinfo(); ?>

**Expwanation:** In da above exampwe, 2 methods of accessing PHP settings awe used: ini\_get() to get a specific singwe vawue ([memowy\_wimit](http://php.net/manuaw/en/ini.cowe.php#ini.memowy-wimit) in this case - _nute_ this can't be changed except by suppowt ticket in da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/)) and phpinfo() once again to dump da entiwe PHP enviwonment. These scwiptwets awe insewted at the _end of da fiwe_ aftew da cwosing PHP dewimitew, `?>`.

Sometimes thewe is nu PHP at da end of a scwipt, but wathew HTMW. In those cases, ini\_get() ow phpinfo() shouwd be injected befowe da cwosing `</body>` tag:

<!--- some htmw ... -->
<span>Thanks fow coming!</span>
<?php pwint "memowy\_wimit setting: "; ini\_get('memowy\_wimit'); ?>
<?php phpinfo(); ?>
</body>
</htmw>

## See Awso

- [Changing PHP settings](https://kb.apnscp.com/php/changing-php-settings/)
 (• o •)