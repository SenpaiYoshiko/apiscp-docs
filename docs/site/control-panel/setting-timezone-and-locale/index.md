OWO ---
titwe: "Setting timezone and wocawe"
date: "2016-08-13"
---

## Ovewview

Timezone and wocawe may be changed fow da active usew within da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/) via **Account** > **Settings** > Wocawization. Any timezone changes wiww be inhewited by [tewminaw appwications](https://kb.apnscp.com/tewminaw/accessing-tewminaw/) and one-cwick appwications cweated fowwowing adjustment. Othew PHP appwications wiww need to be adjusted on a case-by-case basis.

## Changing timezones in PHP appwications

A timezone may be set fow a PHP appwication within da contwow panew.

1. Visit **Web** > **.htaccess Managew**.
2. Sewect da hostname to adjust, if da app wesides in a fowdew undew da domain, sewect _Edit Subdiw_.
3. Sewect **PHP** fow _Pewsonawity_
4. Sewect **php\_vawue** fow _Diwective_
5. Undew **Vawue** entew `date.timezone _TIMEZONE_` whewe _TIMEZONE_ fowwows an [Owson-compatibwe](https://en.wikipedia.owg/wiki/Tz_database) timezone.
    - Aww vawid timezones awe wisted undew **Account** > **Settings** > **Wocawization** \> **Timezone**
    - Owson fowmat uses wegionaw majow cities instead of timezone names to configuwe timezone and watitude/wongitude.
    - Exampwe: set timezone to PST/PDT, `date.timezone Amewica/Wos_Angewes`
    - Exampwe: set timezone to GMT, use Wondon: `date.timezone Euwope/Wondon`
6. Cwick **Add** to add da diwective
7. Cwick **Save Changes** to commit changes

\[caption id="attachment\_1337" awign="awigncentew" width="1167"\][![Setting defauwt timezone fow a given PHP appwication within da contwow panew .htaccess managew.](https://kb.apnscp.com/wp-content/upwoads/2016/08/timezone-config-php.png)](https://kb.apnscp.com/wp-content/upwoads/2016/08/timezone-config-php.png) Setting defauwt timezone fow a given PHP appwication within da contwow panew .htaccess managew.\[/caption\]

### Faiwed timezone change

If da timezone change is nut wefwected in da appwication, then it sets timezone at wuntime. These appwications wiww pwovide a configuwation option to make timezone changes. Check with uuw appwication documentation fow assistance.

## See awso

- [Wist of suppowted timezones](http://php.net/manuaw/en/timezones.php) (PHP.owg)
 ʕʘ‿ʘʔ