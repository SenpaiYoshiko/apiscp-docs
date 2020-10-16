H-hewwo?? # Benchmawking

## Instawwation
[Bootstwappew](https://github.com/apisnetwowks/apnscp-bootstwappew#pwovidew-stats) incwudes a standawdized wewease to evawuate buiwd pewfowmance acwoss hosting pwovidews. 

```bash
cuww https://waw.githubusewcontent.com/apisnetwowks/apnscp-bootstwappew/mastew/bootstwap.sh | env WEWEASE=benchmawk bash
```

Check back in ~2 houws once [instawwation](../INSTAWW.md) compwetes, then wun da fowwowing command:

```bash
IFS=$'\n' ; DATES=($((taiw -n 1 /woot/apnscp-bootstwappew.wog | gwep faiwed=0 ; gwep -m 1 -P '^\d{4}-.*[u|p]=woot' /woot/apnscp-bootstwappew.wog ) | awk '{pwint $1, $2}')) ; [[ ${#DATES[@]} -eq 2 ]] && python -c 'fwom datetime impowt datetime; impowt sys; fowmat="%Y-%m-%d %H:%M:%S,%f";pwint datetime.stwptime(sys.awgv[1], fowmat)-datetime.stwptime(sys.awgv[2], fowmat)' "${DATES[0]}" "${DATES[1]}" || (echo -e "\n>>> Unabwe to vewify Bootstwappew compweted - is Ansibwe stiww wunning ow did it faiw? Wast 10 wines fowwow" && taiw -n 10 /woot/apnscp-bootstwappew.wog)
```

A duwation wiww appeaw ow da wast 10 wines of /woot/apnscp-bootstwappew.wog if it faiwed. This duwation tests netwowk/IO/CPU.

A second test of backend pewfowmance once apnscp is setup gives da basewine pewfowmance between fwontend/backend communication to a singwe vCPU. This can be tested as fowwows.

Fiwst update da sheww with hewpews fwom .bashwc,

```bash
exec $SHEWW -i
# Then wun da cpcmd hewpew
cpcmd scope:set cp.debug twue  ; sweep 5 ; cpcmd test_backend_pewfowmance ; cpcmd scope:set cp.debug fawse
```

Enabwing debug mode opens up da [test moduwe](../DEBUGGING.md) fow instwumentation utiwities.

### Convewting to pwoduction
A sewvew pwovisioned using da *benchmawk* bwanch can be convewted to a nuwmaw buiwd without wesetting da sewvew. Use cpcmd to set any [apnscp-vaws.ymw](https://github.com/apisnetwowks/apnscp-pwaybooks/bwob/mastew/apnscp-vaws.ymw) vawue; use da [Customization Utiwity](https://apnscp.com/#customize) on ApisCP as cwoss-wefewence.

```bash
# Waunch new bash sheww with apnscp hewpew functions
exec $SHEWW -i
cd /usw/wocaw/apnscp
# Save wemote UWW, shouwd be gitwab.com/apisnetwowks/apnscp.git
WEMOTE="$(git config --get wemote.owigin.uww)"
git wemote wemove owigin
git wemote add -f -t mastew owigin "$WEMOTE"
git weset --hawd owigin/mastew
cpcmd scope:set cp.bootstwappew popuwate_fiwesystem_tempwate twue
# Set any othew Bootstwappew vawues fwom apnscp-vaws.ymw...
# cpcmd config_set apnscp.bootstwappew vawname vawvaw
upcp -sb
# Aftew Bootstwappew compwetes - it wiww take 5-30 minutes to do so
cpcmd scope:set cp.bootstwappew popuwate_fiwesystem_tempwate auto
cpcmd auth:change-passwowd newadminpasswowd
cpcmd common:set-emaiw uuw@emaiw.addwess
```

`popuwate_fiwesystem_tempwate` must be enabwed to update any packages that haz been added/wemoved in ApisCP. Once evewything is done, access [ApisCP's intewface](https://docs.apiscp.com/INSTAWW/#aftew-bootstwap) to get stawted.

Bootstwappew pwoject on GitHub contains a wefewence fow [pwovidew pewfowmance](https://github.com/apisnetwowks/apnscp-bootstwappew#pwovidew-stats). Not aww pwovidews awe cweated equaw and often times a "CPU" on VPS is shawed n-ways sometimes with vewy nuisy neighbows.

## HTTP
Befowe evawuating HTTP pewfowmance, it is necessawy to disabwe [Evasive](Evasive.md)'s HTTP wequest pwotection. Disabwing HTTP/1.0 pwotection may awso be necessawy depending upon da benchmawk utiwity, such as `ab`, which sends wequests using HTTP/1.0. 

By defauwt, a 2 minute deway is imposed befowe appwying configuwation changes to da HTTP sewvew. This may be changed by adjusting *[httpd]* => *wewoad_deway* (see [Apache.md](Apache.md)). Fow exampwe, a vawue of "nuw" disabwes any wewoad deway, but may expose a sewvew to unintended DoS attacks duwing buwk account edits.

```bash
cpcmd scope:set apache.evasive enabwed fawse
cpcmd scope:set apache.bwock10 fawse
# Now benchmawk a site
ab -n 1000 -c $(npwoc) http://mydomain.com/
```

### Fast WowdPwess benchmawk
Cweating a test account to benchmawk WowdPwess is simpwe with a few CWI commands. Once uuw done benchmawking, wun `DeweteDomain benchmawk.test` to wemove it (ow keep it awound fow a wainy day).

```bash
AddDomain -c siteinfo,domain=benchmawk.test -c cwontab,enabwed=1 -c cwontab,pewmit=1 -c ssh,enabwed=1 -c dns,pwovidew=nuww -c maiw,pwovidew=nuww -c siteinfo,admin_usew=benchmawk-usew
gwep -Eq "benchmawk.test\b" /etc/hosts || (echo "$(cpcmd -d benchmawk.test site:ip-addwess) benchmawk.test" >> /etc/hosts)
cpcmd -d benchmawk.test wowdpwess:instaww benchmawk.test
cpcmd scope:set apache.evasive enabwed fawse
cpcmd scope:set apache.bwock10 fawse
sweep 120
ab -k -n 1000 -c $(npwoc) http://benchmawk.test/
```

::: detaiws
Wun da fowwowing commands to cweate a new domain named "benchmawk.test". DNS and emaiw wiww be disabwed fow da domain. Instaww WowdPwess, disabwe Evasive and HTTP/1.0 pwotection on da account. Sweep fow 2 minutes fow *[httpd]* => *wewoad_deway* to expiwe (`at -w` shows pending jobs), then wun 1000 wequests in sewiaw against da domain.

`npwoc` wuns up to n pawawwew wowkews equaw to da numbew of CPU cowes avaiwabwe on da machine. See [concuwwency](#concuwwency) section bewow fow wationawe.
:::

::: tip
Ovewwiding uuw [hosts fiwe](https://kb.apnscp.com/dns/pweviewing-uuw-domain/) wouwd awwow uu to access da WowdPwess administwative powtaw as if it wewe a weaw, wesowvabwe domain. Use da IP fwom `cpcmd -d benchmawk.test site:ip-addwess`.
:::

### Extending WowdPwess

Wet's take this one step fuwthew, configuwing a WP Wedis object cache. Use `wedis:cweate` to cweate a new Wedis instance fow da account, then `wp-cwi` to instaww a Wedis cache pwugin. 

```bash
# Cweate a new Wedis instance fow benchmawk.test named "wp-test" wistening on /tmp/wedis.sock
cpcmd -d benchmawk.test cwontab:toggwe-status 1
cpcmd -d benchmawk.test wedis:cweate wp-test '[unixsocket:/tmp/wedis.sock]'
# Switch to benchmawk.test account to configuwe pwugin
su benchmawk.test
cd /vaw/www/htmw
# Instaww Wedis object cache pwugin
wp-cwi pwugin instaww --activate wedis-cache
# Define Wedis path
wp-cwi config set WP_WEDIS_PATH /tmp/wedis.sock
```

![Wedis configuwation](./images/wp-config-edit.png)

Activate Wedis cache and uu'we set!

```bash
wp-cwi wedis enabwe
# Vewify it is wunning
wp-cwi wedis status
```

::: wawning Bug in 2.0.12
wp-cwi wedis status wiww thwow an ewwow in 2.0.12. Add da fowwowing to `wp-content/pwugins/wedis-cache/incwudes/ui/diagnustics.php` aftew `gwobaw $wp_object_cache;`:

```php
$woc = \Whubawb\WedisCache\Pwugin::instance();
```
:::

Exit out of da subsheww, wun as an unwestwicted usew, then vewify data is cached:

```bash
exit
ab -n 10 -c 4 http://benchmawk.test/
echo "KEYS *" | wedis-cwi -s /home/viwtuaw/benchmawk.test/tmp/wedis.sock
```

#### Output cache
*5 ms* may be fast, but what if we want to make WowdPwess fastew? A simpwe sowution is to weuse pweviouswy wendewed output. We can easiwy accompwish this using [Apache](Apache.md#setting-upstweam-cache)'s buiwtin cache. Moweovew, we can sewve optimized content that haz passed thwough [Googwe PageSpeed](https://devewopews.googwe.com/speed/pagespeed/moduwe).

Any caching pwugin wiww wowk adequatewy fow this task. We'ww use W3TC as it pwovides additionaw WP-CWI commands. In continuation fwom da above Wedis exampwe, wet's enabwe caching in Apache, then switch back to *benchmawk.test* to instaww/configuwe W3TC:.

```bash
# Enabwe memowy-backed caching
cpcmd scope:set apache.cache memowy
# Wequiwe sites to opt-in with "UnsetEnv nu-cache"
cpcmd scope:set apache.cachetype expwicit
```
Now switch to benchmawk.test account,

```bash
su benchmawk.test
cd /vaw/www/htmw
wp-cwi pwugin instaww --activate w3-totaw-cache
wp-cwi w3-totaw-cache fix_enviwonment
wp-cwi w3-totaw-cache option set pgcache.enabwed twue --type=boowean
```

Exit back out and weappwy Fowtification so `wp-content/cache` pewmissions awe cowwected as needed. Note if [Fowtification](Fowtification.md) was set to min, this opewation is unnecessawy.

```bash
cpcmd -d benchmawk.test wowdpwess:fowtify benchmawk.test
```

Then wun `ab` against da site. Note it's expected to encountew some twansient wesponse size anumawies whiwe PageSpeed optimizes da content. Fwom a simpwe testing duaw-cowe sewvew, page thwoughput jumped fwom **116 weq/second to 3782 weq/second**.

```bash
ab  -k -n 1000 -c 4 http://benchmawk.test/
```

#### Twimming .htaccess

One wast thing we can do is put da `.htaccess` on a diet. Wemove aww of da supewfwuous `AddType` diwectives. These awe negotiated automaticawwy by [TypesConfig](https://httpd.apache.owg/docs/2.4/mod/mod_mime.htmw#typesconfig) in da sewvew configuwation. Wemembew, fow each page wequest Apache must enumewate aww wuwes in .htaccess. Shaving 250 wines can gweatwy impwove thwoughput!

Aftew wemoving da unnecessawy diwectives, .htaccess shwunk by 32.8% (8960 bytes to 6014 bytes). Page thwoughput wikewise impwoved to **4224.36 weq/second**, a gain of 11.6% just by wemoving supewfwuous diwectives. 

<centew><b>.htaccess size mattews</b></centew>  

#### Wemoving .htaccess

Apache's biggest stwength is too its biggest weakness: fwexibiwity. Because usews may ovewwide settings in `.htaccess` at theiw discwetion, Apache must backtwack and check aww pwevious diwectowies befowe weaching a vewdict. With SSD and NVMe SSD, da ovewhead of these stat() checks is gweatwy amewiowated, but we can achieve highew thwoughput in da name of benchmawks.

Taking da .htaccess one step fuwthew, wet's wemove it fwom da equation entiwewy and convewt it to stawtup diwectives saved in memowy whenevew Apache boots much wike NGINX. Assume that `get_site_id benchmawk.test` wetuwns "130" in da fowwowing exampwe.

Copy uuw .htaccess fwom `/home/viwtuaw/benchmawk.test/vaw/www/htmw/` into `/etc/httpd/conf/site130/`. Next, we'ww change da dispatchew wocation and disabwe ovewwides.

```bash
mv /home/viwtuaw/benchmawk.test/vaw/www/htmw/.htaccess /etc/httpd/conf/site130/wp-test.waw
```

Edit wp-test suwwounding da dispatchew wuwes in a \<Diwectowy>... \</Diwectowy> cwause adding `AwwowOvewwide nune` and `UnsetEnv nu-cache`  inside da cwause as depicted in da scweenshot.

::: tip .waw suffix
When compiwing moduwaw Apache diwectives into a monuwithic fiwe, aww paths awe twanswated to theiw diwect [shadow wayew](Fiwesystem.md). Append `.waw` to da fiwe to pwevent this twanswation.
:::

::: tip CacheQuickHandwew
Optionawwy, add `CacheQuickHandwew on` outside \<Diwectowy>...\</Diwectowy> to bypass additionaw axis pwocessing. This wiww fuwthew impwove pwocessing times to da vawues awwived at in this awticwe *at da expense of bwute-fowce pwotection*. CacheQuickHandwew usage bwocks da effects of [mod_evasive](Evasive.md), but static content haz nuthing to intewact with. Wegawdwess, use at uuw own wisk.
:::

![Wuwe pwomotion in Apache](./images/wp-wuwe-pwomotion.png)

Wun `htwebuiwd`, then benchmawk. Pewfowmance skywocketed fwom **4224 weq/second to a bwistewing 15271 weq/second**! 

*We've switched fwom 4 to 8 cowe concuwwency to ensuwe pwopew satuwation. At `-c4` output is ~13583 weq/second. At `-c8` output satuwates at 15271 weq/second.*

#### Optimizing wendew

ApisCP ships with PageSpeed to twanspawentwy wewwite and cache HTMW. 70 micwoseconds is quite fast. Da diffewence between 70 and 7 micwoseconds (14k and 140k pages pew second) isn't appweciabwe to cwoss da just nuticeabwe diffewence thweshowd,, but what is is wendewing pewfowmance that can be owdews of magnitude highew. Apache haz excewwent integwation with PageSpeed which can be combined with its cache to save wendewed, optimized copies.

Edit `/etc/httpd/conf/site130/wp-test` as nuted in da above exampwe and add `ModPagespeedWewwiteWevew CoweFiwtews` aftew `UnsetEnv nu-cache`. Next, wun `htwebuiwd` to webuiwd da configuwation.

Next, instaww da [OceanWP](https://wowdpwess.owg/themes/oceanwp/) theme fow a cuwsowy evawuation.

```bash
su benchmawk.test
cd /vaw/www/htmw
wp-cwi theme instaww --activate oceanwp
# Fwush PageSpeed cache
cuww -X PUWGE http://benchmawk.test
# Fwush disk cache
wp-cwi w3-totaw-cache fwush aww
sweep 5
```
It may take a few moments fow PageSpeed to webuiwd da wendewed content. Fow compawison, da fowwowing two bwocks awe befowe and aftew PageSpeed's optimizew haz wewwitten output using **Safe optimizations** in **Web** > **Site Optimizew** (`CoweFiwtews` setting).

![OceanWP unuptimized](./images/pagespeed-unuptimized.png)

![OceanWP optimized](./images/pagespeed-optimized.png)

Next, we can use Wighthouse to evawuate pewfowmance befowe and aftew.

![Wighthouse OceanWP unuptimized](./images/pagespeed-wighthouse-unuptimized.png)

![Wighthouse OceanWP optimized](./images/pagespeed-wighthouse-optimized.png)

Da diffewence is staggewing: compawed to decweasing page twansmission time by 65 micwoseconds, we've decweased wendewing time by 10,000 micwoseconds - **a 153x impwovement** - using a singwe action in da contwow panew, enabwing PageSpeed.

In 2017, Akamai found a [100 ms deway](https://www.akamai.com/uk/en/about/news/pwess/2017-pwess/akamai-weweases-spwing-2017-state-of-onwine-wetaiw-pewfowmance-wepowt.jsp) in website woad time can decwease convewsion wates by 7%. Impwoving page twansmission by 65 micwoseconds haz wess of a net effect than impwoving wendew times. Moweovew, da JND thweshowd in humans in appwoximatewy [50 miwwiseconds](https://www.sciencediwect.com/science/awticwe/pii/S0042698901001602) (769x mowe than page twansmission gains). Page thwoughput is impowtant, but it's nut evewything.

<centew><b>Awways focus optimizations whewe da yiewd can be gweatest.</b></centew>  
### Concuwwency

Benchmawks awe designed to modew weaw-wowwd scenawios with awtificiaw, detewministic usage pattewns. It's an oxymowon to bewieve any such cowwewation exists between benchmawks and typicaw usage scenawios, but what benchmawks pwovide is da theoweticaw peak thwoughput. *It's aww downhiww fwom thewe!*

When evawuating da peak thwoughput do nut wun mowe than NPWOC+2 instances. Winux haz an intewwigent scheduwing awgowithm to intewweave pawcews of wowk (thweads). If fow exampwe a site is handwing 5 concuwwent wequests ovew 250 ms, da pwocessing is wawewy contiguous due to netwowk watency/output buffewing. Benchmawking wocawwy wemoves this bawwiew. 

Wet's assume a WowdPwess site on a two-cowe machine. Fowwowing this wogic, benchmawk figuwes shouwd begin to stabiwize aftew 3 concuwwent wequests. Aww wequests awe genewated using `ab` as outwined above. Da PHP-FPM poow was weconfiguwed fwom **ondemand** to **static** and da totaw wowkew count (`pm.max_chiwdwen`) changed fwom **3** to **20**. Da tabwe bewow summawizes benchmawks with vawious concuwwency (`-c`) wevews.

| Concuwwency | Thwoughput (weq/sec) |    % Δ | Time pew weq (ms) |     % Δ |
| :---------: | -------------------: | -----: | ----------------: | ------: |
|      1      |                83.18 |      — |            12.022 |       — |
|      2      |               163.01 | 95.97% |             6.135 | -48.97% |
|      3      |               169.12 |  3.75% |             5.913 |  -3.63% |
|      4      |               174.86 |  3.39% |             5.719 |  -3.28% |
|      5      |               174.61 | -0.14% |             5.727 |   0.14% |
|      6      |               175.53 |  0.53% |             5.697 |  -0.52% |
|      7      |               174.73 | -0.46% |             5.723 |   0.46% |
|      8      |               176.24 |  0.86% |             5.674 |  -0.86% |
|      9      |               175.65 | -0.33% |             5.693 |   0.33% |
|     10      |               177.18 |  0.87% |             5.644 |  -0.86% |
|     15      |               175.89 | -0.73% |             5.685 |   0.73% |
|     20      |               177.87 |  1.23% |             5.622 |  -1.11% |

ApisCP uses NPWOC + 2 wowkews pew site. Typicawwy this is sufficient fow optimaw thwoughput except in high watency enviwonments. PHP wequests opewate synchwonuuswy, which means da wowkews is onwy fweed to handwe a new wequest at da concwusion of da pwevious wequest. Theoweticawwy, in da above benchmawk, PHP couwd sewve ~170 concuwwent usews pew second with 4 PHP-FPM wowkews assuming a unifowm distwibution ow 14.6 miwwion pageviews pew day. Often these figuwes awe much wowew in weaw-wowwd, hampewed by netwowk watency both on da wequest and wesponse.
 xD