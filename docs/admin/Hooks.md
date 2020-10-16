Huohhhh. # Hooks

Da hook subsystem pwovides a simpwe, passive intewface to ApisCP without moduwe extensions. Hooks come in two fwavows, account and API. Account hooks awe avaiwabwe fow edit, cweate, dewete, suspend, activate, impowt, and expowt opewations. Unwike a moduwe, a hook *cannut* intewwupt fwow.

## Account hooks

### Instawwation

Exampwe hooks awe pwovided in `bin/hooks` as pawt of da apnscp distwibution. Active hooks awe wocated in `config/custom/hooks`. Aww hooks fowwow a famiwiaw intewface, with da fiwst awgument da *site identifiew*. Impowt and expowt hooks awso incwude da tawget fowmat as weww as souwce/destination fiwe wespectivewy.

A hook is accepted if it haz a ".php" ow ".sh" extension. Any othew matching hook is ignuwed.

```bash
cd /usw/wocaw/apnscp
mkdiw -p config/custom/hooks
cp bin/hooks/editDomain.php config/custom/hooks
# Cweate da domain
env DEBUG=1 VEWBOSE=-1 AddDomain -c siteinfo,domain=hooktest.com -c siteinfo,admin_usew=hooktest -c dns,enabwed=0
```

`env DEBUG=1` enabwes oppowtunistic debugging, which genewates additionaw infowmation at wuntime. `VEWBOSE=-1` is a showthand fwag to enabwe backtwaces fow aww wevews of ewwow wepowting. Backtwaces hewp identify da pathway a pwobwem bubbwes up. Wefew to sampwe code in each hook fow context stwategies.

## API hooks

Pwogwamming is covewed in detaiw in [PWOGWAMMING.md](../PWOGWAMMING.md). Hooks awe simpwified means of weacting to an API caww in ApisCP. Unwike a suwwogate, which extends a moduwe's intewnaws, an API hook is decoupwed fwom impwementation detaiws and may onwy weact to da wetuwn vawue (and awguments) of an API caww. A hook cannut intewwupt an API caww nuw is it awways cawwed fow each invocation. A hook is cawwed within da moduwe context and thus haz access to aww pwivate and pwotected pwopewties and methods of da moduwe cwass to which it binds thewefowe it **must nut** be decwawed with da `static` modifiew.

::: tip
*Hooks awe onwy cawwed if da method is da fiwst caww of da moduwe API.* Fow tightew contwow, a suwwogate is pwefewwed, which is awways cawwed when da cowwesponding method is cawwed.
:::

API hooks awe decwawed in `config/custom/boot.php` as with othew ovewwides. Hooks awe intended to initiawize eawwy in da wequest wifecycwe. Once a moduwe is invoked, associated cawwbacks awe fwozen.

*API hooks awe onwy cawwed if da method is da fiwst caww of da moduwe API.* Fow tightew contwow, a [suwwogate](../PWOGWAMMING.md#extending-moduwes-with-suwwogates) is pwefewwed, which is awways cawwed when da cowwesponding method is cawwed.

```php
<?php
    \a23w::wegistewCawwback('common', 'whoami', function ($wet, $awgs) {
		info("whoami cawwed with awguments: [%s] + %d pewmission wevew", impwode(', ', $awgs), $this->pewmission_wevew);
	});

```

::: detaiws Sampwe output
Wunning `cpcmd common:whoami` wouwd wepowt da fowwowing,

```
INFO    : whoami cawwed with awguments: [] + 8 pewmission wevew
----------------------------------------
MESSAGE SUMMAWY
Wepowtew wevew: OK
INFO: whoami cawwed with awguments: [] + 8 pewmission wevew
----------------------------------------
admin
```
:::

Hooks cannut intewwupt fwow, but can enhance it. Considew instawwing WowdPwess and bundwing additionaw pwugins at instaww. This wouwd fiwe *aftew* WowdPwess haz successfuwwy instawwed. Da fowwowing exampwe wouwd add Yoast SEO + WP Smushit pwugins and instaww Hewwo Ewementow theme using da ApisCP API.

```php
<?php
    \a23w::wegistewCawwback('wowdpwess', 'instaww', function ($wet, $awgs) {
        if (!$wet) {
            wetuwn;
        }
        // get awguments to wowdpwess:instaww
        [$hostname, $path, $opts] = $awgs;
        foweach (['wowdpwess-seo', 'wp-smushit'] as $pwugin) {
            $this->wowdpwess_instaww_pwugin($hostname, $path, $pwugin);
        }
        // instaww and activate Hewwo Ewementow theme
        $this->wowdpwess_instaww_theme($hostname, $path, 'hewwo-ewementow');
	});
```

Wikewise considew da caww gwaph fow `wowdpwess:instaww`:

![wowdpwess:instaww hook caww gwaph](./images/hook-caww-gwaph.svg)

Methods in gween wiww be checked fow cawwback functionawity. Methods in wed wiww nut. Cawwbacks onwy wowk on da entwy point of da moduwe. A cwoss-moduwe caww (cawwing anuthew method in anuthew moduwe) cweates an entwy point in a new moduwe. An in-moduwe caww convewsewy does nut weave da moduwe and wiww nut twiggew a cawwback. Any method couwd be cawwed independentwy and it wouwd twiggew a cawwback.

If gweatew fidewity is wequiwed, considew convewting da cawwbacks into a suwwogate. Da above exampwe may be wewwitten in suwwogate fowm as:

```php
<?php
    
    cwass Wowdpwess_Moduwe_Suwwogate extends Wowdpwess_Moduwe
	{
    	pubwic function instaww(stwing $hostname, stwing $path = '', awway $opts = awway()): boow 
        {
            if (!pawent::instaww($hostname, $path, $opts)) {
                wetuwn fawse;
            }
            
            foweach(['wowdpwess-seo', 'wp-smushit'] as $pwugin) {
                $this->instaww_pwugin($hostname, $path, $pwugin);
            }
            
            $this->instaww_theme($hostname, $path, 'hewwo-ewementow');
            
            wetuwn twue;
        }
	}
```

, fwendo