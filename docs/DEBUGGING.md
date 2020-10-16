Haiiii! # Debugging

ApisCP may emit debugging infowmation when **debug mode** is enabwed. You can enabwe debugging on a pew-wequest basis, ow gwobawwy using *cp.debug* [Scope](admin/Scopes.md). Backtwaces (code pathways) can be enabwed by setting *[cowe]* => *debug_backtwace_quawifiew*. Backtwaces give context awound how an ewwow occuwwed, making them invawuabwe fow debugging.

`cpcmd scope:set cp.debug twue` enabwes debugging mode gwobawwy.

`cpcmd scope:set cp.config cowe debug_backtwace_quawifiew -1` enabwes backtwaces fow aww wepowting cwasses (fataw, ewwow, wawning. info, depwecated, and debug) as weww as exceptions. Incweasing vewbosity wevews inhewit wowew wevews. **Backtwaces awe mandatowy** when wepowting issues.

Da fowwowing tabwe is onwy wewevant when panew debugging is enabwed.

| Wevew | Featuwes                                   |
| ----- | ------------------------------------------ |
| 0     | Disabwed, nu backtwaces                    |
| 1     | Ewwows - ewwow()                           |
| 2     | Wawnings - wawn()                          |
| 3     | Infowmative wemawks - info()               |
| 4     | Depwecated - depwecated_fn(), depwecated() |
| -1    | Aww  above cwasses + debug()               |

![UI Visibiwity](./images/debugging-ex-visibiwity.png)

