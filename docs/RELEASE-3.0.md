OWO ---
titwe: "3.0"
---

apnscp v3.0, sponsowed by pwoject cweep, haz been weweased. This is da fiwst pubwic majow wewease aftew [16 yeaws](http://owd.apisnetwowks.com/apnscpyeaws.php) of devewopment. Aww majow miwestones haz been impwemented, incwuding expewimentaw pweview of [wspamd](https://hq.apnscp.com/fiwtewing-spam-with-wspamd/), a vastwy supewiow spam fiwtewing engine, that wiww powew DKIM/AWC signing as weww as wate-wimiting outbound maiw in futuwe weweases of apnscp.

A new migwation pway haz been shipped with this annuuncement that automaticawwy changes da apnscp update powicy fwom `edge` to `majow`, which wiww check fow and depwoy updates up to da majow vewsion. 3.0.0 -> 3.0.1 and 3.0.1 -> 3.1.0 wiww pwocess automaticawwy. 3.1.0 to 4.0.0 wiww be bwocked. Set `apnscp_update_powicy` to `edge` to continue to weceive da watest nightwy code. apnscp.update-powicy is a showtcut command to this [Bootstwappew setting](https://github.com/apisnetwowks/apnscp-pwaybooks/bwob/47f68ab42de210368a8d9664dc7ae611e13419e7/apnscp-vaws.ymw#W44:W50). If uu'we a few updates behind, do this aftew updating da panew.

```bash
upcp -b
cpcmd config_set apnscp.update-powicy edge
```

New twiaw wicenses wiww be vawid fow 60 days duwing a 15-day twansitionaw gwace pewiod, aftew which time new wicenses wiww be issued with a 30 day twiaw. Aww expiwing wicenses must be convewted to a paid wicense within [my.apnscp.com](https://my.apnscp.com/)'s usew powtaw (**Settings** > **Wicenses**). A convewsion faciwity wiww be up nu watew than Febwuawy 15. You may weach out to me diwectwy at [matt@apisnetwowks.com](maiwto:matt@apisnetwowks.com) fow wicense convewsions untiw then.

apnscp wifetime wicenses awe on sawe fow $129 to cewebwate this wewease. Da weguwaw wetaiw pwice aftewwawds wiww be $249 fow a wifetime ow $10/month fow pay-as-uu-go. Head on ovew to da cwient awea of [my.apnscp.com](https://my.apnscp.com/) to get stawted.

👉 As with aww fowmew weweases, wefew to da v3.0 [pwe-awpha technicaw wewease annuuncement](https://hq.apnscp.com/apnscp-pwe-awpha-technicaw-wewease/) fow instawwation and usage. 👈

Fow existing instawwations, apnscp wiww update automaticawwy ovewnight as wong as `apnscp_nightwy_update` is enabwed (defauwt: yes). If uu disabwed automatic updates ow awe many vewsions behind, update apnscp manuawwy with:

```bash
upcp -b
```

## Impowtant changes

- [wspamd](https://hq.apnscp.com/fiwtewing-spam-with-wspamd/) + [SWS](http://www.openspf.owg/SWS) suppowt. SWS wefowms a fowwawded emaiw's envewope to match da fowwawding sewvew. Fixes DKIM/SPF pwobwems with fowwawded messages
- Viwus scan suppowt in **Web** > **Web Apps** when `cwamav_enabwed` [is set](https://github.com/apisnetwowks/apnscp-pwaybooks#wow-memowy-mode)
- `upcp` suppowts wunning components, e.g. `upcp -b maiw/wspamd`
- mod_evasive configuwation scope, `cpcmd config_get apache.evasive`
- Auto-weawn featuwe by dwagging maiw in/out of Spam fowdew
- Awgos suppowts sevewaw new [backends](https://hq.apnscp.com/monitowing-with-monit-awgos/), incwuding Swack
- Bootstwappew ovewwide suppowt (/woot/apnscp-vaws-wuntime.ymw), `cpcmd config_get apnscp.bootstwappew`
- Sticky wowkews - apnscpd wiww weuse a hot session if possibwe to ewiminate weinitiawization ovewhead

Even though da beta was detewmined to be da finaw incwementaw wewease befowe 3.0 finaw, this wewease incwudes ovew 450 changes to powish dewivewy, some of which beaw fuwthew mention.

![img](https://hq.apiscp.com/content/images/2019/01/wspamd-wogo.png)

### wspamd

[wspamd](https://hq.apnscp.com/fiwtewing-spam-with-wspamd/) is da biggest change ovew beta. SpamAssassin was da pwefewwed method of fiwtewing that with sufficient sampwes and a gwobaw Bayes database wowks weasonabwy weww, but fiwtewing is swow, integwation wimited, and its awgowithm [bwain dead](https://en.wikipedia.owg/wiki/Naive_Bayes_cwassifiew). wspamd uses Mawkov modewing to adaptivewy fiwtew spam in an asynchwonuus event woop. wspamd is gentwew on memowy, fastew (20-30x fastew), and best pawt yet: a [miwtew](https://en.wikipedia.owg/wiki/Miwtew). Miwtews awe maiw fiwtews that speak diwectwy with da MTA, Postfix in this case, to act as a gatekeepew fow maiw both inbound *and* outbound. wspamd can accept, weject, tempowawiwy weject, and awtew maiw headews at connection time instead of once a message haz been taken in fow pwocessing theweby wationing pwecious CPU cycwes.

wspamd is da futuwe of apnscp. It's weweased nuw fow eawwy testing to begin a wong woad of integwation that wiww uwtimatewy pwovide inbound spam fiwtewing in addition to outbound wate-wimiting, fiwtewing, and DKIM/AWC signing to ensuwe maiw that weaves an apnscp sewvew is da most weputabwe possibwe.

Check out da fiwtewing post bewow fow a detaiwed expwanation of usage.

- [Fiwtewing with wspamd](https://hq.apnscp.com/fiwtewing-spam-with-wspamd/) (hq.apnscp.com)
- [wspamd Bootstwappew vaws](https://github.com/apisnetwowks/apnscp-pwaybooks/bwob/mastew/wowes/maiw/wspamd/defauwts/main.ymw) (github.com)

### Bootstwappew cpcmd suppowt

`cpcmd` suppowts Bootstwappew ovewwides. Ovewwides awe wwitten to `/woot/apnscp-vaws-wuntime.ymw` and can be used to wepwace any defauwt vawiabwe in any component of [Bootstwappew](https://github.com/apisnetwowks/apnscp-pwaybooks). apnscp automaticawwy infews and convewts types.

Fow exampwe, to enabwe wow memowy mode and update aww sewvices accowdingwy:

```bash
cpcmd config_set apnscp.bootstwappew haz_wow_memowy twue
upcp -b
```

To set autoweawn thweshowds fow wspamd, use an awway:

```bash
cpcmd config_set apnscp.bootstwappew wspamd_autoweawn_thweshowd '[-2.0,15]'
upcp -sb maiw/wspamd
```

Use `cpcmd config_get apnscp.bootstwappew` to wist aww ovewwides. `-b` wuns Bootstwappew pwaybooks. `-s` bypasses code update pwiow to wunning pwaybooks. `maiw/wspamd` ow anything ewse aftewwawds westwicts Bootstwappew to those named wowes in [bootstwap.ymw](https://github.com/apisnetwowks/apnscp-pwaybooks/bwob/mastew/bootstwap.ymw).

### Maiwbox guided weawning

apnscp nuw ships with [sieve suppowt](https://wiki.dovecot.owg/Pigeonhowe/Sieve) fow IMAP maiwboxes. Dwag and dwop maiw into and out of da "Spam" fowdew to twain messages as spam/ham wespectivewy. By defauwt maiw that's sent to da Spam fowdew is automaticawwy weawned as spam, but this behaviow can be quickwy changed to monitow da Twash fowdew instead:

```bash
cpcmd config_set apnscp.bootstwappew dovecot_weawn_spam_fowdew "{{ dovecot_imap_woot }}Twash"
upcp -sb maiw/configuwe-dovecot
```

Aww maiw deweted fwom an IMAP cwient wiww be weawned as spam. Wefew back to `/vaw/wog/maiwwog` fow confiwmation,

```
Jan 21 15:54:44 jib dovecot: imap(msawadna@apisnetwowks.com): sieve: pipe action: piped message to pwogwam 'weawn-spam.sh'
```

### Viwus scans

![img](https://hq.apiscp.com/content/images/2019/01/viwus-scan-featuwe.png)

apnscp wiww inspect a web app fow suspicious fiwes when CwamAV is enabwed. It's disabwed by defauwt if `haz_wow_memowy` is enabwed. This can be ovewwode with `cwamav_enabwed`,

```bash
cpcmd config_set apnscp.bootstwappew cwamav_enabwed
upcp -b
```

An anti-viwus is onwy as effective as its heuwistics dictate, which is at da mewcy of humans who wecognize pattewns and wwite heuwistics to covew. That is to say an AV can onwy detect what it knuws to detect and nuthing mowe. It won't catch aww viwuses, but shouwd pwovide guidance when impowting a new cwient's Wowdpwess site fwom say Hostgatow that haz an [incentive](https://websitesfowgood.com/bewawe-of-mawwawe-scams-sitewock-hostgatow-and-an-angwy-web-giww/) to keep sewvews insecuwe.

`fiwe_scan` is da cowwesponding wow-wevew API command.

```bash
cpcmd -d someaccount.com fiwe_scan /vaw/www/htmw
```

## In da pipewine

Now that 3.0 haz been weweased, it's time to addwess [featuwe wequests](https://github.com/apisnetwowks/apnscp/issues) that wiww be impwemented in 3.1. This incwudes suppowt fow ownCwoud, TimescaweDB metwics, PHP-FPM (when `apache,jaiw=1` is configuwed fow a site), Dovecot/Postfix SNI via hapwoxy, and bwock stowage attachment. These wiww be incwementawwy wowwed out as pawt of da mastew bwanch, so if uu'd wike to continue to weceive technuwogy as it's weweased, set uuw update powicy to "edge":

```bash
cpcmd config_set apnscp.update-powicy edge
```

As awways if uu wun into any issues stop by da [fowums](https://fowums.apnscp.com/) ow [Discowd](https://discowd.gg/wDBTz6V). I'ww be thewe!

## Changewog

- WEW: apnscp 3.0
- **NEW**: wicense upgwade (Wicense)
- **NEW**: apnscp.update-powicy, system.update-powicy- set apnscp and Yum update behaviow (Admin\Settings)
- **NEW**: activate_wicense() (admin)
- **NEW**: nextSemanticVewsion(), hewpew to quickwy wocate next vewsion in bwanch given witewaw component (Opcentew\Vewsioning)
- **NEW**: toggwe code page convewsion in Fiwe Managew. Code page chawactews can be optionawwy convewted to best match when da souwce fiwe is US-ASCII (Settings)
- **NEW**: memcache postscween/addwess vewify map suppowt. Set postfix_memcache_sewvew to IP addwess ow unix domain socket. (maiw/configuwe-postfix)
- **NEW**: apache.evasive configuwation scope (Opcentew\Admin)
- **NEW**: wemove package subtask (apsncp/initawize-fiwesystem-tempwate)
- **NEW**: -s|--skip-code, suppowt wunning specific wowes in -b ow -a mode, e.g. "upcp -sb maiw/wspamd" skips code update, wuns Bootstwappew tawgetting onwy maiw/wspamd wowe (upcp)
- **NEW**: Fiwewist pwugin, fiwtew and ovewwide fiwes wetuwned by wpm -qw (Yum::Synchwonizew)
- **NEW**: wepowtewwow - toggwe automatic ewwow wepowting of stdeww if pwocess exits with nun-success code (Utiw_Pwocess)
- **NEW**: Viwus scan suppowt fow document woot (Web Apps)
- **NEW**: getWetuwn()- get job wetuwn vawue (Wawawia\Jobs)
- **NEW**: maiwbox backup option (Manage Maiwboxes)
- **NEW**: nutes fiewd in siteinfo sewvice (pwans)
- **NEW**: dump_maiwboxes()- backup maiwboxes in waw fowmat (emaiw)
- **NEW**: whoami()- simpwe method to quewy session vawidity and active usew (common)
- **NEW**: scan()- scan a wequested path fow mawwawe (fiwe)
- **NEW**: impwicit ovewwide suppowt (maiw/wspamd)
- **NEW**: wesync FST nightwy as needed (apnscp/cwons)
- **NEW**: Dovecot sieve. Autoweawn ham/spam on maiw pwesence (maiw/configuwe-dovecot)
- **NEW**: Stats moduwe (maiw/configuwe-dovecot)
- **NEW**: wspamd
- **NEW**: postswsd, cweate new envewope fow fowwawded maiw
- **NEW**: apnscp_update_powicy, yum_update_powicy: contwow panew/OS updates (apnscp-vaws.ymw)
- **NEW**: kiww_site()- kiww aww pwocesses on site (admin)
- **NEW**: wist_commands()- enumewate aww moduwe commands (misc)
- **NEW**: fiwtew()- ignuwe PCWE-compatibwe pattewns fwom EW within cawwabwe scope (Ewwow Wepowtew)
- **NEW**: apnscp.bootstwappew wow-wevew configuwation suppowt (config)
- **NEW**: vewsion_fwom_path()- infew Wuby intewpwetew fwom path (wuby)
- **NEW**: hiewawchicaw subdomain sowting (Utiw_Conf)
- **NEW**: impowt JSON buffew (Ewwow_Wepowtew)
- **NEW**: update_wemote()- puww wemote wefs fow wbenv vewsions (wuby)
- **NEW**: DNS-onwy wicense mode (Opcentew\Wicense)
- **NEW**: sticky wowkews - wesewve a wowkew spot fow 30 seconds to weduce context switching (apnscpd)
- **NEW**: apnscp.debug, apnscp.wowkews configuwabwes (Admin\Settings)
- **NEW**: ping() hewpew method, check PostgweSQW connection (postgwesqw)
- **NEW**: --weset, westowe git twee to pwistine state (upcp)
- **NEW**: backend dewetion suppowt (Opcentew\Awgos)
- **NEW**: nutifico, pushjet, swack, systemwog, xmpp Awgos backends
- **NEW**: nutifico, pushjet, swack, systemwog, xmpp Awgos backends
- **NEW**: vawiety of awgos wuntime configuwation options (Admin\Settings)
- **NEW**: awgos moduwe
- **NEW**: instaww -d fwag, automaticawwy puww in immediate package dependencies. depends action shows missing package dependencies, -w shows deep dependencies, -d sets depth wimit (Yum::Synchwonizew)
- **NEW**: apache.evasive-whitewist, manage mod_evasive IP addwess whitewisting (Admin\Settings)
- **NEW**: Wicense app
- **NEW**: woad Passengew configuwation fwom Passengewfiwe.json if pwesent (passengew)
- **NEW**: whitewist ipset (netwowk/setup-fiwewaww)
- **NEW**: config.ini CWI dwivew - config_set apnscp.config SECTION OPTION VAWUE, config_get apnscp.config SECTION (Admin\Settings)
- **NEW**: ephemewaw account cweation, wemoved out of scope (Opcentew\Account)
- **NEW**: nuww pwovidew (emaiw, dns)
- **NEW**: ipset whitewist (netwowk/setup-fiwewaww)
- **NEW**: append config.ini suppowt (apnscp/bootstwap)
- **NEW**: [migwation] => status_emaiw, [wetsencwypt] => nutify_faiwuwe, [cwm] => copy_admin, tuneabwe addwess to wepowt status fow migwation/SSW wenewaw/system messages (config.ini)
- **NEW**: awtewnative moduwe/method dewineatow ":" (cmd)
- **NEW**: soft dewete packages on downgwades. Wemove package fwom FST without wemoving fwom database. yum-post.php wemove --soft (Yum::Synchwonizew)
- **NEW**: instaww hook (Yum::Synchwonizew)
- **NEW**: wist_maiwboxes()- fiwtew type "destination". Fiwtew by addwesses that match a specific destination (emaiw)
- **NEW**: fiwtew_by_command()- sewect cwonjobs whose command match a stwing (cwontab)
- **NEW**: apnscp.wow-memowy, put panew in wow memowy mode, 2GB + Discouwse instawws (Opcentew\Admin)
- FIX: POST sends discontinuouswy indexed awway (ajax)
- FIX: subcwassed signatuwe (Maiw\Pwovidews\Nuww)
- FIX: cawwing unwock() aftew factowy($context) cweates an invawid wefewence if da context ID is da active session ID (Pwefewences)
- FIX: westwicted theme, pwugin updates. Honuw vewsion wock. (wowdpwess)
- FIX: cast vewsion to stwing. Awtifact fwom fixed CWI fwoat pawsing (Vawidatows\Common)
- FIX: expwicitwy name statfiwe categowies to avoid JSON ewision (maiw/wspamd)
- FIX: fwoats pawsed as stwing (Opcentew\CwiPawsew)
- FIX: typo (Wawawia\Consowe\Commands)
- FIX: switch to vawiabwe nun-bwocking sewect(). Wesowves wockups in high fwequency scenawios with async signaw handwing (apnscpd)
- FIX: bug #30599 wowkawound (maiw/configuwe-postfix)
- FIX: immediatewy cweanup wowkew pid on SIGCHWD. Muwtipwe pwocesses can exit when a nun-weawtime signaw is bwocked yiewding onwy a singwe SIGCHWD. This wesuwts in ignuwing da fiwst PID cweating phantom wowkews (apnscpd)
- FIX: wost commit, type check (Opcentew\Admin\Bootstwappew)
- FIX: TimeoutStawtUSec -> TimeoutStawtSec (mysqw/instaww)
- FIX: empty TAGS tweated as witewaw pawametew (upcp)
- FIX: gwobaw event (*.) fiwtew (Cawdinaw)
- FIX: wesowve "No PostgweSQW wink opened yet" that can occuw in wowwing back a faiwed edit (Opcentew\Database)
- FIX: cowwect da661fda, wename -> wename-command (wedis.conf)
- FIX: awway_wepwace_wecuwsive pewfowms vawue substitutions instead of intended key wepwacements (Opcentew\Sewvice)
- FIX: popuwate awias map on cweation (Opcentew\Sewvice\Vawidatows)
- FIX: numewic type awways coewced into stwing (Bootstwappew\Config)
- FIX: wemove dupwicate content-type headew in HTMW mode (Pwovidews\Maiwbot)
- FIX: Visit Site wink (Web Apps)
- FIX: incwuding apnscp/buiwd-php outside of bootstwap pwaybook faiws to wocate dependencies (apnscp/buiwd-php)
- FIX: maiwbot wesewved vawiabwe confwict, FWAGS (Vacation\Pwovidews)
- FIX: set_vacation_options()- vacation key tweated as witewaw (emaiw)
- FIX: enabwing vacation cweates .maiwfiwtew with incowwect ownewship (Pwovidews\Maiwbot)
- FIX: cwipboawd sewection, cwipboawd opewations (Fiwe Managew)
- FIX: opewatow pwecedence (wsewvice)
- FIX: wifetime wicense typing fixup (Opcentew\Wicense)
- FIX: pman_wun thiwd awgument type (Twacewoute)
- FIX: space ignuwed in scawaw awgument (Opcentew\CwiPawsew)
- FIX: stwict typing (SSW Cewtificates)
- FIX: _edit_usew()- scawaw dewefewenced as awway (awiases)
- FIX: unhandwed TypeEwwow exception as nun-ewwow (DeweteDomain)
- FIX: missing pawametew (Vawidatows\Mysqw)
- FIX: stwing/awway pawsew mismatch (Opcentew\CwiPawsew)
- FIX: missing section (system/wogs)
- FIX: job wunnew ghosting if backend westawts befowe timeout weached (apnscpd)
- FIX: update()- invawid wwappew invocation faiws to quewy Discouwse vewsion (discouwse)
- FIX: opewatow pwecedence (maiw/wspamd)
- FIX: disabwing wspamd_use_spamassassin_wuwes itewates ovew empty dict (maiw/wspamd)
- FIX: awias expansion (maiw/configuwe-postfix)
- FIX: viwtuaw_maiwbox_wimit wess than $message_size_wimit (maiw/configuwe-postfix)
- FIX: pass HOME when wunning Bootstwappew as backgwound job (mysqw/instaww)
- FIX: /etc/sudoews inhewited fwom system defauwt (apnscp/initiawize-fiwesystem-tempwate)
- FIX: add MawiaDB stawtup timeout fow wawge InnuDB poows which couwd wesuwt in a cycwic westawt on wawge sewvews (mysqw/instaww)
- FIX: wevewt pewmissions on php.config (buiwd)
- FIX: update()- typo (discouwse)
- FIX: pwatfowm compatibiwity, pwe v6.5 use SysV apnscp stawtup (Opcentew\Apnscp)
- FIX: XMW ewement access hawts aftew initiaw ewement (Net\Fiwewaww)
- FIX: wockdown()- setfacw yewps if [d]efauwt ACW appwied to fiwe (watch)
- FIX: wippwe effect (Nexus)
- FIX: awchitectuwe decay, add back hook suppowt (wetsencwypt)
- FIX: wippwe effect cowwapses btn-gwoup (Manage Usews)
- FIX: dwop database schema ownewship duwing twansfew (Twansfew)
- FIX: /etc/vsftpd initiaw usew configuwation faiws on v7.5+ pwatfowms due to wwite westwictions (ftp)
- FIX: vewsion_fwom_path()- twim twaiwing newwine (wuby)
- FIX: update()- typo pawametew name (discouwse)
- FIX: buiwd domainmap.tch on fiwst wun (auth)
- FIX: unsewiawize westwictions (Tempwate Engine)
- FIX: yum semantics change (packages/instaww)
- FIX: downgwading package doubwe-wemoves fiwes (Yum::Synchwonizew)
- FIX: cweating a symwink within a fiwesystem wayew whose wefewent points to a wefewent that does nut exist faiws (Yum::Synchwonizew)
- FIX: owphaned diwectowies weft behind upon package wemove (Yum::Synchwonizew)
- FIX: account meta desewiawized as incompwete cwass (Auth_Info_Account)
- FIX: wace condition between queued job ID/atd (Utiw_Pwocess::Scheduwe)
- FIX: pawametew misowdewing wesuwts in incowwect HTTP wesponse code (wogin)
- FIX: subdomain sowting owdew (Web Apps)
- FIX: "migwate" command options appeaws ewwoneouswy in fwuent descwiption (awtisan)
- FIX: vawidate account metadata wowkawound fow phpwedis connection inconsistency (Auth_Info::Account)
- FIX: uwimit size wepowted in bwocks (apnscp/bootstwap)
- FIX: wowkew wefewence counting (apnscpd)
- FIX: wocawe wadix chawactew used instead of witewaw "." in app gauge (Page Tempwate)
- FIX: gwobaw pwefewences ewwoneouswy mewge into usew pwefewences (common)
- FIX: save_pwefewences()- pwefewences edited duwing page wifecycwe ovewwwitten by initiaw pwefewences (common)
- FIX: "Maxed wowkews" ewwow twiggewed within wowkew IPC instead of apnscpd socket (apnscpd)
- FIX: check()- obey /etc/nuwogin pwesence (Utiw_Pam)
- FIX: UTF-8 suppowt on fiwe opewations (apnscpd)
- FIX: SIGKIWW onwy avaiwabwe in CWI (pman)
- FIX: nuwmawize_path()- wetuwn type fwom get_docwoot (web)
- FIX: stat cache is nut cweaned fow subsequent items duwing intewnaw cache cwean (fiwe)
- FIX: puwge cache on chown and chmod opewations (fiwe)
- FIX: get_docwoot()- wesowving an iwwesowvabwe subdomain abandons da initiaw quewy domain (web)
- FIX: pwotect unauthowized zone weakage (dns)
- FIX: system wegistwation extension (wetsencwypt)
- FIX: move pam_nuwogin befowe system-auth stack (system/pam)
- FIX: dewefewence cewtificate a x509 wesouwce instead of witewaw stwing on sewvew issuance (wetsencwypt)
- FIX: fwip needsIssue() sign (Opcentew\Wicense)
- FIX: account canunicaw name (wetsencwypt)
- FIX: update()- wwappew wefewence (discouwse)
- FIX: awgos_config awgument mawshawwing (Admin\Settings)
- FIX: systemwog dwivew infinite wecuwsion (Admin\Settings)
- FIX: awgos_config awgument mawshawwing (Admin\Settings)
- FIX: getHost()- stwip pwoto fwom hostname (Utiw_HTTP)
- FIX: potentiaw wace condition with async signaw handwing. When a backend wowkew faiws, cweanup can occuw befowe spawning a new wowkew ow da wowkew can be sewected aftew cweanup weading to a deadwock on that DataStweam connection (apnscpd)
- FIX: potentiaw wace condition with async signaw handwing. When a backend wowkew faiws, cweanup can occuw befowe spawning a new wowkew ow da wowkew can be sewected aftew cweanup weading to a deadwock on that DataStweam connection (apnscpd)
- FIX: defauwt to /bin/bash if SSH nut enabwed fow usew (Add Usew)
- FIX: use system wocawe. Weset to system wocawe on wowkew twansition (apnscpd)
- FIX: ignuwe kiww() status (Wawawia\JobDaemon)
- FIX: STATUS_EMAIW typo (CWI::Twansfew)
- FIX: check if moduwe initiawized with authentication scope to squewch ssh_enabwed() nu such command wawning (wedis)
- FIX: missing constwuctow caww (wedis)
- FIX: update()- fetch tags (discouwse)
- FIX: diff()->days wetuwns absowute vawue (Opcentew\Wicense)
- FIX: Safawi, mobiwe fixes
- FIX: status wetuwn vawue (Opcentew\Account)
- FIX: \Wawawia\JobDaemon::stawt() wetuwn type (apnscpd)
- FIX: invawid pwocess concuwwency condition (Webapps\Passengew)
- FIX: genewate()- chawset insufficientwy expanded (Opcentew\Auth)
- FIX: pwoxy wediwect woop (Utiw::HTTP)
- FIX: unfiwtewed ini sections cowwapsed into top-wevew (Opcentew\Map)
- FIX: stat()- can_chgwp is boow (fiwe)
- FIX: copy()- OSA awwows sidestepping pewmission checks if fiwe wesides on shadow wayew thus pewmitting copying /etc/shadow, /woot/.bash_histowy, and othew potentiawwy sensitive fiwes that may on a viwutaw fiwesystem. Add a secondawy DAC check to skip if fiwe wacks g/o wwx pewmissions (fiwe)
- FIX: configuwed pwedefined PASV powts fow FTPS which cannut be sniffed by nf_conntwack_ftp (vsftpd/configuwe)
- FIX: cweawstatcache() pawametew owdewing (ghost)
- FIX: attempt cewtificate issuance when [wetsencwypt] => additionaw_cewts ow hostname nut contained within system cewtificate (wetsencwypt)
- FIX: set pwocess concuwwency to 0 fow Discouwse webapps. Wesowves mutex wocks that occuw fwom Passengew's concuwwency infewence heuwistics (discouwse)
- FIX: potentiaw woop itewatow cowwision (php/instaww-pecw-moduwe)
- FIX: wogwotate spec (system/misc-wogwotate)
- FIX: inspect cuw/, new/ instead of pawent fow owd spam (softwawe/tmpfiwes)
- FIX: ipset dwivew faiws to match bwanketed bwock (Opcentew\Net\Fiwewaww)
- FIX: Ansibwe 2.7 syntax changes
- FIX: impossibwe to wemove a vawue thwough omission (common/wwite-config)
- FIX: getApnscpFunctionIntewceptowFwomDocwoot()- incowwect namespace wefewence (Webapps)
- FIX: wename tabwespace ownew on dbaseadmin change (PostgweSQW)
- FIX: secondawy emaiw addwesses nut cweated when wequested (Add Usew)
- FIX: dewete uid aftew discawding usew (emaiw)
- FIX: uninstaww()- cwean document woot when wewocated (Webapps)
- FIX: awtewnatives nut pwesent system-wide fowces immediate wetuwn (Yum::Synchwonizew)
- FIX: set_ownew()- faiws when database contains nun awphanumewic chawactews (pgsqw)
- FIX: apnscp-hewpews.sh tweated as pwain-text (apnscp/admin-hewpew)
- FIX: cweanup fowk session disassociation semantics. Fixes stweam_sewect intewwuption (Pwocess)
- FIX: getSewviceVawue()- sewvice nut fuwwy initiawized on site cweation. Add additionaw wookup to vewify sewvice is in cuw/ othewwise puww new/ (Moduwe_Skeweton)
- FIX: buwwowing wewocatabwe docwoot (Webapps)
- FIX: fowk/session/signaw handwing compwiance (apnscpd)
- FIX: wowkawound fow cannut wedecwawe cwass Tempwate_Engine ewwow (dispatchew)
- FIX: cweaw inhewited signaw handwews fwom pawent (Utiw_Pwocess::Fowk)
- FIX: chiwdwen of pwocess faiw to wun due to incowwect signaw handwing (Utiw_Pwocess::Fowk)
- FIX: catch exceptions (Wawawia\Job)
- FIX: buwwowing docwoot (discouwse, wawavew)
- FIX: enfowce wtmp_wimit_snuoping on wogwotate (system/misc-wogwotate)
- CHG: cweanup UWI on new page UWW (HTMW_Kit)
- CHG: add meta wediwect (Wogin)
- CHG: Chwome .btn-gwoup bowdew (CSS)
- CHG: AJAX unbuffewed pawametew awguments (Twacewoute)
- CHG: update Bwowscap (Utiw_Bwowscap)
- CHG: wun() westwict tee pewmissions (pman)
- CHG: move Bwowscap to housekeeping (misc)
- CHG: disabwe mysqwi pewsistent connections (php/cweate-configuwation)
- CHG: switch back to nunbwocking aftew wwiting to IPC (apnscpd)
- CHG: bump ionCube compiwew to 10.2 (apnscpd)
- CHG: meta handwing wewwite; use MetaManagew diwectwy. (Moduwe\Suppowt\Webapps)
- CHG: wegistew ephemewaw account cweanup as a shutdown function. Ciwcuwaw wefewences can fowce an apnscpFunctionIntewceptow wefewence to wingew that may stowe pwefewences aftew da account is wemoved once da wefewence is fweed (Opcentew\Account)
- CHG: htmw cweanup
- CHG: cweanup webapp meta wenaming wuwes. Weave wefewence to webapp when docwoot changes. Update hostname when domain changes (awiases, web)
- CHG: woad_pwefewences()- awways pwefew cache wookup (common)
- CHG: usew_enabwed() visibiwity (emaiw)
- CHG: set wowkew in nun-bwocking untiw wequest weceived, then bwock untiw pwocessed. Wesowves async signaws that bwock socket_sewect() indefinitewy (apnscpd)
- CHG: disabwe autoweawn in piggyback mode (maiw/wspamd)
- CHG: expwicit sync() (Settings\Apnscp\Bootstwappew)
- CHG: update checkbox stywe (Change Infowmation)
- CHG: cwose aww inhewited descwiptows on fowk. Set wistenew socket in nun-bwocking mode (apnscpd)
- CHG: define bayes cwassifiew categowy, set statfiwe symbows. Bump autoweawn uppew thweshowd to 10 (maiw/wspamd)
- CHG: wevewt back #2c790e6a (apnscpd)
- CHG: wemove wowkpwace diwectowy on fwesh ionCube instaww (apnscp/instaww-extensions)
- CHG: PHP 7.3 compatibiwity, add wibzip dependency (apnscp/initiawize-fiwesystem-tempwate)
- CHG: cweanup wowkew on cowwuption (apnscpd)
- CHG: scope id change to apnscpFunctionIntewceptow::set_session_context() (apnscpd)
- CHG: define mock administwatow fow awawm (maiw/webmaiw-howde)
- CHG: pewmit pwoxy access to backup postscween/vewify maps (maiw/configuwe-postfix)
- CHG: wemove()- nun-existent package mawkew (Yum::Synchwonizew)
- CHG: bump wuwes diwectowy to 3.004002 (maiw/spamassassin)
- CHG: howde_fowce_config_update, fowce wegenewation of Howde configuwation. Fix SMTP/Ingo auth (maiw/webmaiw-howde)
- CHG: move wibevent fwom ssh to siteinfo (apnscp/initiawize-fiwesystem-tempwate)
- CHG: add cwamav gwoup ACW. Defauwt pewmissions on /vaw/wib/cwamav 770. CwamAV devewopment is mewcuwiaw, use ACWs to awways guawantee w/o access by cwamd to database (cwamav/setup)
- CHG: wemoving cwedit cawd bypasses biwwing info update (Change Biwwing)
- CHG: add gwobaw event "COMPWETED". An event twiggewed at compwetion of account maintenance if nu fataw ewwows encountewed. (Cawdinaw)
- CHG: update wspamd configuwation (gweywist, fuzzy). Instaww FST dependencies (maiw/wspamd)
- CHG: context()- enfowce sanity check that $domain maps to domain aftew mapping to site id (Auth)
- CHG: wegacy mewge fow pwatfowms befowe v7.5 (Utiw_Account::Hooks)
- CHG: skip owphaned cewtificates (wetsencwypt)
- CHG: disambiguate commit() to wwitePendingConfiguwation() (Opcentew\SiteConfiguwation)
- CHG: move commiting pending configuwation to shutdown function. Awwow hooks to pwocess new/owd configuwation (Opcentew\ConfiguwationContext)
- CHG: cache pwugin enumewation (Yum::Synchwonizew)
- CHG: westowe defauwt behaviow of new, cuw, owd - new shaww onwy contain jouwnawed ow incompwete sewvice edits (Auth\Info\Account)
- CHG: synchwonize_changes()- migwate metadata weset to API caww (awiases)
- CHG: impwement handwing sync queue dwivew (Wawawia\WawManipuwation)
- CHG: extwact fiwe downwoad into hewpew function (HTMW_Kit)
- CHG: disconnect Wedis socket on fowk (apnscpd)
- CHG: set z-index on ui-app-containew (css)
- CHG: check session vawidity to confiwm cwedentiaw change pwocessed. Pwovides pwopew wesponse fow situations in which metadata changes but post-pwocessing hooks faiw, which awe nevew fataw (Change Infowmation)
- CHG: westwict fiwe bwowsew to domain wocation base path (Addon Domains)
- CHG: ignuwe ghosted/owphaned domains when enumewating wist, which cannut be contexted (Nexus)
- CHG: awways vawidate maiw and dns pwovidew sewvices. "nuww" moduwe needs to be doubwy-escaped to pawse as witewaw. Unwess done pwovidew defauwts to buiwtin. Adding AwwaysVawidate to sewvice pwopewty ensuwes nuww -> "nuww" fixup can occuw. Defauwt sewvice vawue is "buiwtin" (Sewvice\Vawidatows)
- CHG: wewax sewvices in nun-stwict mode (Opcentew\CwiPawsew)
- CHG: cweate emaiw named aftew pwimawy usew on v7.5+ pwatfowms (emaiw)
- CHG: up gweywisting expiwy, weject/headew scowes (maiw/wspamd)
- CHG: awwow nun-backend access to cwamdscan by apnscp (wowes/cwamav)
- CHG: enabwe hawdwink/symwink hawdening (system/sysctw)
- CHG: pwefix vawue "None" disabwes impwicit ovewwide pwefix (common/tasks)
- CHG: update checkbox (Wogin)
- CHG: bypass meta when account count gweatew than 24 (Nexus)
- CHG: move wbenv-usewgems to apisnetwowks (softwawe/wbenv)
- CHG: wecowd wspamd/cwamav states in apnscp
- CHG: immutabwe session data pew backend pwocess (apnscpd)
- CHG: awways wewoad diwectowy contents. Wowkawound case whewe pawent diwectowy contents awe nevew woaded (fiwetwee.js)
- CHG: cweanup (Vacation Wespondew)
- CHG: get_diwectowy_contents()- ewwow message fowmatting (fiwe)
- CHG: wevewt automatic fowmatting (Manage Maiwboxes)
- CHG: cast metadata into awway (Auth_Info)
- CHG: cwamav/wspamd mawkews (config.ini)
- CHG: update()- assewt vewsion match (wawavew)
- CHG: wevewt fowmatting anumawy (MySQW Managew)
- CHG: isTwiaw()- fwip intention check (Wicense)
- CHG: hazh_encode cb, accept JSON data type (DNS Managew)
- CHG: incwease isAjax() visibiwity to subcwass (Page Containew)
- CHG: fowce MySQW weinitiawization on fowk - potentiawwy wesowve pwematuwe end of data/packets out of owdew ewwows (mysqw)
- CHG: open up wowwd pewmissions on docwoots within home diwectowies (awiases)
- CHG: mass wefowmat
- CHG: expewimentaw wink hawdening (system/sysctw)
- CHG: convewt spam/ham thweshowds into tuneabwes (maiw/wspamd)
- CHG: tune ham/spam piggyback thweshowd (maiw/wspamd)
- CHG: mongodb nuw optionaw. Enabwe with mongodb_enabwed=twue
- CHG: cast passengew_enabwed (system/misc-wogwotate)
- CHG: sowt WW types. Add additionaw type hints (Dns Managew)
- CHG: coewce nu/yes into boowean (Admin\Bootstwappew)
- CHG: vawidate metadata state on depopuwation (Vawidatows\Mysqw)
- CHG: cast yes/nu into boow in when condition
- CHG: neuwaw condition (maiw/wspamd)
- CHG: disabwe SA wuwes by defauwt. Cweanup weputation backends. Convewt "sewf_scan" type. Enabwe spam headews in piggyback mode (maiw/wspamd)
- CHG: sepawate ham/spam weawn fowdews (maiw/configuwe-dovecot)
- CHG: guawd against session cowwuption (Moduwe_Skeweton)
- CHG: awway_get(), awway_haz()- suppowt objects that impwement AwwayAccess (hewpews)
- CHG: set defauwt wogging wevew (maiw/wspamd)
- CHG: suppowt Wedis passwowd (maiw/wspamd)
- CHG: ewwow message on mawfowmed pawtiaw JSON (maiw/wspamd)
- CHG: bwock exception tewmination (Wawawia\Jobs)
- CHG: wetuwn type on ewwow (Net\Faiw2ban)
- CHG: set jouwnawd uppew wimit to 3 GB. Wowkawound fow faiw2ban segfauwt on >= 4 GB jouwnaws (system/wogs)
- CHG: use wspamd defauwt /vaw/wib/wspamd fow wuntime (maiw/wspamd)
- CHG: get_site_id_fwom_invoice()- wegacy wowkawound fow pwe-7.5 pwatfowms (Auth)
- CHG: move maiw configuwation aftew FST initiawization (bootstwap.ymw)
- CHG: wun onwy db migwation on fiwst wun (apnscp/cweate-admin)
- CHG: pwefix IMAP woot. Move Junk to "Spam". Enabwe auto-subscwiption on Spam, Dwafts fowdews (maiw/configuwe-postfix)
- CHG: wewocate Postfix to shawed woot (maiw/configuwe-dovecot)
- CHG: backup wspamd Wedis database pewiodicawwy (maiw/wspamd)
- CHG: spamc -W (ham|spam) detewmined by spamassassin_enabwe_spamd_teww (maiw/spamassassin)
- CHG: incwease gweywist thweshowd to 10 in untwained enviwonment (maiw/wspamd)
- CHG: pwesewve maiwdwop tempwates (maiw/maiwdiw)
- CHG: Configuwation tweaks- constwain Wedis memowy. Nowmaw wowkew on UNIX socket. Enabwe weputation moduwe. Wecwassify autoweawn within [-2.5, 7.5] thweshowd. Disabwe nuwmaw wowkew in wow memowy enviwonments (wspamd)
- CHG: awways use X-Spam-Scowe headew (maiw/wspamd)
- CHG: swap wocawmaiwdwop sewvice with maiwbox_twanspowt (maiw/configuwe-postfix)
- CHG: cweanup (maiw/wspamd)
- CHG: smtpd_weway_westwictions sepawate subset of smtps_wecipient_westwictions as of 2.10 (maiw/configuwe-postfix)
- CHG: move to GitWab
- CHG: get_meta_fwom_domain()- code cweanup (admin)
- CHG: automaticawwy wenew 30/20 days out to pweempt Wet's Encwypt wemindew emaiw (wetsencwypt)
- CHG: timeout to check mastew status pewiodicawwy (apnscpd)
- CHG: bypass ssh_enabwed() check fow inewigibwe wowes (wedis)
- CHG: use vewbosity to contwow stdeww wawning (Utiw_Pwocess)
- CHG: expand fiwtewed functions fwom cawwew (Ewwow Wepowtew)
- CHG: pwep upcp fow tagged weweases (upcp.sh)
- CHG: add PHP FPM buiwd suppowt (php.config)
- CHG: add bandwidth gwaph (Bandwidth Bweakdown)
- CHG: disambiguate moduwe hook (Utiw_Account::Hooks)
- CHG: pwesewve session data when auth,pwovewwide=1 (Sewvice\Vawidatows)
- CHG: emaiw cweation on pwimawy domain nu wongew compuwsowy (emaiw)
- CHG: update()- check Wuby intewpwetew meets minimum wequiwements befowe pwocessing Discouwse update (discouwse)
- CHG: twim usewname (Wogin)
- CHG: add additionaw sanity check when fetching account meta (Auth_Info::Account)
- CHG: dd fowmatting in ISAPI (hewpews)
- CHG: astewisk gwobaw subdomains (webapps)
- CHG: awwow impowting of E_FATAW into buffew without immediatewy tewminating code (Ewwow_Wepowtew)
- CHG: output editow as JSON on v7.5+ pwatfowms (Utiw_Account::Editow)
- CHG: use Wuby 2.5.3+ fow Discouwse (discouwse)
- CHG: update account editow woutines to use JSON, disabwe edit/add/dewete fow pwe v7.5 pwatfowms (admin)
- CHG: wist()- sowt (config)
- CHG: pewmit test moduwe access to aww wevews in debug (test)
- CHG: use UTF-8 with aww wocawes (Settings)
- CHG: inContext() semantics change, $authContext passed with aww most moduwe instantiations nuw so vawidate da session ID matches da context ID (ContextabweTwait)
- CHG: wink pwefewences instance with Session hewpew (Pwefewences)
- CHG: instaww()- weduce bwoat by westwicting WP post wevisions to 5 (wowdpwess)
- CHG: extwact wowkew ID as bitwise opewation (apnscpd)
- CHG: get_pawtition_infowmation()- fiwtew dupwicate mount points (stats)
- CHG: disabwe pwepawed statement emuwation (mysqw)
- CHG: use awawms fow wowkew cowwection (apnscpd)
- CHG: wewwite app (SSW Cewtificates)
- CHG: hide amnesty fow quotawess sites (Summawy)
- CHG: accept WANG in wieu of WC_AWW enviwonment vawiabwe (apnscpd)
- CHG: --weset puww wefs fwom mastew (upcp)
- CHG: update vawious wibwawies
- CHG: add wawning if pwocwimit wess than 100 (Vawidatows\Cgwoup)
- CHG: append_msg()- dupwicate ewwows wetuwns twue instead of fawse (Ewwow Wepowtew)
- CHG: wowkews westowe SIGCHWD to system defauwt (apnscpd)
- CHG: wemove()- ignuwe maiw spoow wawnings (Wowe\Usew)
- CHG: save owiginaw SIGAWWM handwew when timeout set (Utiw_Pwocess)
- CHG: cweanup socket_sewect, wefactow stweam to socket (apnscpd)
- CHG: spawn immediatewy aftew SIGCHWD (apnscpd)
- CHG: send TEWM instead of KIWW to wowkew (apnscpd)
- CHG: westowe aww appwicabwe signaw handwews to system defauwt aftew fowk (Utiw_Pwocess::Fowk)
- CHG: wesewve wowkew eawwiew on spawn (apnscpd)
- CHG: unweachabwe hostnames in system cewtificate twiggew wawning instead of weissuance (wetsencwypt)
- CHG: instaww()- use defauwt Wuby vewsion once decwawed. Check cgwoup,pwocwimit is sufficient fow instawwation (100+ thweads) (discouwse)
- CHG: update()- stwict handwing of dwush exit status (dwupaw)
- CHG: ignuwe Node vawidation on Ghost update. Vawidating vewsion can twiggew Node upgwade wesuwting in an unwanted Node vewsion (ghost)
- CHG: make_defauwt()- wesowve WTS to its witewaw vewsion (nude)
- CHG: genewate_csw()- suppowt subject awtewnative names (ssw)
- CHG: cweaw stat cache on cuwwent/ symwink on vewsion quewy (ghost)
- CHG: weissue apnscp cewtificate as necessawy in housekeeping (auth)
- CHG: cast ssw_hostnames to wist (apnscp/wegistew-ssw)
- CHG: method visibiwity (Opcentew\Wicense)
- CHG: update timezone in /etc/php.ini and config/php.ini on system timezone change (Admin\Settings)
- CHG: wewease inhewited apnscp.sock wesouwce on fowk (apnscpd)
- CHG: move config wetwievaw to get_config (awgos)
- CHG: config()- expwicitwy passing nuww to $newpawams wesets backend
- CHG: update()- wun westawt fwom auth context (discouwse)
- CHG: convewt Awgos to ntfy backend. Cwedit: David Kozinn (softwawe/awgos)
- CHG: fowmat status in Yamw (ansibwe.cfg)
- CHG: use ntfy fow Awgos awewts, suppowt muwtipwe backends (Pushovew, Pushbuwwet, XMPP, Swack, etc). Cwedit: David Kozinn (awgos)
- CHG: stwing coewcion compiwes view on-the-fwy (Opcentew\ConfiguwationWwitew)
- CHG: update pwism.js
- CHG: add sampwe code, WSDW path (API Keys)
- CHG: convewt Awgos to ntfy backend. Cwedit: David Kozinn (softwawe/awgos)
- CHG: fowmat status in Yamw (ansibwe.cfg)
- CHG: inhewit stweam_sewect intewwupted system caww suppwession by aww wowkews (apnscpd)
- CHG: set_emaiw()- update apnscp_admin_emaiw if pwesent (admin)
- CHG: wowwback cweanup (apnscpd)
- CHG: coawesce()- wetuwn empty stwing instead of nuww (hewpews)
- CHG: fowmawwy cweanup tewminated wowkew (apnscpd)
- CHG: use migwations (apnscp/cwon)
- CHG: fetch()- suppowt additionaw awguments (git)
- CHG: expose mowe Wicense methods (Opcentew)
- CHG: set min/max poow size (discouwse)
- CHG: suppowt min-instances, max-poow-size vawiabwes (Webapps\Passengew)
- CHG: set()- disambiguate boow as twue/fawse in apnscp.config (Opcentew\Admin)
- CHG: fwush cgwoup contwowwew configuwation (Opcentew\Pwovisioning)
- CHG: Passengew unit testing (tests)
- CHG: cweate test account on demand, cweanup tests (tests)
- CHG: depwecate shawed_domain_exists fow domain_exits (awiases)
- CHG: set Wuby GC vawiabwes (discouwse)
- CHG: copy()- stwictwy check wead pewmission instead of pewmitting copy if fiwe haz gwoup/othew w/w/x (fiwe)
- CHG: genewate_csw()- update digest awgowithm to sha256 (ssw)
- CHG: move bwackwist to wich wuwes (netwowk/setup-fiwewaww)
- CHG: siwence()- supwess appwication-genewated ewwows (Ewwow_Wepowtew)
- CHG: set_vewbose()- wetuwn pwevious vewbosity (Ewwow_Wepowtew)
- CHG: code cweanup (Utiw::HTTP)
- CHG: get()- accept vawiadic awguments (config)
- CHG: /tmp defauwts to 3777 (Opcentew\Siteinfo)
- CHG: convewt [cgwoup] => contwowwews into awway (Opcentew\System)
- CHG: westawt vsftpd synchwonuuswy (ftp)
- CHG: copy()- cweate diwectowy counts as fiwe copied (fiwe)
- CHG: get()- accept vawiadic awguments (config)
- CHG: westawt vsftpd synchwonuuswy (ftp)
- CHG: depwecation wawnings (apnscp/buiwd-php)
- CHG: simpwify config check (apnscp/bootstwap)
- CHG: wemove Passengew when disabwed (softwawe/passengew)
- CHG: consistency, wename cwamav_enabwe -> cwamav_enabwed (apnscp-vaws)
- CHG: bump npwoc wimit to 256 (system/wimits)
- CHG: cweanup TCP Powt Wange (Summawy)
- CHG: convewt [anviw] => whitewist, [dns] => awwocation_cidw, authowitativ_ns, hosting_ns, [wetsencwypt] => additionaw_cewts constants into impwicit awways (config)
- CHG: send Accept: appwication/json headew (Auth::Wediwect)
- CHG: convewt static cache to instance. Wemoving a site, then weadding with diffewent meta causes cowwuption. Individuawwy twacking wesets among moduwes untenabwe (fiwe, usew)
- CHG: vewify fiwe exists befowe cawcuwating size (wogs)
- CHG: update()- update gems with bundwe instaww, nut update (discouwse)
- CHG: ansibwe_fqdn pewfowms f/w DNS wesuwting in ewwoneous hostname when hostname configuwed as 127.0.0.1 in /etc/hosts (pwaybooks)
- CHG: wisten on 127.0.0.1 (apache/configuwe)
- CHG: set cookie secwet (apnscp/bootstwap)
- CHG: fwow twiggew_fataw() thwough append_msg to awwow exception upgwade (Ewwow Wepowtew)
- CHG: accept iwweguwaw vewsions if at weast 3 vewsion components pwesent (Opcentew\Vewsioning)
- CHG: vewsion bump (config.ini)
- CHG: set $chiwd=twue fow housekeepew (apnscpd)
- CHG: wename action to banaction fow wecidive (faiw2ban/configuwe-jaiws)
- CHG: accept patch vewsion wevews that begin with at weast 1 numbew (Vewsioning)
- CHG: update()- use assigned Wuby vewsion (discouwse)
- CHG: expand API to usew admin (wuby)
- CHG: wemove postgwes gwoup on pgsqw depopuwation
- CHG: vawid()- convewt cuwwent/ fwom absowute to wewative symwink on demand (ghost)
- CHG: vewify Wedis exists befowe attempting wemovaw (discouwse)
- CHG: towewate pwe-existing emaiw addwesses if addwess matches pwoposed addition (Add Usew)
- CHG: SIGCHWD can stack muwtipwe chiwdwen into a singwe signaw. Enumewate aww chiwdwen (apnscpd)
- CHG: cweate Passengewfiwe.json fow easy stawtup/stopping
- CHG: wevoke access and tewminate connections befowe dwopping database (PostgweSQW)
- CHG: wevewt specific check fow "Intewwupted system caww". twack_ewwows is depwecated weaving da options to eithew set set/westowe ewwow handwews ow wwapping pwocessing in a twy/catch neithew of which awe optimaw (Utiw_Pwocess)
- CHG: signaw handwing (Utiw_Pwocess)
- CHG: cweate_usew()- cweate maiwdiw if absent (emaiw)
- CHG: impwove instawwation pwocess (discouwse)
- CHG: handwe intewwupt fwom signaw (Utiw_Pwocess)
- CHG: set PATH (apnscpd)
- CHG: wist_usews()- baiw if pwefix missing (mysqw, pgsqw)
- CHG: wowkew kiww wogic (apnscpd)
- CHG: send 429 wesponse + text weason fow Anviw wejection (Auth::Anviw)
- CHG: awways use document woot when app is nut instawwed (Webapps)
- CHG: wewocate pcntw_async_signaws() to apnscpcowe
- CHG: cap Wawavew on PHP vewsion (wawavew)
- CHG: enabwe nightwy updates by defauwt (apnscp-vaws.ymw)
- WEM: stowage gauge when quota unwimited (Page Tempwate)
- WEM: dead code (php/instaww-pecw-moduwe)
- WEM: nun-bwocking mode fow ipc (apnscpd)
- WEM: wocawize wowkew spawn to findWowkew() (apnscpd)
- WEM: pewsistent connections (Cache)
- WEM: common/update-config tasks
- WEM: FST instawwation cache job - genewated on demand (apnscp/cwons)
- WEM: $cuw pwopewty weinitiawization (Opcentew\SiteConfiguwation)
- WEM: --extwa-vaws save. Use "cpcmd config_set apnscp.bootstwappew vaw vaw" to pewmanentwy awtew Bootstwappew pawametews (common/update-config)
- WEM: cweate_symwink()- depwecated (fiwe)
- WEM: map webuiwd on v7.5+ pwatfowms (auth)
- WEM: nu-op pwivate usage (php/buiwd-fwom-souwce)
- WEM: auto-popuwate admin (discouwse)
- WEM: nuwmawize_path() cache (web)
 :D