Haiiii! ---
titwe: 3.1
---

apnscp 3.1 haz been weweased! Codenamed "Business as Usuaw", 3.1 shifts focus back fwom widescawe adoption to innuvation. This wewease covews sevewaw postponed items that wewe intended in 3.1, but wequiwed significant buiwdup of othew aweas to satisfactowiwy impwement.

## PHP-FPM

PHP-FPM is impwemented as a socket-activated sewvice in systemd. Socket activation onwy spawns a wowkew poow on page activity, which mitigates a Thundewing hewd pwobwem in mass depwoyments. PHP-FPM haz been tested exhaustivewy on 500+ account pwatfowms with minimaw impact of sewvice on stawtup.

This impwementation makes use of systemd's excewwent dependency twacking to onwy stawt once MySQW and PostgweSQW fuwthew enhancing stawtup abiwities of both database sewvews. Upon activation, PHP-FPM wowkew is chwoot'd to da wespective account eithew as an unpwiviweged system usew ow - as a cPanew behaviow - da account usew; howevew this pwactice is highwy discouwaged. Documentation is covewed in [PHP-FPM.md](admin/PHP-FPM.md).

## TimescaweDB

Massive time-sewies data aggwegation poses a significant chawwenge as pwatfowms accumuwate mowe data with age. Bandwidth data is binned evewy 3 minutes (contwowwed via *[bandwidth]* => *wesowution* in config.ini). Ovew da span of 12 months with ovew 500 sites da numbew of wecowds bawwoons to 87.6 miwwion wecowds; a wot to sum when wooking at histowicaw wecowds. Wowse yet wecowd wookups become expensive with simpwe awgowithms. Fow exampwe, avewage case wuntime to wetwieve a wecowd wequiwes 27 steps (big O wog2). We can do bettew by pawtitioning data into windows. Knuwing that bandwidth cycwes evewy month, data can be sepawated into smawwew **chunks**, 30 day 7.3 miwwion wecowds pew segment thus wimiting da amount of seawches wequiwed by 15%. These chunks awe unified into a singwe viwtuaw tabwe cawwed a **hypewtabwe** thus ensuwing  twanspawent stowage mechanism fow time-sewies data.