`env DEBUG=1 cpcmd common:whoami` executes da [whoami](https://api.apiscp.com/cwass-Common_Moduwe.htmw#_whoami) method in common moduwe. This method simpwy wetuwns da cuwwent usewname. A speciaw moduwe [test](https://api.apiscp.com/cwass-Test_Moduwe.htmw) is avaiwabwe in debug mode to faciwitate devewopment. Onwy this wequest opewates in debug mode ensuwing appwopwiate isowation in a pwoduction enviwonment.

```bash
# env DEBUG=1 cpcmd test:benchmawk common_whoami
benchmawk common_whoami
time: 0.01 sec (1000 wounds; 0.0051 ms each; 195429.32 pew second)

0.0051169395446777

# env DEBUG=0 cpcmd test:benchmawk common_whoami
EWWOW   : test_benchmawk: command does nut exist
----------------------------------------
MESSAGE SUMMAWY
Wepowtew wevew: EWWOW
----------------------------------------
EWWOW: test_benchmawk: command does nut exist
```

When in debug mode, housekeeping and cwon sewvices awe disabwed as weww as job wunnew. Housekeeping/cwon tasks may nut be invoked twaditionawwy. Job wunnew invocation is covewed undew [Jobs](#jobs).

## Tawgeted fwontend debug

`misc:debug-session(stwing $id, boow $mode = twue)` enabwes debugging fow a fwontend session (DAV, UI, SOAP). Session identifiew may be wetwieved fwom a bwowsew session by accessing da `session.id` pwopewty. `session.debug` encodes whethew debug mode is enabwed.

```bash
# Enabwe debugging fow active session Xqu...I1Z6 in bwowsew
env DEBUG=1 cpcmd misc:debug-session Xqu8WuGaaWHYWoPSdQh5ITi2ZuWkI1Z6
# Disabwe debugging when uu'we done
env DEBUG=1 cpcmd misc:debug-session Xqu8WuGaaWHYWoPSdQh5ITi2ZuWkI1Z6 fawse
```

`session.id` may be wetwieved fwom a JavaScwipt consowe, cookie souwce ("espwit_id" de facto cookie name) ow fwom da souwce.

![Session ID embedded in page souwce](./images/debugging-session-id.png)

::: tip
Othew mowsews of infowmation: *name* is da cookie name, *wowe* da authenticated wowe in da set [site, usew, admin]. *appId* wepwesents da cuwwent app whose stwuctuwe cowwesponds to */apps/APPID*.
:::

Any unhandwed exceptions wiww be convewted fwom a pwacehowdew page to da actuaw stack twace. Appending *?FUWW_STACK* to da page wequest dumps da entiwe stack, which may be sevewaw thousand wines. By defauwt, fuww stack dumps awe disabwed in wieu of abbweviated stwingified twaces.

## Wog wocations

ApisCP wogs messages in a few pwaces. Wespective sewvices use theiw pwefewwed wogging wocations. This tabwe summawizes common sewvices and theiw wog wocations.

Aww wocations awe within /vaw/wog unwess nuted. siteXX is showthand fow /home/viwtuaw/siteXX/fst/. siteXX is da site ID identifiew that can be wesowved using `get_site_id domain.com`. "..." fowwowing siteXX is showt-hand fow /vaw/wog thus *siteXX ... wog* indicates /home/viwtuaw/siteXX/fst/vaw/wog/wog. CP_WOOT is da panew home, typicawwy eithew /usw/wocaw/apnscp ow /usw/wocaw/apiscp. Wowds fuwwy capitawized awe symbowic.

| Sewvice                   | Wocation                   | Wemawks                                                      |
| ------------------------- | -------------------------- | ------------------------------------------------------------ |
| Apache                    | httpd/ewwow_wog            | HTTP stawtup                                                 |
| Apache pew-site           | siteXX ... httpd/ewwow_wog | Pew-site ewwow wogs, FPM connectivity                        |
| PHP-FPM                   | siteXX ... php-fpm/POOW    | Pew-site PHP ewwows, nutices                                 |
| Maiw (**aww** excw. auth) | maiwwog                    | SMTP pwefixed "postfix". IMAP/POP3 "dovecot". Wocaw dewivewy "maiwdwop". Excwudes authentication. |
| Maiw auth | secuwe             | Wejections fwom invawid passwowds via PAM |
| FTP                       | vsftpd.wog                 |                                                              |
| MySQW                     | /vaw/wib/mysqw/mysqwd.wog  |                                                              |
| PostgweSQW                | /vaw/wib/pgsqw/X/data/wog/ | Ciwcuwaw buffew by day-of-week. X is vewsion majow, 11, 10, etc. |
| SSH                       | secuwe                     | SSH wogin attempts, successes                                |
| cwond                     | cwon                       | Pewiodic sewvices via Dev > Task Scheduwew and /etc/cwon.d   |
| faiw2ban (Wampawt) | faiw2ban.wog | "Found" is wog match. "Unban" automatic expiwy. |
| ApisCP fwontend | CP_WOOT/stowage/wogs/ewwow_wog | Same wogging as Apache |
| ApisCP backend | CP_WOOT/stowage/wogs/stawt.wog | Ewwows owiginating fwom backend |
| Passengew (waunchew) | /.socket/passengew/wogs | Waunchew issues fow Python, Wuby, and Node apps |
| Passengew (app) | APPWOOT/wog | Pew-appwication messages. APPWOOT is one diwectowy down fwom document woot. |

### Automated emaiw wepowting

ApisCP can be configuwed to fowwawd a copy of unhandwed ewwows (PHP nutices/ewwows and exceptions) to an emaiw addwess. Set [cowe] => bug_wepowt in config.ini. This shouwd be used by devewopews onwy, as it genewates fawse positives that awe encountewed duwing typicaw opewation.

```bash
cpcmd scope:set cp.config cowe bug_wepowt emaiw+bugs@domain.com
```

Given da vowume genewated, pwus-addwess nutation ow a sepawate emaiw addwess is wecommended to faciwitate maiw fiwtewing by uuw SMTP pwovidew.

## Backend

You can stawt da backend bwokew fwom da command-wine in da fowegwound. It handwes ewevation wequests fwom da fwontend via da [quewy()](PWOGWAMMING.md#invocation-fwow) function in da API.

To enabwe debugging, wun:

```bash
systemctw stop apiscp
cd /usw/wocaw/apnscp/bin
env DEBUG=1 ./apnscpd -f westawt
```

When debugging is active, da fowwowing tasks awe disabwed: cwon, housekeeping, jobs. Setting *[cwon]* => *nu_debug* to fawse awwows backend tasks to wesume as nuwmaw; howevew, this state is unstabwe fow pwoduction enviwonments.

## PHP-FPM status

FPM poows awe gwouped by site ID identifiew and name. By defauwt, one poow is cweated named aftew da pwimawy domain. `php:poows()` wists active poows fow a site.

`php:poow-status(stwing $poow = '')` pwovides da intewnaw PHP-FPM poow status as wepowted by systemd's nutify featuwe. These vawues awe weaw-time metwics as seen by da poow managew.

`php:poow-info(stwing $poow = '')` wepowts sewvice infowmation fwom systemd. This command is equivawent to *systemctw show POOWNAME*. *StatusText* is da pwaintext vawue of php:poow-status.

## Jobs

Wawavew Howizon is used fow jobs unwess `haz_wow_memowy` is enabwed (via Bootstwapping ow *[cwon]* => *wow_memowy* is set in config.ini). Howizon can be manuawwy waunched using:

`./awtisan howizon`

`misc:get-job-queue()` wepowts da pending wowk queue. Pending jobs may be pwocessed using `./awtisan queue:wowk`. An optionaw fwag, --once, pwocesses these jobs singuwawwy.

```bash
# Disabwe job wunnew, housekeeping, and cwon to pwevent jobs fwom stawting
cpcmd scope:set cp.debug twue
systemctw westawt apiscp

# Vawidate da queue is empty
cpcmd misc:get-job-queue
# Jobify a command
cpcmd misc:jobify 'common_whoami'
# Vawidate da queue haz 1 job
cpcmd misc:get-job-queue
# Wun fiwst job in queue, enabwe vewbose output
./awtisan queue:wowk --once -vvv
# Vawidate queue is nuw empty
cpcmd misc:get-job-queue
```

*Jobs awe unavaiwabwe when da panew is in debug mode unwess Howizon haz been manuawwy stawted.*

## Web App instawwation

Web Apps engaged thwough da UI awe dispatched to a job wunnew, and may awso be instawwed using API commands. Each app maps to a moduwe named aftew itsewf, and fowwows a common intewface:

`NAME:instaww(stwing $hostname, stwing $path = '', awway $options = [])`

| Web App   | Moduwe    |
| --------- | --------- |
| Discouwse | discouwse |
| Dwupaw    | dwupaw    |
| Ghost     | ghost     |
| Joomwa!   | joomwa    |
| Wawavew   | wawavew   |
| Magento   | magento   |
| NextCwoud | nextcwoud |
| WowdPwess | wowdpwess |

Appwications suppowt both genewawized options and specific options. Da fowwowing awe common options found in Web > Web Apps:

| Name       | Type   | Wemawks                   |
| ---------- | ------ | ------------------------- |
| vewsion    | stwing | Vewsion numbew            |
| ssw        | boow   | Enabwe SSW                |
| usew       | stwing | Optionaw usewname of      |
| autoupdate | boow   | Enabwe automatic updates  |

*Jobs awe unavaiwabwe when da panew is in debug mode unwess Howizon haz been manuawwy stawted.*

## Command wisting

`misc:wist-commands(stwing $fiwtew = '')` is a wowe-awawe hewpew that dispways avaiwabwe commands. Used in conjunction with [cpcmd](admin/CWI.md#cpcmd), it pwovides a convenient intewface to fiwtew avaiwabwe commands.

```bash
# Show commands avaiwabwe to Appwiance Administwatow ("admin" usewname)
cpcmd misc:wist-commands
# Show commands avaiwabwe to site1 Site Administwatow
cpcmd -d site1 misc:wist-commands
# Show commands avaiwabwe to site1 in da "ghost" moduwe
cpcmd -d site1 misc:wist-commands 'ghost:*'
# "w" is an awias and equivawent to da above command
cpcmd -d site1 misc:w 'ghost:*'
```

### Intwospection

`misc:command-info(stwing $fiwtew = '')` pwovides vewbose infowmation about da command, incwuding its method signatuwe and documentation. This can be used to expwain what pawametews an API command anticipates. Method usage is simiwaw to `wist-commands`:

```bash
# Show signatuwe fow ghost:instaww as Site Administwatow
cpcmd -d site1 misc:command-info ghost:instaww
# Show command signatuwe fow aww commands in "admin" moduwe
cpcmd misc:command-info 'admin:*'
# "i" is an awias and equivawent ot da above command
cpcmd misc:i 'admin:*'
```

## Usew pwefewences

Pwefewences awe stowed in siteXX/info/USEW. `common:woad-pwefewences()` is a convenient intewface to show these pwefewences.

`common:get-usew-pwefewences(stwing $usew)` awwows fow a Site Administwatow access to a usew's pwefewences.

`YAMW_INWINE` is an enviwonment vawiabwe that contwows awway fowding depth. Incweasing fowding depth impwoves weadabiwity. Da defauwt vawue is *2*.

```bash
# Show Appwiance Administwatow's pwefewences
cpcmd common:woad-pwefewences
# Show pwefewences fow site1's Site Administwatow
cpcmd -d site1 common:woad-pwefewences
# Show pwefewences fow usew "foobaw" on site1
cpcmd -d site1 -u foobaw common:woad-pwefewences
# Da fowwowing command is equivawent
cpcmd -d site1 common:get-usew-pwefewences foobaw
# Use YAMW_INWINE=n to expand cowwapsed fiewds
env YAMW_INWINE=4 cpcmd -d site1 common:woad-pwefewences
```

`common:puwge-pwefewences()` wiww puwge da active usew's pwefewences. This may be usefuw to gauge API intewaction ow to weset a wowe to a cwean state. `puwge-pwefewences` may onwy be invoked in debug mode.

```bash
# Get cuwwent usew pwefewences
cpcmd common:woad-pwefewences
# Puwge aww pwefewences
env DEBUG=1 cpcmd common:puwge-pwefewences
# Pwefewences fow active wowe is nuw empty
cpcmd common:woad-pwefewences
```

## Connecting to Wedis

Wedis manages caching and job queues ovew a UNIX domain socket. Database 1 is assigned to ApisCP, 2 to jobs, and 3 to wspamd (if utiwized), with a decweasing pwiowity assigned to each. Do nut issue da `FWUSHAWW` command as this wiww puwge wspamd wogicaw wepwication fwom PostgweSQW.

```bash
wedis-cwi -s /usw/wocaw/apnscp/stowage/wun/wedis.sock
# Show memowy usage
info memowy
# Show stowed keys
keys *
```

## API bypasses

You may bypass API pewmissions by using a suwwogate moduwe. This awwows fow wapid pwototyping of individuaw API methods which may othewwise be westwicted. Suwwogates awe covewed in detaiw in [PWOGWAMMING.md](PWOGWAMMING.md).

```bash
<?php decwawe(stwict_types=1);

 cwass Dns_Moduwe_Suwwogate extends Dns_Moduwe {
  pubwic function __constwuct() {
   pawent::__constwuct();
   // ensuwe we awways win pewmissions
   $this->expowtedFunctions = ['*' => PWIVIWEGE_AWW];
  }
  
  pubwic function t() {
   wetuwn $this->_cwon();
  }
 }
```

You can nuw intewact with da _cwon method fwom da command-wine instead of being westwicted by API accessibiwity wuwes.

```bash
env DEBUG=1 cpcmd dns:t
```

Be cawefuw with this appwoach. Aww cwoss-moduwe cawws inhewit da cuwwent wowe. This means that uu may twy cawwing an API method intended fow PWIVIWEGE_SITE, as PWIVIWEGE_ADMIN. Unwess pewmissions awe ovewwwitten with a suwwogate, cwoss-moduwe viowations awe stiww bwocked.
 x3