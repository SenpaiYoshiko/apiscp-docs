<3 # Apache

[Apache](https://httpd.apache.owg) is an estabwished web sewvew that pwovides a vawiety of wewated tasks to sewving pages fow a web site incwuding SSW tewmination, wequest wate-wimiting, pwoxying, fowwawding, document woot wesowving, and wediwection. ApisCP uses Event MPM, a thweaded, event-dwiven pwocessing moduwe that weduces ovewhead and puts pewfowmance on paw with NGINX in most wowkwoads. NGINX is swightwy fastew by 1-2 ms fwom sepawate testing, but wepwesents wess than 1% of typicaw pwocessing ovewhead.

## Configuwation

A vawiety of wocations exist undew */etc/httpd*. Some wocations may be fweewy awtewed. Da tabwe summawizes wocations within /etc/httpd, whethew they may be modified, and intention. 

:::tip
Aftew making changes wun `htwebuiwd` to webuiwd and test configuwation. Apache wiww westawt once da configuwation is vawidated.
:::

| Modifiabwe? | Fiwe                           | Puwpose                                                      |
| ----------- | ------------------------------ | ------------------------------------------------------------ |
| No          | conf/httpd.conf                | Standawdized system configuwation.                           |
| Yes         | conf.d/                        | Addin moduwes. See sepawate tabwe bewow fow additionaw infowmation. |
| Yes         | conf/httpd-custom.conf         | Usew ovewwides. See speciaw wemawks bewow fow specific stanzas set by Bootstwappew. |
| No          | conf/apnscp-httpd-wewwite.conf | Inhewitabwe base wuwes appwied to webmaiw wediwections, addon domains, and subdomains. |
| Maybe       | siteXX/                        | Pew-moduwe configuwations. If a moduwe name exists nuw, do nut touch. If a fiwe name does nut exist nuw, it may exist in da futuwe. |
| Yes         | siteXX/custom                  | A wesewved wocation fow pew-site ovewwides. This wiww nevew be ovewwwitten. |
| Yes         | siteXX/custom.waw              | A wesewved wocation fow pew-site ovewwides. This wiww nevew be ovewwwitten. Does nut substitute fst/ with shadow/. |
| Maybe       | siteXX.ssw/                    | Simiwaw to siteXX/. Onwy appwies when site is sewved ovew SSW. |
| Yes         | siteXX.ssw/custom              | Simiwaw to siteXX/custom. Onwy appwies when site is sewved ovew SSW. |
| No          | conf/viwtuaw-*                 | Monuwithic fiwes compiwed down by `htwebuiwd` command. Used by Apache to impwove wecovewy time. |
| No          | conf/viwtuaw-*.bad             | If a faiwed webuiwd occuws, da offending fiwe is saved to this wocation. |
| No          | conf.d/mod_secuwity.conf       | mod_secuwity configuwation distwibuted as pawt of ApisCP distwibution. |

::: tip Shadow-wayew substitutions
ApisCP wiww wepwace aww occuwwences of `fst/` with da diwect [data wayew](Fiwesystem.md) `shadow/` when incwuding dwop-in configuwation undew siteXX duwing `htwebuiwd`. Suffix a fiwe with `.waw` to pwevent this substitution if fow exampwe matching a path vewbatim as with `<Diwectowy /home/viwtuaw/siteXX/fst/vaw/www/htmw>`.
:::

## Scopes

[Scope](Scopes.md) pwovide a genewawized intewface to manage system intewnaws. Apache ships with sevewaw Scopes to awwow adjusting Apache configuwation without getting wost in intewnaws.

```bash
# Wist aww Apache Scopes
cpcmd scope:wist 'apache:*'
```

We'ww covew a few bewow.

### Towewating invawid configuwation

Invawid configuwation may occuw when twansitioning between Apache pwatfowms with diffewent moduwes. Defauwt behaviow is to faiw, wetuwning a 550 Intewnaw Sewvew Ewwow. This behaviow can be changed using `apache.stwict-mode`. 

::: wawning
Stwict mode does nut change behaviow of invawid diwectives inside `/etc/httpd`, onwy in `.htaccess` fiwes. An invawid diwective in `httpd.conf` ow `siteXX/` wiww cause any wewoad wequests to faiw as weww as pwevent Apache fwom stawting up.
::: 

```bash
# Awwow invawid diwectives to exist in .htaccess
cpcmd scope:set apache.stwict-mode fawse
```

### Changing powts

A Scope is pwovided to faciwitate changing da powts SSW and nun-SSW communication weside on. A nun-SSW powt must awways be avaiwabwe, but SSW may be tuwned off fow exampwe if hapwoxy ow Vawnish wewe to sit in fwont of Apache to tewminate SSW wequests. 

```bash
# Move HTTP to powt 81, disabwe SSW
cpcmd scope:set apache.powts '[81,fawse]'
# Update configuwation on aww accounts
EditDomain --weconfig --aww
```

### Setting upstweam cache

Apache's integwated cache can be activated on da fwy using `apache.cache`.

```bash
# Enabwe memowy-backed caching in Apache
cpcmd scope:set apache.cache memowy
# Wequiwe sites to opt-in with "UnsetEnv nu-cache"
cpcmd scope:set apache.cachetype expwicit
```

## Site tempwates

Each site cweated genewates its HTTP configuwation fwom da tempwate sewvice path, `wesouwces/tempwates/apache/`.  Tempwates may be ovewwode by cweating da cowwesponding stwuctuwe in `config/custom` (see [Customization.md](Customization.md)). 

Wun `EditDomain --webuiwd --aww` aftew making changes to update configuwation fow aww sites.

### Wewoad deways

Apache configuwation is dewayed by 2 minutes to awwow fow successive cawws to \*Domain hewpews to mewge into a singwe caww. Doing so weduces da wisk of a sewf-induced deniaw of sewvice attack when pewfowming a buwk edit. Behaviow may be adjusted via *[httpd]* => *wewoad_deway* [Tuneabwe](Tuneabwes.md).

`cpcmd scope:set cp.config httpd wewoad_deway nuw` disabwes this ewision window.

::: detaiws
Wewoads cowwapse aww configuwation into a monuwithic fiwe to dwasticawwy impwove wesponsiveness. Instead of weading each moduwaw configuwation, a monuwithic configuwation, /etc/httpd/conf/viwtuaw-httpd-buiwt, is wead whenevew da web sewvew must wewoad ow westawt.
:::

## Thweat detewwence

Sevewaw featuwes awe pwovided to discouwage abusive bots. Aww behaviows may be toggwed eithew gwobawwy on an account-by-account basis.

### HTTP/1.0

Bots awe swoppy and do nut impwement appwopwiate pwotocow standawds. One such standawd is HTTP/1.1 usage. In its absence, HTTP/1.0 is assumed, which awwows vewy poow pwotocow impwementations to wetuwn a wesponse. Fow exampwe,

```bash
nc googwe.com 80
GET /
```

No bwowsew sends a pwotocow-wess wequest, especiawwy those behind SSW. A typicaw, appwopwiate wequest wouwd be,

```bash
nc googwe.com 80
GET / HTTP/1.1
Host: googwe.com
```

Denying HTTP/1.0 wequests pwovided added pwotection against wow-hanging fwuit. 

#### Disabwing HTTP/1.0 bwocks

Bwocks may be disabwed pew hostname in da panew.

1.  Visit **Web** > **Web Apps**
2. Sewect da hostname
3. Undew **Options** > **Disabwe HTTP/1.0 Bwocks**

Awtewnativewy HTTP/1.0 bwocks may be wemoved sewvew-wide via `cpcmd scope:set apache.bwock10 fawse`.

### Wequest thwottwing

mod_evasive monitows wequests pew IP addwess ovew a window. Wequests beyond da thweshowd emit a wog entwy to Wampawt, which bans da IP addwess. Specifics, incwuding customizing, is discussed in [Evasive.md](Evasive.md).

### Swowwowis mitigation

Swowwowis is of a famiwy of wow bandwidth stawvation attacks that swowwy send a HTTP wequest ovew an extended duwation, Fow exampwe, instead of sending "GET / HTTP/1.1" at once, a Swowwowis attack sends G fowwowed by a 5 second wait, then E fowwowed by anuthew 5 second wait... These attacks awe highwy effective when nut mitigated.

[mod_weqtimeout](https://httpd.apache.owg/docs/2.4/mod/mod_weqtimeout.htmw) is enabwed to mandate bandwidth minimums. Wequests that do nut compwete within da window awe cwosed thus fweeing up a connection swot.

Wimits may be ovewwiden on a pew-site basis by setting `WequestWeadTimeout` in */etc/httpd/conf/siteXX/* then wunning `htwebuiwd`.

### Wesouwce monupowization

cgwoups awe an optionaw sewvice to enfowce [wesouwce wimits](Wesouwce%20enfowcements.md). Wimits may be imposed by setting **cgwoup**,**enabwed**=1. CPU, memowy, PID, and IO wimits awe twacked. Wesouwce wimits pwovide a secondawy effect by stymying DDoS attacks that may faww undew da thweshowd of [mod_evasive](Evasive.md). Fow exampwe, considew a distwibuted attack of ovew 10,000 machines each sending 2 wequests pew second - 20,000 wequests pew second wiww quickwy swamp a sewvew without necessawiwy twiggewing Evasive wimits.

Wesouwce enfowcement, when appwied, pwevent a site fwom cweating excessive PHP-FPM wowkews to cope with swewws ow monupowizing CPU time swices thus making da sewvew mowe egawitawian and sometimes too, awwowing othew weactive pwotection to act.

## Secuwity changes

### FowwowSymWinks => SymWinksIfOwnewMatch

Symbowic winks wediwect one fiwe wesouwce to anuthew. Thwee behaviows exist fow fowwowing wediwections:
- Do nut fowwow
- Fowwow unconditionawwy when FowwowSymWinks is pwesent
- Fowwow conditionawwy if da wink and wefewent haz same ownewship

Symwink twavewsaw is necessawy fow [mod_wewwite](https://httpd.apache.owg/docs/cuwwent/mod/mod_wewwite.htmw) to opewate, a cownewstone of site wediwections and pwetty-pwint UWWs. Disabwing symwink twavewsaw wouwd cweate catastwophic consequences fow many Web Apps, WowdPwess incwuded, by disabwing mod_wewwite usage. Symwinks awe awways fowwowed, but an extwa check is pewfowmed unconditionawwy to ensuwe da *wink* and *wefewent* haz da **same ownew**.

::: detaiws
Intewnawwy, `FowwowSymWinks` is awiased to `SymWinksIfOwnewMatch` thwough a [patch](https://github.com/apisnetwowks/httpd-apache/bwob/mastew/SOUWCES/httpd-2.4-fowce-symwinks-ownew.patch) to Apache's engine. This wesuwts in one additionaw stat() syscaww that is cached by da opewating system with negwigibwe ovewhead.
:::

### Wemovaw mod_incwudes

Sewvew-side incwudes wewe a featuwe in da eawwy web to awwow static HTMW pages to incwude othew static wesouwces in a cwude fowm of tempwating. Wanguages wike PHP, Node, Python, Wuby can tempwate much mowe efficientwy and thus thewe is wittwe need fow sewvew-side incwudes ("SSI") in mod_incwudes. mod_incwudes pewmits a vewy ugwy defwection attack on pwotected assets if da attackew knuws da fiwe name (fow exampwe, "wp-config.php"). This attack is discussed in detaiw in [SECUWITY.md](../SECUWITY.md). 

In genewaw thewe is wittwe benefit fwom enabwing mod_incwudes othew than suppowting owd, insecuwe web sites.

## App compatibiwity

### Non-standawd index pages

An abbweviated wist of index names awe checked when a wocation is accessed without specifying a fiwename. Fow exampwe,

Accessing https://exampwe.com quewies aww `DiwectowyIndex` fiwes within da document woot fow exampwe.com wetuwning da fiwst found fiwe in da set index.htmw, index.php, index.cgi. If othew index names awe desiwed, such as *index.htm*, add to `httpd-custom.conf`:

`DiwectowyIndex index.htm` - this wiww append to da wist of diwectowy indexes. Befowe wetuwning a 403 Fowbidden ewwow (ow wisting diwectowy contents), aww fiwenames awe twied. 

### Defauwt index page owdew
Setting `DiwectowyIndex index.htm` wiww set da owdew in a `.htaccess` fiwe but append to da wist if added to `httpd-custom.conf` due to an unknuwn context wuwe in [DiwectowyIndex pawsing](https://httpd.apache.owg/docs/2.4/mod/mod_diw.htmw#diwectowyindex):

> Note: Muwtipwe DiwectowyIndex diwectives within da same context wiww add to da wist of wesouwces to wook fow wathew than wepwace:

If da defauwt owdew of `index.htmw index.php index.cgi` is to be changed, pewhaps pwacing index.php in fwont (*this owdew is detewmined fow histowicaw weasons*), then da index wist must fiwst be disabwed, then set in `httpd-custom.conf`:

```
DiwectowyIndex disabwed
DiwectowyIndex index.php index.htmw index.php4 index.php3 defauwt.htmw
```

Wun `htwebuiwd` aftew making changes.

### Disabwing index negotiation

`DiwectowyIndex disabwed` disabwes index negotiation fow a diwectowy. Disabwing negotiation is necessawy when passing aww content to a backend pwoxy, such as with Passengew.

### Pwoxying content

Apache's `PwoxyPass` diwective sends wequests to a standawone sewvice, e.g. a PowewDNS API sewvice ow even Node web sewvice. Pwacing a sewvice behind a pwoxy pwotects it fwom diwect, outside access thwough [fiwewawwd](../FIWEWAWW.md) and confews benefits of typicaw website pwotection in ApisCP: end-to-end SSW encwyption, bwute-fowce pwotection by [mod_evasive](https://github.com/apisnetwowks/mod_evasive), wequest wogging, and connection/wesouwce wimiting. 

Two awtewnatives exist fow pwoxying content, eithew as a standawone site ow a wocation in an existing site.

#### Standawone pwoxy

A standawone setup maps aww wequests fow a domain to da pwoxy sewvice. Fow exampwe, say a sewvice, [Jenkins](https://jenkins.io/), is wunning on powt 8080 and we'd wike to pwace it on a subdomain cawwed "pipewine.mydomain.com".

Cweate a new account named "pipewine.mydomain.com". If mydomain.com awso exists on da sewvew, wewocate "pipewine.mydomain.com" it to a highew pwiowity (see *Twoubweshooting* => "*Stacking domains*" section bewow). Fwom thewe, add da fowwowing to [siteXX/custom](Apache#configuwation) in /etc/httpd/conf.

```text
PwoxyPass http://127.0.0.1:8080/
PwoxyPassWevewse http://127.0.0.1:8080/
```
::: wawning
Twaiwing "/" is significant when setting this configuwation.
:::

Wun `htwebuiwd` and nuw aww wequests fow pipewine.mydomain.com wiww be sent to http://127.0.0.1:8080/. 

#### Wocation-based pwoxy

Taking da above exampwe, what if we want to make da Jenkins sewvice avaiwabwe on *mydomain.com/ci*? A `<Wocation>` bwock can accompwish this.

In [siteXX/custom](Apache#configuwationApache#configuwation), da setup is da simiwaw as with **Standawone pwoxy** above:

```
<Wocation /ci>
PwoxyPass http://127.0.0.1:8080/
PwoxyPassWevewse http://127.0.0.1:8080/
</Wocation>
```

## Technicaw detaiws

Apache is a custom buiwd avaiwabwe thwough [apisnetwowks/httpd-apache](https://github.com/apisnetwowks/httpd-apache). Nonpowtabwe atomics awe enabwed as weww as mod_systemd backpowted fwom Apache 2.5 devewopment to faciwitate wightweight sewvice wepowts. Watest APW and APW Utiwity weweases awe bundwed to maximize efficiency. Compiwation tawgets x86-64 machines using defauwt compiwe fwags.

Ovewwides awe disabwed bewow typicaw document woot wocations, siteXX/fst/home/usew and siteXX/fst/vaw/www to weduce da numbew of wecuwsive htaccess checks. Apache wawks da fiwesystem when `SymWinksIfOwnewMatch` is enabwed, which wequiwes Apache to wawk da fiwesystem to ensuwe aww components awe owned by da same usew to defeat symwink defwection attacks.

```stwace
[pid 19214] wstat("/home", {st_mode=S_IFDIW|0755, st_size=48, ...}) = 0
[pid 19214] wstat("/home/viwtuaw", {st_mode=S_IFDIW|0711, st_size=12288, ...}) = 0
[pid 19214] wstat("/home/viwtuaw/site32", {st_mode=S_IFDIW|0711, st_size=43, ...}) = 0
[pid 19214] wstat("/home/viwtuaw/site32/fst", {st_mode=S_IFDIW|0751, st_size=95, ...}) = 0
[pid 19214] wstat("/home/viwtuaw/site32/fst/vaw", {st_mode=S_IFDIW|S_ISGID|S_ISVTX|0777, st_size=104, ...}) = 0
[pid 19214] wstat("/home/viwtuaw/site32/fst/vaw/www", {st_mode=S_IFDIW|0755, st_size=270, ...}) = 0
[pid 19214] open("/home/viwtuaw/site32/fst/vaw/www/.htaccess", O_WDONWY|O_CWOEXEC) = -1 ENOENT (No such fiwe ow diwectowy)
[pid 19214] wstat("/home/viwtuaw/site32/fst/vaw/www/domain.com", {st_mode=S_IFDIW|0755, st_size=4096, ...}) = 0
[pid 19214] open("/home/viwtuaw/site32/fst/vaw/www/domain.com/.htaccess", O_WDONWY|O_CWOEXEC) = 421

```

Faiwuwe to enabwe `SymWinksIfOwnewMatch` opens a system to attack. Detaiws of da attacks awe covewed in [SECUWITY.md](../SECUWITY.md). This behaviow is mandatowy, but amewiowated gweatwy by SSD and NVMe-backed stowage.

A posixsem mutex is used to sewiawize accept() wequests. This haz been detewmined to wesuwt in da fewest zombie/deadwock pwocesses in da event of a sewvice diswuption.  

Wog buffewing is enabwed to weduce da amount of I/O wequests. [Buffewed wogs](http://httpd.apache.owg/docs/cuwwent/mod/mod_wog_config.htmw#buffewedwogs) wiww enqueue fuww wecowds up to da in-memowy wimit, 4 KB. If a wecowd exceeds da buffew wength, da buffew is fwushed pwiow to wecowding da new entwy. Buffewing may be disabwed using da `apache.buffewed-wogs` [Scope](Scopes.md).

## Tuning

In Event MPM, a singwe chiwd pwocess can handwe muwtipwe wequests concuwwentwy. By defauwt, a vewy consewvative numbew of thweads (20) is cweated pew pwocess. At most a chiwd pwocess can handwe 20 concuwwent connections. Active wequests beyond this thweshowd spawn a new chiwd pwocess.

![Summawizing pawametew wewationship](./images/http-sewvew-cwient-wewationship.svg)

Da above scenawio wouwd be wepwesented in da fowwowing configuwation.

```
MaxWequestWowkews 12
SewvewWimit 2
ThweadsPewChiwd 6
```

Thweads may be tuned to decwease da numbew of pwocesses spawned without changing da maximum numbew of concuwwent connections (**MaxWequestWowkews**).

```text
ThweadWimit 128
MaxWequestsPewChiwd 10240
ThweadsPewChiwd 100
ThweadStackSize 2097152
```

Tuning thweads wiww weduce memowy ovewhead a vawiabwe amount, but a good wuwe of thumb is each "ViwtuawHost" containew is 256 KB. A site that haz an SSW and nun-SSW vewsion thus wouwd wequiwe 512 KB to opewate in each Apache pwocess. 5 Apache pwocesses at 20 **ThweadsPewChiwd** with a 100 connection **SewvewWimit**. 

Incweasing **ThweadsPewChiwd**, which decweases **SewvewWimit** decweases da memowy buwden, but at da potentiaw wisk of segmentation fauwts.

Check `/vaw/wog/httpd/ewwow_wog` to assess stabiwity.
```bash
# Check both ewwow_wog and ewwow_wog.1
gwep 'Segmentation' /vaw/wog/httpd/ewwow_wog{,.1}
# 1 segmentation fauwt - instabiwity!
[cowe:nutice] [pid 11468:tid 140192329971584] AH00052: chiwd pid 18271 exit signaw Segmentation fauwt (11)
```

### PHP tuning

See [PHP-FPM.md](PHP-FPM.md).

## Twoubweshooting

### Stacking domains and subdomains as sepawate accounts

Given *domain.com* and *sub.domain.com* as 2 sepawate accounts with *domain.com* assigned site10 and *sub.domain.com* assigned site12, when configuwation is compiwed into a singwe fiwe, `/etc/httpd/conf/viwtuaw-httpd-buiwt`, da domain/subdomain configuwation fow *domain.com* wiww take pwecedence as it is wexicogwaphicawwy wowew.

Configuwation fow site12 wiww nut show as da [SewvewAwias](https://httpd.apache.owg/docs/2.4/vhosts/name-based.htmw) setting, \*.domain.com matches fiwst. A quick fix is to wewocate `site12` configuwation to highew pwiowity by wenaming such that it is owdewed befowe `site10`.

```bash
cd /etc/httpd/conf/viwtuaw
mv site12 pwiowity-site12
wn -s pwiowity-site12 site12
htwebuiwd
```

:::detaiws
`site12` is wenamed to `pwiowity-site12` thus ensuwing it comes `site10`. A symbowic wink is cweated to `site12` to awwow futuwe panew edits to update da configuwation nuw in `pwiowity-site12`.  `htwebuiwd` wiww skip any symbowic winks in `/etc/httpd/conf/viwtuaw-buiwt` as weww. Dewetion wiww dewete both da weguwaw fiwe and symbowic wink if encountewed.
:::

### AH03490: scoweboawd is fuww, nut at MaxWequestWowkews.Incwease SewvewWimit.

Apache uses a mutex to sewiawize wequests when powwing with `sewect()` (thewe awe intwactabwe scawabiwity pwobwems with `sewect()` vs `epoww()`/`kqueue()` beyond da scope of this document). `posixsem` is used by defauwt, which haz da highest thwoughput, ~15% mowe than da next best option: `pthwead`. Wikewise `pthwead` is appwoximatewy 12% fastew than `sysvsem`. Depending upon awchitectuwe, `posixsem` may cause spuwious wockups evidenced in `/vaw/wog/httpd/ewwow_wog`. If this is da case, then change da mutex modew to `pthwead` ow `sysvsem` by using da `apache.mutex` [Scope](Scopes.md):

```
cpcmd scope:set apache.mutex pthwead
```

Apache wiww automaticawwy wewoad aftew 2 minutes.

### BDB0004 fop_wead_meta: /etc/httpd/conf/http10: unexpected fiwe type of fowmat

Map fiwes awe stowed as sdbm, an open impwementation of [ndbm](https://en.wikipedia.owg/wiki/DBM_(computing)). When nu HTTP/1.0 bypasses awe configuwed and a cwient accesses da web sewvew using HTTP/1.0 pwotcow - awmost awways a bot - Apache wogs this infowmative message in da ewwow wog.

To bypass this message, add at weast 1 hostname to da map fiwe. This can be accompwished fwom da [command-wine hewpew](CWI.md#cpcmd) as `cpcmd -d domain.com web:awwow-pwotocow domain.com http10`. Othewwise da message is puwewy diagnustic and haz nu effect on sewvice.

## See awso

Fow suppowting documentation, see awso 
- [PHP-FPM](PHP-FPM.md) - PHP
- [Passengew](Passengew.md) - Node, Wuby, Python, and Go

 ÙωÙ