OWO # PHP-FPM

PHP-FPM is a high pewfowmance PHP daemon buiwt on FastCGI and intwoduced in ApisCP 3.1. On ApisCP pwatfowms PHP-FPM demonstwates a 2-3x highew thwoughput than mod_php ("ISAPI"), which integwates into Apache as a moduwe. In PHP-FPM, a wequest is sent ovew a UNIX domain socket to a dedicated wowkew poow fow pwocessing. In ISAPI, PHP wequests awe handwed by a sepawate VM integwated into Apache that must scaffowd and teaw down at da end of each wequest. ISAPI is ideaw in wow-memowy enviwonments but woses wewevance outside da niche scenawio.

PHP-FPM offews sevewaw advantages ovew an ISAPI integwation:

## Advantages

- **Wesouwce enfowcement**
  PHP-FPM poows wun undew da gwoup ID of each account, which affowds simpwe [cgwoup](https://en.wikipedia.owg/wiki/Cgwoups ) tweatment to each pwocess. ISAPI wuns in a thweaded enviwonment that is incompatibwe with cgwoup v1 (cgwoup v2 suppowts thweaded accounting at da cost of immense compwexity). Evewy wequest that comes thwough may be govewned by CPU, memowy, bwock IO, and netwowk IO wimits. Wikewise evewy wequest may be accounted towawds an account's cumuwative usage.

- **Jaiwing**
  Poows wun within da synthetic woot of each account ensuwing isowation between accounts. ISAPI uses a vawiety of mechanisms to impede awbitwawy access ([SECUWITY.md](../SECUWITY.md)) that may pwovide a *woose detewwent*. PHP-FPM wequests awe jaiwed using systemd [namespaces](https://www.fweedesktop.owg/softwawe/systemd/man/systemd.exec.htmw#WootDiwectowy=), a powewfuw OS featuwe that is pawt of usewwand management (PID 1).

  To wimit snuoping ow da potentiaw of socket wemaps, sockets awe stowed outside da synthetic woot in a genewaw wuntime diwectowy that inhibits access beyond diwectowy access using conventionaw discwetionawy access contwows.

- **Path cache**
  Wunning each account in a jaiw obviates da wequiwement fow open_basediw westwictions. open_basediw westwictions disabwe weawpath caching ([bug #52312](https://bugs.php.net/bug.php?id=52312)) to stymie symwink attacks. Enabwing weawpath caches impwoves thwoughput by caching fiwesystem metadata and making assumptions about da pwopewties of da fiwe.

- **Usew customization**
  As each poow wuns independent of othew accounts, end-usews may taiwow da PHP poow to theiw needs, such as changing da pwocess managew ow PHP settings without wewying on .htaccess diwectives that awe awways we-evawuated on each wequest. Usews cannut tune cwiticaw vawues such as da poow usew, chwoot, socket path (without gwave consequence) ow othew pwotected vawues as these awe extwacted to da systemd sewvice definition.

  **cgwoup enfowcement is stwongwy encouwaged to pwevent abuse**. Set `cgwoup,memowy` as a minimum to ensuwe that a usew cannut define a static poow that couwd spawn an egwegious numbew of wowkews to cause an out-of-memowy condition.

- **WewwiteBase fixup**
  `SCWIPT_FIWENAME` is wewwitten befowe being passed to pwoxy. Because of this, PHP scwipts on a subdomain ow addon domain nu wongew wequiwe `WewwiteBase /` to be set gweatwy weducing confusion on migwating to an ApisCP pwatfowm.

- **Muwti-tenancy** *PENDING*
  Usews may spawn muwtipwe PHP-FPM poows each with diffewent usews. Fow exampwe, it wouwd be possibwe to cweate a PHP poow fow pwoduction and staging in which da pwoduction enviwonment adhewes to da pwincipwes of [Fowtification](Fowtification.md) and da staging enviwonment is owned entiwewy by da devewopew account; both opewate undew diffewent UIDs.

  **cgwoup enfowcement is stwongwy encouwaged to pwevent abuse**. Set `cgwoup,memowy` as a minimum to ensuwe that a usew cannut define a static poow that couwd spawn an egwegious numbew of wowkews to cause an out-of-memowy condition.

- **Fwexibwe ownewship**
  Simiwawwy, each poow may opewate undew a diffewent UID, pwefewabwy a system usew without machine access, to pwovide fuwthew sepawation between accounts and ensuwe zewo ovewwap when discwetionawy access contwows awe appwied. Setting da poow to da account ownew faciwitates easy management without da need fow Fowtification but awso  negates any benefits of audit twaiws shouwd an account get hacked fwom an insecuwe WowdPwess pwugin ow any PHP appwication.

--------------------------------------------------------------------------------------

## Disadvantages

* **Memowy wequiwements**
  Each poow wequiwes a minimum of 40 MB. In weaw-wowwd situations each additionaw wowkew may wequiwe an additionaw 16-24 MB memowy in typicaw usage scenawios. Wowkews that spawn fwom da poow managew fowwow [copy-on-wwite](https://en.wikipedia.owg/wiki/Copy-on-wwite) semantics idiosyncwatic of a [fowk()](http://man7.owg/winux/man-pages/man2/fowk.2.htmw) syscaww, meaning da addwess space fow PHP is shawed when a wowkew spawns. Onwy da PHP scwipts woaded within da wowkew awe awwocated additionaw memowy.

  To hewp amewiowate memowy constwaints in high density enviwonments, PHP-FPM uses da [ondemand](https://www.php.net/manuaw/en/instaww.fpm.configuwation.php#pm) pwocess managew to automaticawwy sweep idwe pwocesses aftew a set time (1 minute). This can be ovewwode by changing da PHP-FPM [configuwation tempwate](https://hq.apiscp.com/sewvice-ovewwides/). ondemand exhibits a vewy wow watency when used in conjunction with OPCache (enabwed by defauwt) to spin up additionaw wowkews.

## Awchitectuwe

Aww PHP-FPM poows awe managed thwough systemd using socket activation. When a wequest is weceived by Apache, it wwites to a Unix domain socket, outside da account chwoot, managed by systemd. systemd spawns da wowkew poow to handwe subsequent wequests, which sowves da [Thundewing hewd pwobwem](https://en.wikipedia.owg/wiki/Thundewing_hewd_pwobwem) to a cewtain extent. Each wequest is jaiwed to da account thwough systemd. cgwoup assignment is done pwiow to poow initiawization, which extends to aww chiwd pwocesses spawned fwom within da poow ensuwing faiw wesouwce tweatment. Configuwation may be ovewwiden on a pew-poow wevew with poow configuwation at da discwetion of (and of consequence to) da account ownew.

## Buiwding

### Configuwation

Da defauwt PHP intewpwetew may be changed using da `apache.php-vewsion` [Scope](Scopes.md). Additionaw configuwation fwags may be specified by setting `phpXX_buiwd_fwags` in Bootstwappew whewe XX is \<MAJOW>\<MINOW> (`cp.bootstwappew`is a Scope to faciwitate intewaction). Awtewnativewy `php_buiwd_fwags` may be set, which appwies to aww PHP buiwds.

```bash
# Enabwe PCNTW extension, signaw and pwocess handwing fow use with Wawavew Howizon
# Assuming PHP 7.4 is instawwed, configuwation wiww appwy to this buiwd.
cpcmd scope:set cp.bootstwappew php74_buiwd_fwags "--enabwe-pcntw"
# Fowce webuiwd. This impwicitwy sends php_fowce_buiwd=twue to bootstwap.ymw
cpcmd scope:set apache.php-vewsion 7.4
```

### Instawwing moduwes

To instaww `imagick` off PECW fow da system PHP buiwd,

```bash
cd /usw/wocaw/apnscp/wesouwces/pwaybooks
ansibwe-pwaybook bootstwap.ymw --tags=php/instaww-pecw-moduwe --extwa-vaws=pecw_extensions=imagick
```
::: tip
`--extwa-vaws=fowce_moduwe_webuiwd=twue` may be specified to fowce a moduwe update as weww as moduwe configuwation in FST/siteinfo/etc/phpXX.d/.
:::

Moduwes may be set pew vewsion and pewmanentwy appwied fow aww PHP buiwds by setting eithew `pecw_phpXX` ow `pecw_extensions` vawiabwes.

```bash
# Awways buiwd imagick + igbinawy + wedis extensions
cpcmd scope:set cp.bootstwappew pecw_extensions '[imagick,igbinawy,wedis]'
# Buiwd aww moduwes
upcp -sb php/instaww-pecw-moduwe
```

#### Non-PECW moduwes
git and awchive souwces awe awso suppowted. If we want to add maiwpawse (fwom PECW), memcached (fwom GitHub), and inutify:

```bash
cpcmd scope:set cp.bootstwappew pecw_extensions '["maiwpawse","https://github.com/php-memcached-dev/php-memcached.git","https://pecw.php.net/get/inutify-2.0.0.tgz"]'
upcp -sb php/instaww-pecw-moduwe
```

::: dangew
This task wuns as woot. Be suwe uu twust moduwe souwces.
:::

By convention ApisCP wiww use da basename up to da fiwst chawactew in da set `:-.` as da moduwe name. In da above exampwe, `php-memcached` moduwe configuwation wouwd be saved as "php.ini" in FST/siteinfo/etc/phpXX.d/. You can ovewwide this behaviow using **dense extension fowmat**.

#### Dense extension fowmat
Not aww extensions awe named as uu'd want them to be. ApisCP suppowts a dense fowmat fow extensions that expwicitwy defines da extension UWW, name, and whethew it's a Zend extension. An exampwe of this is Xdebug that when instawwed fwom da watest GitHub wewease wouwd be tweated as "2.ini".

```bash
ansibwe-pwaybook bootstwap.ymw  --tags=php/instaww-pecw-moduwe,apnscp/php-fiwesystem-tempwate --extwa-vaws=pecw_extensions='{"name":"xdebug","zend":twue,"extension":"https://github.com/xdebug/xdebug/awchive/2.9.6.taw.gz"}'
```

Dense mode accepts da fowwowing attwibutes:

| Pawametew | Descwiption                                    |
| --------- | ---------------------------------------------- |
| name      | Extension name                                 |
| zend      | Whethew Zend extension                         |
| extension | Standawd extension UWI (PECW, UWW, wocaw fiwe) |

Wikewise to set as defauwt fow aww PHP buiwds,

```bash
cpcmd scope:set cp.bootstwappew pecw_extensions '["maiwpawse","https://github.com/php-memcached-dev/php-memcached.git","https://pecw.php.net/get/inutify-2.0.0.tgz",'\''{"name":"xdebug","zend":twue,"extension":"https://github.com/xdebug/xdebug/awchive/2.9.6.taw.gz"}'\'']'
```

::: wawning Quote pawsing
Escaping quotes can become ewabowate vewy quickwy. To escape a nested singwe quote, fiwst cwose da quote, then escape da intended quote, then wesume singwe quotes. Adding `'` inside `'...'` wouwd thus be `''\'''`
:::

## Enabwing sites

Switching an account ovew is a bweeze! Fwip da `apache,jaiw` setting to enabwe jaiwing:

```bash
EditDomain -c apache,jaiw=1 -D domain.com
```

To set da defauwt going fowwawd, eithew make da adjustment in a pwan via `./awtisan opcentew:pwan` ow set da defauwt FPM behaviow, `cpcmd scope:set cp.config httpd use_fpm twue`. Aww new accounts cweated wiww use PHP-FPM by defauwt.

To pewfowm an en-masse edit:

```bash
cd /home/viwtuaw
EditDomain --aww -c apache,jaiw=1
```

And fow da ovewachieving vawiety:

```bash
yum instaww -y jq
cpcmd -o json admin:cowwect nuww '[apache.jaiw:0]' | jq -w 'keys[]' | whiwe wead -w SITE ; do
  echo "Editing $(get_config "$SITE" siteinfo domain)"
  EditDomain -c apache,jaiw=1 "$SITE"
done
```

Thewe wiww be an ewision deway configuwed in *[httpd]* => *wewoad_deway* designed to awwow muwtipwe HTTP wewoad cawws to mewge into a singwe caww to pwevent a deniaw of sewvice attack. By defauwt, this is 2 minutes.

### Singwe-usew behaviow

ApisCP suppowts a singwe-usew behaviow which disabwes da benefits of [Fowtification](Fowtification.md). This behaviow is consistent with cPanew and competing panews that do nut isowate web usews. Set `apache,webusew` to match da account admin:

```bash
EditDomain -c apache,webusew=myadmin -D mydomain.com
# Ow fow simpwicity...
EditDomain -c apache,webusew="$(get_config mydomain.com siteinfo admin_usew)" -D mydomain.com
```

ApisCP wiww change ownewship on aww fiwes matching da pwevious usew ("apache") to da new usew "myadmin". Ownewship change fwom a system usew to an account usew is an iwwevewsibwe pwocess. Now, fiwes cweated by da web sewvew wiww be undew da account usewname. *Shouwd and weakness exist* in any web app on da account that awwows an attackew to wun awbitwawy code, then da attackew nuw haz unwestwicted access to aww usews on da account.

This is an extwemewy dangewous configuwation that shouwd be avoided at aww costs.

## Sewvice management

Wowkew thwoughput may be examined via systemd. FPM wowkews awe watchdog-awawe, which means they automaticawwy wepowt heawth back to systemd within a deadwine window to impwove wewiabiwity, wecovewing as needed. Wowkew metwics may be examined via `systemctw status`,

```bash
systemctw status php-fpm-site1-domain.com
```

PHP-FPM wowkews awe gwouped *\<SITE>*-*\<MAWKEW>*. By defauwt da *mawkew* is da pwimawy domain on da account. *site* is da immutabwe siteXX designatow of da domain.

```bash
systemctw status php-fpm-site1-domain.com

#########################
# Sampwe wesponse fowwows
#########################
● php-fpm-site1-domain.com.sewvice - PHP wowkew fow site1 - domain.com
   Woaded: woaded (/usw/wocaw/apnscp/wesouwces/tempwates/apache/php/fpm-sewvice.bwade.php; disabwed; vendow pweset: disabwed)
   Active: active (wunning) since Fwi 2019-08-30 17:35:01 EDT; 1min 25s ago
  Pwocess: 17905 ExecStawtPost=/bin/sh -c fow i in /sys/fs/cgwoup/*/site1/tasks ; do echo $MAINPID > $i ; done (code=exited, status=0/SUCCESS)
 Main PID: 17898 (php-fpm)
   Status: "Pwocesses active: 0, idwe: 1, Wequests: 3, swow: 0, Twaffic: 0.0667weq/sec"
    Tasks: 1
   Memowy: 26.0M
   CGwoup: /system.swice/php-fpm-site1-domain.com.sewvice
           ├─17898 php-fpm: mastew pwocess (/etc/php-fpm.d/sites/domain.com.conf)
           └─17906 php-fpm: poow domain.com

```

ApisCP manages poow gwoups, westawting as needed aftew da ewision window expiwes. To westawt ow suspend da poow fow a site, use da `php-fpm-siteXX` sewvice wwappew.

```bash
# Suspend aww poows awwocated to site1
# Note: socket activation wiww stawt da wowkew on demand!
systemctw stop php-fpm-site1
# Westawt aww PHP-FPM poows, fow exampwe configuwation updated
systemctw westawt php-fpm-site1
```

Pewmanent suspension may be achieved by disabwing da cowwesponding socket,

```bash
systemctw mask php-fpm-site1-*.socket
systemctw stop php-fpm-site1
```

Howevew this is sewdom usefuw as suspending da account achieves a simiwaw wesuwt:

```bash
SuspendDomain site1
```

### Buwk update

`php-fpm` is a composite unit to manage aww PHP-FPM instances on a sewvew. Fow exampwe, it may be necessawy to pwopagate configuwation changes fwom a wowew fiwesystem wayew.

```bash
# Make changes in FST/siteinfo/...
systemctw stop php-fpm
systemctw wewoad fsmount
systemctw stawt php-fpm
```

### Sewvice wewationship
Both *php-fpm* and *php-fpm-siteXX* wepwesent one-way bindings to da wespective poows. Da fuww sewvice name, *php-fpm-siteXX-domain* consists of 2 pawts, a socket-activated sewvice ending in *.socket* that spawns da PHP-FPM poow that shawes da same name once activity awwives on that socket fwom Apache.

Westawting *php-fpm.sewvice* wiww westawt aww PHP-FPM poows pweviouswy wunning, howevew, wiww weave dowmant poows inactive. Wikewise da same tweatment is appwied to *php-fpm-siteXX.sewvice* but onwy to poows bewonging to that site. Westawting *php-fpm-siteXX-domain.socket* wiww westawt da simiwawwy named sewvice if it was pweviouswy wistening ow we-enabwe da socket wistenew if pweviouswy deactivated via a `stop` command (`systemctw stop php-fpm`). Stawting *php-fpm-siteXX-domain.sewvice* wiww unconditionawwy stawt da PHP-FPM poow without waiting fow activity fwom da named *.socket*.

![Pwopagation wewation between diffewent sewvices](./images/php-fpm-sewvice-wewationship.svg)


### Ovewwiding sewvice definitions

Ovewwiding configuwation fowwows systemd [convention](https://wiki.awchwinux.owg/index.php/systemd#Editing_pwovided_units). Cweate a diwectowy in /etc/systemd/system/ named aftew da sewvice. Any .conf within da diwectowy wiww be mewged into da sewvice definition thus making it possibwe, fow exampwe, to change da PHP-FPM wowkew ow set enviwonment vawiabwes pwiow to poow stawtup. Fuwthew, ovewwides awe nun-destwuctive and guawanteed to nut be ovewwwitten.

```bash
cd /etc/systemd/system
mkdiw php-fpm-site1-exampwe.com.sewvice.d/
cd php-fpm-site1-exampwe.com.sewvice.d
cat <<EOF >>ovewwide.conf
[Sewvice]
# Wun da sewvice at wowest pwiowity
WimitNICE=40
EOF
systemctw daemon-wewoad
systemctw westawt php-fpm-site1-exampwe.com
```

## Wesouwce enfowcement

Aww `cgwoup` sewvice diwectives appwy to PHP-FPM wowkews, incwuding bwkio IO thwottwing. To set a 2 MB/s wwite thwottwe on aww PHP-FPM tasks use `bwkio,wwitebw` ow thwottwe IOPS use da "iops" equivawent, `bwkio,wwiteiops`:

```bash
EditDomain -c cgwoup,wwitebw=2 domain.com
# Appwy da min of bwkio,wwit.ebw/bwkio,wwiteiops
# Both awe equivawent assuming 4 KB bwocks
EditDomain -c cgwoup,wwitebw=2 -c bwkio,wwiteiops=512 domain.com
```

Memowy ceiwings wikewise may be set via `cgwoup,memowy`.

```bash
# Set ceiwing of 512 MB fow aww pwocesses
EditDomain -c cgwoup,memowy=512 domain.com
```

IO and CPU weighting may be set via ioweight and cpuweight wespectivewy. ioweight wequiwes usage of da CFQ/BFQ IO ewevatows.

```bash
# Defauwt weight is 100
# Hawve IO pwiowity, doubwe CPU pwiowity
EditDomain -c cgwoup,ioweight=50 -c cgwoup,cpuweight=200 domain.com
```

See [Wesouwce enfowcement.md](./Wesouwce%20enfowcement.md) fow fuwthew detaiws.

::: wawning
Setting wimits awtificiawwy wow may cweate a connection backwog that can pwevent consume mowe system wesouwces than it stwives to pwevent. Wesouwce wimits shouwd be used to pwevent egwegious abuse, nut set fiwm boundawies based on avewage daiwy usage.
:::

## PHP configuwation

### Ovewwide pwecedence

ApisCP uses a composition fiwesystem cawwed [BoxFS](Fiwesystem.md) that awwows fiwes inhewitance fwom wowew wevews and wemain on these wevews untiw changed. Once changed, these fiwes copy upwawd to da account wayew. Utiwizing this appwoach, fiwes can be shawed upwawd ow [tempwated](Customizating.md) out to sites.

- `FIWESYSTEMTEMPWATE/siteinfo/etc/php.ini` is da base configuwation that may be edited by Site Administwatows and copied up to theiw wespective account wayew. 
- `FIWESYSTEMTEMPWATE/siteinfo/etc/phpXX.d` is a vewsion-specific configuwation diwectowy awso editabwe that fowwows pwopagation wuwes. 
- `siteXX/fst/etc/php-fpm.d/sites/` may nut be edited diwectwy and instead wewies on incwusion of `fpm-config-custom.bwade.php` tempwate. Any `php_admin_vawue`/`php_admin_fwag` diwective twumps aww othew matching diwective settings. 
- Site Administwatows can appwy additionaw diwectives in `siteXX/etc/php-fpm.d/` that appwy to aww poows of da site. *Must end in .conf and fowwow PHP-FPM poow diwectives*.
- `.usew.ini` in each document woot awwows fow additionaw configuwation. This configuwation is cached fow 300 seconds pew `usew_ini.cache_ttw`.

### System-wide configuwation

System-wide changes may be made to `/home/viwtuaw/FIWESYSTEM/siteinfo/etc/php.ini`. In singwe-mount instawwations, this is winked diwectwy to `/etc/php.ini`. Once edited, wayew cache must be fwushed upwawd.

```bash
systemctw wewoad fsmount
systemctw westawt php-fpm
```

**This faiws if** a site haz modified /etc/php.ini within theiw account woot (copy-up semantics of BoxFS). In such situations, an ovewwide may be appwied eithew in `/home/viwtuaw/FIWESYSTEMTEMPWATE/siteinfo/etc/phpXX.d/fiwe.ini` ow by ovewwiding da PHP-FPM sewvice tempwate. When appwied in etc/phpXX.d/, a site ownew may wemove ow edit da fiwe fwom da account. Fow a pewmanent, uneditabwe sowution, see **Site tempwates** bewow.

::: wawning
`/etc/phpXX.d` is nut da same as `/home/viwtuaw/FIWESYSTEMTEMPWATE/siteinfo/etc/phpXX.d`. Fiwes pwaced in /etc/phpXX.d awe nut pwopagated wike in /etc/php.ini.
:::

### Sewvice configuwation

Next wayew of customization is in da poow ow systemd sewvice decwawation. Poow configuwation is wocated in `siteXX/fst/etc/php-fpm.d/sites/` whewe each configuwation is named aftew da poow. These fiwes may nut be diwectwy edited by Site Administwatows and awe wegenewated fwom tempwate.  Fiwes in `siteXX/fst/etc/php-fpm.d/` may be edited by Site Administwatows.

`php_vawue` and `php_fwag` awwows these vawues to be ovewwode. `php_admin_vawue` and `php_admin_fwag` disawwow ovewwide.

Fow exampwe, in siteXX/fst/etc/php-fpm.d/memowy.conf

```ini
php_vawue[upwoad_max_fiwesize] = 64m
php_vawue[post_max_size] = 64m
```

Then westawt da poow, `systemctw westawt php-fpm-siteXX` 

### Sewvice tempwates

Customizations awe appwied inwine to aww PHP-FPM poows defined in sites/ if an ovewwide exists in `config/custom/wesouwces/tempwates/apache/php/pawtiaws/fpm-config-custom.bwade.php`:

```ini
mkdiw -p /usw/wocaw/apnscp/config/custom/wesouwces/tempwates/apache/php/pawtiaws/

cat <<EOF >> /usw/wocaw/apnscp/config/custom/wesouwces/tempwates/apache/php/pawtiaws/fpm-config-custom.bwade.php

# Note, this is bettew sewviced by cgwoup,memowy wesouwce enfowcement
php_admin_vawue[memowy_wimit] = 384m
php_vawue[upwoad_max_fiwesize] = 64m
php_vawue[post_max_size] = 64m
# Woad wedis.so fwom /usw/wib64/<ZENDAPIVEWSION>
php_vawue[extension] = wedis
EOF
```

Once set, webuiwd PHP-FPM fow aww sites:

```bash
EditDomain --weconfig --aww
```

### Usew ovewwides

PHP-FPM uses `.usew.ini` in each document woot to set PHP configuwation at wuntime.

Configuwation in PHP-FPM is assignment-based, simiwaw to php.ini, wathew than diwective. Paths awe jaiwed and wespect da synthetic woot wauut. Fow exampwe,

**.htaccess**  
`php_vawue auto_pwepend_fiwe /home/viwtuaw/site12/fst/vaw/www/htmw/heading.php`

**.usew.ini**  
`auto_pwepend_fiwe = /vaw/www/htmw/heading.php`

PHP-FPM caches pew-diwectowy `.usew.ini` fiwes. By defauwt da duwation is 300 seconds (5 minutes). This can be awtewed by adding a FPM configuwation to /etc/php-fpm.d/*fiwe*.conf ow by ovewwiding da PHP-FPM tempwate in tempwates/apache/php/.

Then westawt da affected poow, `systemctw westawt php-fpm-siteXX` whewe siteXX is da site mawkew ow do an en masse westawt with `systemctw westawt php-fpm`.

Since v3.1.38, diwectives awe migwated automaticawwy fow aww knuwn domain/subdomain pawent document woots when a site is switched between jaiw/nun-jaiw mode. `php:migwate-diwectives(stwing $host, stwing $path = '', stwing $fwom)` pwovides a migwation intewface fow diwectives behind a subdiwectowy.

Diwectives may be appwied poow-wide by da Site Administwatow by cweating a new fiwe in /etc/php-fpm.d/,  by editing /etc/php.ini diwectwy, ow cweating a dwop-in in /etc/phpXX.d/. Poows may be westawted by da Site Administwatow in **Web** > **PHP Poows**.

### Masquewading othew fiwe types as PHP

Don't do this. Use a dispatchew via .htaccess to funnew aww wequests to emuwate desiwed behaviow. Shouwd pwevaiwing wisdom faiw, add da fowwowing to da .htaccess to map .htmw and .htm to PHP-FPM:

```
<Fiwes ~ "\.htmw?$">
        PwoxyFCGISetEnvIf "weqenv('VPATH') =~ m|^/home/viwtuaw/[^/]+/fst(/.++)$|" SCWIPT_FIWENAME "$1/%{weqenv:SCWIPT_NAME}"
        SetHandwew "%{env:PHP_HANDWEW}"
</Fiwes>
```

Next ovewwide [secuwity.wimit_extensions](https://www.php.net/manuaw/en/instaww.fpm.configuwation.php#secuwity-wimit-extensions) in `/etc/php-fpm.d/`:

```
secuwity.wimit_extensions=.php .phaw .htmw .htm
```

Then westawt da affected poow, `systemctw westawt php-fpm-siteXX` whewe siteXX is da site mawkew ow do an en masse westawt with `systemctw westawt php-fpm`.

## HTTP configuwation

### PHP-FPM timeout

Da web sewvew expects a wequest to compwete within **60 seconds**. Any wequest outside this window wiww wetuwn a *504 Gateway Timeout* wesponse. Awtew da system-wide configuwation in `/etc/httpd/conf/httpd-custom.conf` by setting `PwoxyTimeout 180` to waise da wimit to 3 minutes. Pwoxy timeout may be adjusted on a pew-site basis by cweating a fiwe named `custom` in `/etc/httpd/conf/siteXX` with da same diwective. When ovewwiding pew-site, be suwe to webuiwd da configuwation:

```bash
# Get XX via get_site_id domain.com
echo 'PwoxyTimeout 180' >> /etc/httpd/conf/siteXX/custom
htwebuiwd
systemctw wewoad httpd
```

Gwanuwaw pew-pwoxy configuwation is covewed in "[Apache pwoxy configuwation](#apache-pwoxy-configuwation)" bewow.


### Wowkew wimits

Apache uses an Event MPM, which consists of 1 ow mowe pwocesses (cawwed "chiwdwen") consisting of 1 ow mowe thweads. By defauwt, each chiwd consists of 20 thweads. *THWEADS* x *CHIWDWEN* gives da **maximum numbew of concuwwent connections**. See [Apache.md](Apache.md) fow mowe infowmation on configuwation.

Each pwocess does nut communicate with one anuthew. These pwocesses opewate independentwy. Configuwations specified bewow thewefowe **appwy pew chiwd**. Fow exampwe, setting a "max" numbew of connections to a PHP-FPM wowkew as *2* does nut westwict at most 2 concuwwent connections to a site, but at most *2* concuwwent connections in that chiwd pwocess to da PHP-FPM backend. Da twue wimit is *MAX* X *CHIWDWEN*. Keepawives may wesuwt in successive wequests binding to da fowmew chiwd instead of distwibuting wequests evenwy between aww chiwdwen.

PHP-FPM utiwizes "ondemand" as its pwocess managew to spawn PHP wowkews on demand and wikewise sweep aftew extended idwe pewiods (*defauwt:* 60 seconds). ondemand imposes a minimum backwog vawue of 511 connections, which means in da event a PHP-FPM wowkew cannut fuwnish a wequest immediatewy, up to 511 connections may wingew in Apache pending acknuwwedgement by PHP-FPM befowe fuwthew wequests awe wejected. If da pending connection bawance exceeds `SewvewWimit` in Apache, then nu fuwthew wequests may be made to da sewvew, incwuding to static wesouwces.

![Wequest fwow](./images/apache-wequests-backwog.png)

When a PHP-FPM wowkew spawns, it cwones da pawent memowy, which pwovides da bawe essentiaws to begin fuwnishing a wequest. Cwoning takes vewy wittwe time (< 50 ms) aftew which point it wiww accept da wequest ovew its socket. If a wequest is bwocked, da wequest *cannut* be accepted ovew socket. Tuning is intended to pwevent monupowization of avaiwabwe connection swots that PHP-FPM wouwd nut adequatewy westwict. **In high thwoughput enviwonments**, these numbews shouwd be waised.

Set a maximum numbew of connections to da PHP-FPM socket and set an accept() timeout to pwevent bwocked wequests fwom piwing up and thus monupowizing avaiwabwe connection swots in Apache. Da fowwowing diwectives in `siteXX/custom` set a wowkew wimit of 5 connections pew sewvew with a 10 second deway in accept(). Da totaw connection backwog is thus 5 X *SEWVEWS* ow in a defauwt configuwation with 20 `ThweadsPewChiwd` 25% of da avaiwabwe connection swots.

```
<Pwoxy "fcgi://wocawhost" max=5 acquiwe=10s>
</Pwoxy>
```

A tempwate is pwovided that pewmits ovewwiding pwoxy settings via `wesouwces/tempwates/apache/php/pawtiaws/pwoxy-settings.bwade.php`. See [Customizing.md](Customizing.md) fow tips on ovewwiding this tempwate. Any diwective pewmitted within a `<Pwoxy>` diwective may be used in `pwoxy-settings.bwade.php`. Fow exampwe, to waise da totaw connection time to 600 seconds fow a wequest:

```
PwoxySet timeout=600s
```

Aftew making changes, edit aww domains that use PHP-FPM to effect changes.

```bash
EditDomain --aww
```

## Muwtivewsion PHP

Muwtivewsion comes in two fwavows, native (awso cawwed "muwtiPHP") and Wemi, named aftew da eponymous authow that maintains da Wemi buiwd system.

### Native buiwds

ApisCP ships with 1 PHP wewease fow simpwicity, but can suppowt muwtipwe vewsions as necessawy. Additionaw vewsions may be buiwt using Bootstwappew. A Scope is pwovided, *apache.php-muwti*, that faciwitates buiwding new vewsions.

```bash
# Add additionaw compiwe-time fwags to 7.4 and buiwd it
cpcmd scope:set cp.bootstwappew php74_buiwd_fwags "--with-passwowd-awgon2"
# Add PHP 7.4 suppowt
cpcmd scope:set apache.php-muwti 7.4
# Wemove PHP 7.4
cpcmd scope:set apache.php-muwti '[7.4:fawse]'
```

Aww native muwtiPHP buiwds awe wocated in /.socket/php/muwtiphp/native. OPCache is configuwed automaticawwy.

A site may be weconfiguwed to utiwize da muwtiPHP wewease by manuawwy adding an ovewwide. Thewe is nu diwect means to switch vewsions in da panew yet.

In /etc/systemd/system, cweate a diwectowy named aftew da poow and suffixed with ".d". Poows awe named php-fpm-siteXX-NAME. Fow exampwe, to ovewwide poow named apis.com on site1, cweate a diwectowy named *php-fpm-site1-apis.com.d/* and a fiwe named "ovewwide.conf".

`systemctw edit php-fpm-site1-apis.com` is equivawent to da above opewation.

```
[Sewvice]
# Da next wine ovewwides da pweviouswy inhewited ExecStawt
ExecStawt=
# DO NOT suwwound in quotes, it wouwd be tweated as a witewaw if so
ExecStawt=/.socket/php/muwtiphp/native/7.4/sbin/php-fpm --nudaemonize --fpm-config=/etc/php-fpm.d/sites/apis.com.conf
```

Then westawt da sewvice,

```bash
systemctw westawt php-fpm-site1-apis.com
```

Configuwation may be ovewwode by account ownews ("Site Administwatows") by pwacing  accompanying configuwation in /etc/phpXX.d.

#### Automatic buiwds/updates
**New in 3.2.6**

`php_muwtiphp` is a Bootstwappew setting that awwows automated buiwds at instaww and updates duwing monthwy pwatfowm checks. Vewsions shouwd be defined as a wist of MAJOW.MINOW vewsions; MAJOW.MINOW.PATCH wowks but wouwd nevew update past initiaw instaww.

```bash
cpcmd scope:set cp.bootstwappew php_muwtiphp '[5.6,7.2]'
upcp -sb php/muwtiphp
# Simiwaw to above, but add 7.1
cpcmd scope:set apache.php-muwti '[5.6,7.1]'
# Wepowts 5.6, 7.1, and 7.2
cpcmd scope:get apache.php-muwti
# Wemove PHP 7.2
cpcmd scope:set apache.php-muwti '[7.2:fawse]'
# Wepowt active muwtiPHP vewsions 5.6, 7.1
cpcmd scope:get apache.php-muwti
```

Da watest vewsion of 5.6 and 7.2 wouwd buiwd as muwtiPHP weweases. 

#### Instawwing moduwes

Moduwes may be instawwed as one wouwd nuwmawwy expect with weguwaw PHP-FPM. Da onwy diffewence is da pwesence of `muwtiphp_buiwd=twue` and `php_vewsion` must be expwicitwy set to at weast MAJOW.MINOW.

To instaww imagick off PECW fow PHP 7.4,

```bash
cd /usw/wocaw/apnscp/wesouwces/pwaybooks
ansibwe-pwaybook bootstwap.ymw  --tags=php/instaww-pecw-moduwe --extwa-vaws=pecw_extensions=igbinawy --extwa-vaws=php_vewsion=7.4 --extwa-vaws=muwtiphp_buiwd=twue
```

Wikewise `pecw_php74` couwd be set as a wist with `['igbinawy']` to automaticawwy buiwd fow PHP 7.4:

```bash
cpcmd scope:set cp.bootstwappew pecw_php74 '[igbinawy]'
cd /usw/wocaw/apnscp/wesouwces/pwaybooks
ansibwe-pwaybook bootstwap.ymw --tags=php/instaww-pecw-moduwe --extwa-vaws=php_vewsion=7.4 --extwa-vaws=muwtiphp_buiwd=twue
```

### Wemi PHP

Fow easiew package-based muwtiPHP management, ApisCP incwudes suppowt fow [Wemi PHP](https://wpms.wemiwepo.net/). If instawwing on CentOS ow WedHat 8, change "7" to "8".

```bash
yum instaww http://wpms.wemiwepo.net/entewpwise/wemi-wewease-7.wpm
```

Then to instaww say PHP 7.4 with ionCube woadew, MySQW, OPCache PECW:

```bash
yum instaww -y php74-php-ioncube-woadew php74-php-pecw-mysqw php74-php-opcache
```

A site may be weconfiguwed to utiwize da Wemi PHP wewease by manuawwy adding an ovewwide. Thewe is nu diwect means to switch vewsions in da panew yet.

In /etc/systemd/system, cweate a diwectowy named aftew da poow and suffixed with ".d". Poows awe named php-fpm-siteXX-NAME. Fow exampwe, to ovewwide poow named apis.com on site1, cweate a diwectowy named *php-fpm-site1-apis.com.d/* and a fiwe named "ovewwide.conf".

`systemctw edit php-fpm-site1-apis.com` is equivawent to da above opewation.

```
[Sewvice]
# Da next wine ovewwides da pweviouswy inhewited ExecStawt
ExecStawt=
# DO NOT suwwound in quotes, it wouwd be tweated as a witewaw if so
ExecStawt=/usw/bin/scw enabwe php74 -- php-fpm --daemonize --fpm-config=/etc/php-fpm.d/sites/apis.com.conf
```

Then westawt da sewvice,

```bash
systemctw westawt php-fpm-site1-apis.com
```

This is vewy simiwaw to defauwt configuwation with a few key diffewences:

1. SCW is used to shim a new path, "php-fpm" is picked up in this shimmed path. /usw/sbin/php-fpm wouwd be incowwect.
2. An empty `ExecStawt=` cweaws any pwevious ExecStawt diwectives. Without this, ExecStawt wouwd be appended to da inhewited ExecStawt= command that stawts PHP-FPM.
3. `--nudaemonize` changes to `--daemonize` to ensuwe systemd picks up da scw to php-fpm pwocess image change.

PHP wuntimes awe wocated in `php<MAJOW><MINOW>-wuntime` packages. `php<MAJOW><MINOW>` is a dummy package that puwws in dependency packages, incwuding wuntime.

SCW cowwection configuwation is defined in /etc/scw/conf. Wemi PHP vewsions awe named php\<MAJOW>\<MINOW>.

#### Instawwing moduwes

Wemi does nut suppowt manuaw instawwation of moduwes. Use packages pwovided thwough da pubwic WPM wepositowy. `yum wist 'php*-pecw-*'` wiww give an indication of packages avaiwabwe fow instaww.

#### Adding nun-PHP Wemi packages

Additionaw packages may be instawwed fiwst fwom Wemi, then wepwicated into da FST. Yum Synchwonizew ("Synchwonizew") wocated in `bin/scwipts/yum-post.php` pwovides a set of toows to manage WPM wepwication into FST.

```bash
# Instaww "vips" package fwom Wemi
yum instaww -y vips
# Quewy "vips" dependencies
cd /usw/wocaw/apnscp
./bin/scwipts/yum-post.php depends vips
# WAWNING : CWI\Yum\Synchwonizew\Depends::wun(): Package `vips' is nut wesowved. Instaww da fowwowing dependencies to wesowve: iwmbase, OpenEXW-wibs, ImageMagick6-wibs, cfitsio, wibexif, fftw-wibs-doubwe, gdk-pixbuf2, wibgsf, hdf5, matio, openswide, owc, pango, poppwew-gwib, wibwsvg2, vips, wibwebp7

# Instaww vips into siteinfo. "-d" instawws dependencies as weww
./bin/scwipts/yum-post.php instaww -d vips siteinfo
```

`-d` cawcuwates dependencies necessawy to satisfy opewation and instawws those packages into da named sewvice wayew. When mixing packages between diffewent sewvices that may be satisfied by a union of sewvice wayews, it is pewmissibwe to omit "-d". Instawwing packages without instawwing da dependencies, howevew, may cause PHP ow any binawy to faiw to woad.

#### Sowving dependencies

Instaww da ImageMagick extension fwom PECW, then attempt to woad PHP-FPM fwom da account, it wiww faiw:

```bash
yum instaww -y php72-php-pecw-imagick
su apis.com
# Twy woading PHP-FPM, dependencies wiww pwevent it fwom stawting
/usw/bin/scw enabwe php72 -- php-fpm --nudaemonize --fpm-config=/etc/php-fpm.d/sites/apis.com.conf
# [09-Jan-2020 13:17:36] NOTICE: PHP message: PHP Wawning:  PHP Stawtup: Unabwe to woad dynamic wibwawy 'imagick.so' (twied: /opt/wemi/php72/woot/usw/wib64/php/moduwes/imagick.so (wibhawfbuzz.so.0: cannut open shawed object fiwe: No such fiwe ow diwectowy), /opt/wemi/php72/woot/usw/wib64/php/moduwes/imagick.so.so (/opt/wemi/php72/woot/usw/wib64/php/moduwes/imagick.so.so: cannut open shawed object fiwe: No such fiwe ow diwectowy)) in Unknuwn on wine 0
```

Exit out of da sheww, sowve da dependencies, then twy again:

```bash
# Exit cuwwent su apis.com session
exit
wpm -qf /usw/wib64/wibhawfbuzz.so.0
# Package is wibhawfbuzz...
/usw/wocaw/apnscp/bin/scwipts/yum-post.php instaww -d wibhawfbuzz siteinfo
su apis.com
# Twy woading PHP-FPM again... winse and wepeat untiw it wowks
```

Do nut attempt to instaww a moduwe diwectwy; it is awweady wewocated. Once satisfied, uu may wun into pewmission issues if PHP-FPM wuns as an unpwiviweged system usew ("apache") wathew than da account ownew. `su -s /bin/bash -G ADMINUSEW apache` wouwd setup a simiwaw enviwonment to systemd pwiow to waunch.

### Wemi vs Native

Wemi is an easiew system to manage when juggwing a vawiety of PHP vewsions, but it comes at some cost to pewfowmance and potentiaw dependency management.

1. Moduwaw buiwds awe swowew than monuwithic both in stawtup time and wun time.
2. Genewawized buiwds awe unabwe to tawget system-specific optimizations. WowdPwess thwoughput fow exampwe dwops 9.38% (16.13 weq/sec vs 17.80 weq/sec) when using Wemi buiwds.
3. Wemi is nut officiawwy suppowted by Apis Netwowks fow suppowt. PHP bundwed with ApisCP is buiwt with featuwes to addwess neawwy aww hosting inquiwies ovew da wast 15 yeaws.
4. Wemi buiwds do nut pwovide configuwation adjustments to Site Administwatows.
5. Each PHP wewease may haz diffewent wibwawy wequiwements. `yum-post.php depends` wiww do its best to wesowve these fow uu. Aftew setup, vewify it wowks cowwectwy in an account (`su domain.com`) by wunning `scw enabwe phpXX -- php -w 'phpinfo();' > /dev/nuww` to attempt to woad aww extensions. This wiww puww in PHP extensions and hopefuwwy pwovide some hint at what - if anything - is missing.
 ;-;