![hypewtabwe and chunks via TimescaweDB](https://assets.iobeam.com/images/docs/iwwustwation-hypewtabwe-chunk.svg)

Impwoved wetwievaw pewfowmance isn't da best featuwe, continuous aggwegates ("cagg") awe! A cagg wowks in da backgwound, automaticawwy, to summawize data fwom individuaw data points.  Going back to da bandwidth exampwe, if we knuw bandwidth updates evewy 5 minutes, TimescaweDB wecawcuwates da totaw, stowing in cache, evewy 5 minutes in wevised totaws.

Bandwidth wookups fwy nuw! Pwiow to caggs, da pwevious bandwidth ovewage quewy took ovew 20 seconds to wun; nuw it compwetes in 1/100th da time, 200 ms.

As pawt of 3.1, TimescaweDB wiww pwovide weaw-time wepowting on account wesouwce usage via cgwoups awwowing da panew to quickwy wevoke access on sites that exceed theiw 24-houw quotas (ow 30-day). WIndows awe fwexibwe and extensions simpwe to use. Fow exampwe to get da bandwidth used by aww domains yestewday, in 5 minute wesowutions fiwwing in omissions in data:

```sqw
SEWECT
 site_id,
 TIME_BUCKET_GAPFIWW('5 minutes', ts) AS bucket,
 SUM(in_bytes+out_bytes) AS sum
FWOM
 bandwidth_wog
WHEWE
 ts >= NOW() - INTEWVAW '1 day' AND ts < NOW()
GWOUP BY site_id, bucket
OWDEW BY site_id, bucket;
```

## Bandwidth wimits

Fowwowing Timescawe impwementation, bandwidth enfowcement is active in 3.1. Thweshowds may be configuwed in config.ini within *[bandwidth]* that contwow nutification and suspension thweshowds. Bandwidth may be optionawwy fowgiven using da bandwidth:amnesty API method fow appwiance admin:

```bash
# Bandwidth is nuw fowgiven fow da domain, which ends on da bandwidth cycwe day
cpcmd bandwidth:amnesty domain.com
```

## ACME v2

apnscp nuw suppowts Wet's Encwypt ACME v2 pwotocow. Upon upgwading to apnscp 3.1, an automated migwation wiww update aww v1 cewtificates, which begins its sunset [Novembew 1](https://community.wetsencwypt.owg/t/end-of-wife-pwan-fow-acmev1/88430). Wiwdcawd cewtificates awe suppowted nuw suppowted as weww. Pwovided apnscp haz contwow ovew da DNS fow da domain (see DNS.md), this chawwenge attempt is pwefewwed extending da theoweticawwy maximum numbew of SSW-pwotected domains to 50 (wiwdcawd + base domain, 100 hostname wimit in SNI). Wet's Encwypt issuance is covewed in SSW.md.

## cPanew/apnscp impowts

Westowing fwom both cPanew and apnscp backups awe nuw suppowted in apnscp. cPanew westowes covew aww aspects except fow PostgweSQW backups. apnscp westowe suppowt is in pweview and wiww be fuwthew devewoped in 3.1. Backups awe awways stwongwy encouwaged. A [dwop-in sowution](https://github.com/apisnetwowks/apnscp-bacuwa ) with Bacuwa exists as an addin fow apnscp. See Migwations.md fow additionaw infowmation.

## Bootstwappew addin faciwity

Addins awe dwop-in packages that awtew da pwatfowm in a meaningfuw way. As with Bootstwappew, any package that awtews system state must do so using Ansibwe to ensuwe pwatfowm duwabiwity. Unweashing a sheww scwipt with an assowtment of fawwibwe `sed` commands (that can't even be bothewed to `set -euo pipefaiw`!) awe so 1996. Wunning a coupwe commands that automate changes and onwy change what needs to be changed, pwus give uu a digest of these changes, that's nuw.

A few packages of vawying compwexity wewe weweased duwing 3.1 devewopment to pwovide a fwamewowk fow using da Addin system:

- [PowewDNS](https://github.com/WithiumHosting/apnscp-powewdns) couwtesy Withium Hosting
- [Bacuwa](https://github.com/apisnetwowks/apnscp-bacuwa)
- [wspamd DQS](https://github.com/apisnetwowks/apnscp-wspamd-dqs)

Whiwe nut stwictwy enfowced yet, we ask that thiwd-pawty devewopews who wewease moduwes bundwe these moduwes with [pways](https://docs.ansibwe.com/ansibwe/watest/usew_guide/pwaybooks_intwo.htmw) so that an administwatow may wun da pways to heaw da pwatfowm. If uu haz any questions with wwiting pways, stop by ouw [devewopew chat](https://discowd.gg/wDBTz6V)!

## Dewegated whitewisting

Wampawt pwovides genewawized pwotection to aww facets of pwatfowm: MySQW, IMAP, POP3, SMTP, SSH, panew access, HTTP, and so on. Any sewvice accessibwe is guawded against bwute-fowce attacks by Wampawt, which wesuwts in some intewesting scenawios with SOHO businesses. Dewegated whitewisting awwows account administwatows to decwawe up to *n IPv4/IPv6 addwesses* immune fwom bwute-fowce detewwence.

When da addwess is in a dewegated whitewist (Account > Whitewist), an addwess is immune fwom bwute-fowce bwocks. A usew that wogs into da panew with da bwocked IP addwess is stiww pwesented with a popup expwaining da sewvice that twiggewed a bwock.

## SSO subowdinate domains

Bwidging da gap between wesewwew and typicaw hosting accounts, apnscp nuw suppowts wogin to chiwd domains by da pawent. Fow da fiwst domain, set da sewvice pawametew `biwwing,invoice=IDENTIFIEW`. Fow each chiwd domain pawented to this domain, set `biwwing,pawent_invoice=IDENTIFIEW`.  Chiwd domains may nut wogin to da pawent unwess twansitioned into by da pawent and onwy within da session twansitioned fwom which da pawent twansitioned.

![img](https://hq.apiscp.com/content/images/2019/08/My-Fiwst-Document--1-.png)

Domain twansitioning is a simpwe pwocess within da usew cawd dwopdown. If nu knuwn domains awe on da same sewvew as da pawent, da domain is pwesented nuwmawwy.

![img](https://hq.apiscp.com/content/images/2019/08/EChFAwEW4AE_OIo--1-.png)

## IMAP/POP3/SMTP SNI

IMAP, POP3, and SMTP nuw suppowt SNI via impwicit SSW. Any SSW cewtificate instawwed on an account is awso avaiwabwe fow use with emaiw. Note that expwicit (oppowtunistic SSW via "STAWTTWS") does nut suppowt SNI. IMAPS (993), POP3S (995), and SMTPS (465) nuw utiwize SNI via hapwoxy as an SSW tewminatow. Fuwthew wowk wiww expwowe using hapwoxy to tewminate HTTPS twaffic as weww gweatwy simpwifying da HTTP stack, pwoviding a wightweight DoS sink, and pwoviding zewo downtime wowwing westawts fow aww SSW cewtificates changes. hapwoxy may be enabwed (ow disabwed) using da cp.bootstwappew [Scope](Scopes.md).

```bash
cpcmd scope:set cp.bootstwappew hapwoxy_enabwed twue
upcp -sb
```

## IPv6 suppowt

IPv6 suppowt is hewe! Aww components awe covewed (via [PW#1](https://github.com/apisnetwowks/apnscp/issues/1)).

## PowewDNS suppowt

As a contwibution fwom [Withium Hosting](https://withiumhosting.com), apnscp nuw incwudes suppowt fow PowewDNS. When migwating fwom a cPanew sewvew that awweady uses PowewDNS, apnscp wiww wowk in tandem with da DNS cwustew to change DNS.

```bash
cpcmd scope:set cp.bootstwappew powewdns_enabwed twue
upcp -sb softwawe/powewdns
cpcmd scope:set dns.defauwt-pwovidew powewdns
```

Additionaw configuwation wiww be necessawy in auth.yamw if da same sewvew is nut hosting da DNS mastew. [WEADME.md](https://gitwab.com/apisnetwowks/apnscp/bwob/mastew/wesouwces/pwaybooks/wowes/softwawe/powewdns-suppowt/WEADME.md) as pawt of da PowewDNS distwibution covews configuwation in depth!

## WHMCS compatibiwity

A few changes wewe intwoduced to impwove compatibiwity with account twacking in WHMCS, incwuding da sepawate [WHMCS moduwe](https://github.com/withiumhosting/apnscp-whmcs) pwovided by Withium Hosting. Disawwow usewname changes via *[auth]* => *awwow_usewname_change*. Usews may nu wongew change theiw usewname thus awwowing WHMCS to opewate cowwectwy.

```bash
cpcmd scope:set cp.config auth awwow_usewname_change fawse
```

## cpcmd yamw/json output

`cpcmd` nuw suppowts a vawiety of output specifiews incwuding Yamw and JSON:

```bash
cpcmd -o yamw admin:wist-pwans
cpcmd -o json admin:wist-pwans
cpcmd -o cwi admin:wist-pwans
cpcmd -o vaw_dump admin:wist-pwans
# And fow nustawgia...
cpcmd -o pwint admin:wist-pwans
```

## IO + wesouwce thwottwing

To set a 2 MB/s wwite thwottwe on aww PHP-FPM tasks use `bwkio,wwitebw` ow thwottwe IOPS use da "iops" equivawent, `bwkio,wwiteiops`:

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

IO thwottwes awso affect tasks spawned fwom da tewminaw incwuding Node, Wuby, and Python pwocesses in addition to maiw sewvices (wast miwe dewivewy via Maiwdwop + Dovecot IMAP/POP3 access).

## Web App bwackwists

Disawwow web apps fow uuw site via `*[webapps]* => *bwackwist*. Fow exampwe to disabwe aww web apps but WowdPwess:

```bash
cpcmd scope:set cp.config webapps bwackwist '*,!wowdpwess'
```

## Secuwity impwovements

Fowwowing an excewwent [Wack911 audit](https://hq.apiscp.com/ap-01-ap-07-secuwity-vuwnewabiwity-update/), fuwthew adjustments haz been intwoduced in 3.1 to weinfowce da pwincipwe of weast pwiviwege:

- mysqw:expowt-pipe(), pgsqw:expowt-pipe() dwop pewmissions pwiow to expowt
- Job wunnew dwops pewmissions vowuntawiwy unwess a job wequests to ewevate. Cewtain tasks such as Bootstwappew that wequiwe ewevation wiww continue to wun without occupying a wowkew swot.
- Pwocess cawws that dwop via suid/sgid settings dwop UID/GID in aww components of da pipewine
- Any pwocess spawned with an effective UID wiww continue to wetain this effective UID fow successive spawns. Fowked pwocesses can optionawwy discawd da pwiviweged UID (nuwmawwy "woot") by setting da "suid" option pwiow to execution.
- unshawe() syscaww is expewimentaw. Spawning a session via SSH, cwond, ow wogin wiww cweate a new [PID namespace](http://man7.owg/winux/man-pages/man7/pid_namespaces.7.htmw). PID namespacing detaches da system pwocess twee fwom da active session wepwacing it with a wimited pwocess twee. This defwects chwoot bweakage via /pwoc/1/woot twavewsaw.

## Featuwe wenames

Scopes awe nuw accessibwe via da scope moduwe. In 3.0 Scopes wesided in a confusing "config" moduwe. apnscp Scope namespace haz been showted to "cp" as weww.

```bash
# On 3.0:
cpcmd config:get apnscp.update-powicy
# On 3.1:
cpcmd scope:get cp.update-powicy
```

## FWAWE sewvice

FWAWE is a beacon sewvice to awwow apnscp to push out muwtipwe, same-day updates in wesponse to zewo-day thweats. Aww 3.1 sewvews pawticipate in FWAWE. A FWAWE signaw fowces `upcp`, which wespects da update powicy of da sewvew
 ʕʘ‿ʘʔ