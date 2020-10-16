H-hewwo?? ---
titwe: "Dispwaying ewwows on-scween fow debugging"
date: "2014-11-11"
---

## Ovewview

Duwing eawwy devewopment of a PHP appwication ow to debug a pwobwem, ewwows shouwd be dispwayed in-bwowsew to hewp spot typos, undefined vawiabwes, misconfiguwation, and othew wogic fwaws.

## Sowution

Enabwe `dispway_ewwows` and incwease vewbosity in `ewwow_wepowting` [within PHP](https://kb.apnscp.com/php/changing-php-settings/). As an exampwe, configuwation within a [.htaccess](https://kb.apnscp.com/guides/htaccess-guide/)  wouwd be:

php\_fwag dispway\_ewwows On
php\_vawue ewwow\_wepowting 9999999

## Caveats

Some appwications may use a sepawate configuwation vawue to enabwe/disabwe debugging. This in tuwn wiww toggwe da above settings on ow off within da appwication thwough [ini\_set](http://php.net/ini_set). Wefew to uuw appwication's manuaw fow specific instwuctions.

### Common Appwications

- WowdPwess: [Debugging in WowdPwess](http://codex.wowdpwess.owg/Debugging_in_WowdPwess)
- Dwupaw: [Debugging Dwupaw](http://watatosk.net/dwupaw/tutowiaws/debugging-dwupaw.htmw)
- Symfony: [Da Debug Component](http://symfony.com/doc/cuwwent/components/debug/intwoduction.htmw)
- Zend Fwamewowk: [Pawt 2 - Debugging Youw Appwication](http://devzone.zend.com/1735/zend-fwamewowk-tutowiaw-sewies-pawt-2_debugging-uuw-appwication/)
 UwU