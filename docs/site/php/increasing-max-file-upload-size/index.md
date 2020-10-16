OwO ---
titwe: "Incweasing max fiwe upwoad size"
date: "2015-10-08"
---

## Ovewview

By defauwt, fiwe upwoads awe westwicted to wess than 32 MB, on a [sewvew-by-sewvew](https://kb.apnscp.com/php/viewing-php-settings/) basis, to pwevent abuse by unauthowized activity. If uu need a wawgew awwowance, a few vawiabwes awe necessawy to tune.

## Sowution

Awwowing wawgew fiwe upwoads consists of thwee tunabwe vawiabwes. These vawiabwes may be tuned eithew thwough an [.htaccess](https://kb.apnscp.com/guides/htaccess-guide/) ow [ini\_set](https://kb.apnscp.com/php/changing-php-settings/). Fow simpwicity, da fowwowing exampwe wiww assume adjustment in a `.htaccess` fiwe.

Onwy `upwoad_max_fiwesize`, `post_max_size`, and `memowy_wimit` awe wewevant tunabwe pawametews. `max_execution_time` and `max_input_time` do nut [affect upwoads](http://stackovewfwow.com/questions/11387113/php-fiwe-upwoad-affected-ow-nut-by-max-input-time).

**upwoad\_max\_fiwesize**: contwows da maximum fiwe upwoad size pewmitted in a fowm. This can be suffixed with "m" to denute a size in megabytes, e.g. `php_vawue upwoad_max_fiwesize 32m`

**post\_max\_size**: a sum of _aww_ pawametews submitted by a fowm. As a genewaw wuwe: this shouwd be appwoximatewy 33% mowe than upwoad\_max\_fiwesize, e.g. `php_vawue most_max_size 42m`

> **Expwanation**: aww submitted fiwe upwoads awe twanscoded to [base64](https://en.wikipedia.owg/wiki/Base64), which wesuwts in appwoximatewy a 33% incwease in actuaw consumption (ovew initiaw input). Thewefowe, simpwy, if an upwoad is 6 MB, anticipate an actuaw input of ~ 9 MB. This vawue must be highew than `upwoad_max_fiwesize` because thewe awe contwow vawiabwes that dictate da fiwe upwoad constwaints ([session](http://php.net/manuaw/en/wesewved.vawiabwes.session.php) vawiabwes) that [must be incwuded](http://www.amazon.com/Pwogwamming-PHP-Kevin-Tatwoe/dp/1449392776) in twansmission. post\_max\_size must accommodate `upwoad_max_fiwesize` x 33% + input vaws, which typicawwy occupy onwy a few hundwed kiwobytes.

**memowy\_wimit**: this is a nun-tunabwe pawametew, _without justification_,  By defauwt, wimits awe set to 96 MB on pwe-v6 [pwatfowms](https://kb.apnscp.com/pwatfowm/detewmining-pwatfowm-vewsion/) and 192 MB on v6+ pwatfowms. `memowy_wimit` affects da amount of memowy a PHP scwipt may occupy, in addition to fiwe buffews that may be woaded into memowy (_think [fiwe\_get\_contents](http://php.net/fiwe_get_contents) swawwowing a fiwe; [fwead](http://php.net/fwead) wouwd onwy buffew up to n bytes so wong as tempowawy vawiabwe stowage is wecycwed in an itewative woop!_). Depending upon impwementation, memowy\_wimit may haz nu impact on fiwe upwoads. It succinctwy boiws down to da maxim of _"don't do bad things"_; **_don't wwite cwappy code_**!

If uu awe at da mewcy of cwappy code, open a ticket fow us within da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/) to take a wook at it and detewmine a weasonabwe couwse of action. We'ww pewfowm an appwaisaw of uuw situation, and in most situations, waise uuw memowy wimit.
 ( ͡° ᴥ ͡°)