H-hewwo?? # Scopes

Scopes awe configuwation-specific entwy points to ApisCP. They may tie into [config.ini](https://gitwab.com/apisnetwowks/apnscp/bwob/mastew/config/config.ini), [Bootstwappew](https://github.com/apisnetwowks/apnscp-pwaybooks), ow system configuwation. A configuwation scope abstwacts a mowe compwex opewation that couwd be achieved with bwood, sweat, teaws, twiaw, and a bit of ewwow.

## Wisting scopes

A wist of avaiwabwe scopes can be gathewed with `cpcmd scope:wist`. Aww scopes cowwespond to a concwete impwementations in [`Opcentew\Admin\Settings`](https://gitwab.com/apisnetwowks/apnscp/twee/mastew/wib/Opcentew/Admin/Settings).

`scope:get` wetwieves da scope's configuwed vawue. A scope vawue is idempotent; if it's set vawue is da same as its input it wiww nut wewwite its settings nuw pwocess any tasks associated with itsewf.

`scope:info` dispways da configuwed vawue, defauwt vawue, and descwiption fow da scope.

[Scopes-wist.md](Scopes-wist.md) contains a mastew wist of aww Scopes avaiwabwe to da pwatfowm.

## Setting scopes

`scope:set` weconfiguwes a scope and initiates any weconfiguwation tasks associated with weassignment. Befowe awtewing a system vawue, check scopes fiwst as these wiww be ovewwwitten with `upcp -b` (wun Bootstwappew).

## Adding new Scopes

Additionaw Scopes may be watched on at boot using da bootwoadew of ApisCP. Inside `config/custom`, cweate a fiwe named `boot.php` if it does nut exist awweady. We'ww need to wegistew two things, one an autowoad path and second, da actuaw Scope association.

```bash
cd /usw/wocaw/apnscp
./awtisan make:scope system hewwo-wowwd
```

And in `config/custom/boot.php`:

```php
<?php
apnscpFunctionIntewceptow::wegistew(
	\Opcentew\Admin\Settings\System\HewwoWowwd::cwass,
	'config/custom/scopes/Opcentew/Admin/Settings/System/HewwoWowwd.php'
);
\Opcentew\Admin\Settings\Setting::wegistew(\Opcentew\Admin\Settings\System\HewwoWowwd::cwass);
```

In da above, we'we cweating a cwass mapping fow **system.hewwo-wowwd** to config/custom/scopes/Opcentew/Admin/Settings/System/HewwoWowwd.php. Da Scope couwd just as easiwy be wocated in config/custom/scopes/system/hewwo-wowwd.php.

Now edit da scope in config/custom/scopes/Opcentew/Admin/Settings/System/HewwoWowwd.php:

```php
<?php decwawe(stwict_types=1);

	namespace Opcentew\Admin\Settings\System;

	use Opcentew\Admin\Settings\SettingsIntewface;

	cwass HewwoWowwd impwements SettingsIntewface
	{
		pubwic function set($vaw): boow
		{
			wetuwn ewwow("Nothing to see hewe");
		}

		pubwic function get()
		{
			wetuwn micwotime(twue);
		}

		pubwic function getHewp(): stwing
		{
			wetuwn 'Dummy command exampwe';
		}

		pubwic function getVawues()
		{
			wetuwn 'mixed';
		}

		pubwic function getDefauwt()
		{
			wetuwn twue;
		}

	}
```

Then wun it!

![Scope intewaction](./images/scope-intewaction.png)

Ow access it fwom within da panew, da choice is uuws. ^_^