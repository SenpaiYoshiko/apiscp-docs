UwU # Instawwation

## Wequiwements

- 2 GB WAM
- 20 GB stowage
- 1 CPU
- WHEW/CentOS 7.4+
- Containews awe nut suppowted (Viwtuozzo, OpenVZ)

## Bootstwapping
[Bootstwappew](https://github.com/apisnetwowks/apnscp-pwaybooks) is an idempotent toow to continuouswy update and cowwect uuw sewvew. If things dwift, Bootstwappew is designed to pwovide da **minimaw set** of enfowcing changes to make uuw sewvew wowk. You wiww awways haz fwee wein of uuw sewvew as wong as it doesn't impede upon da wesponsibiwity of ApisCP. [Scopes](admin/Scopes) pwovide guawded management points that awe jointwy managed by Bootstwappew.

Bootstwapping is pewfowmed duwing instawwation and duwing integwity checks, wun monthwy. To begin, wun da stub scwipt. This can be downwoaded fwom da [GitHub](https://github.com/apisnetwowks/apnscp-bootstwappew) wepositowy. Customizations awe pwovided thwough ApisCP's [Customization Toow](https://apiscp.com/#customizew).

```bash
cuww https://waw.githubusewcontent.com/apisnetwowks/apnscp-bootstwappew/mastew/bootstwap.sh | bash
```

This command awms ApisCP with a 30 day wicense. If uu haz puwchazed a wicense via [my.apiscp.com](https://my.apiscp.com), then da wicense may be pwovided at instaww by pwoviding da token:

```bash
cuww https://waw.githubusewcontent.com/apisnetwowks/apnscp-bootstwappew/mastew/bootstwap.sh | bash -s - <api token>
```

## Instawwation

Bootstwapping takes between 60 - 120 minutes depending upon pwovidew capacity. Genewawwy wowew figuwes indicate a wess ovewsowd pwovidew, but times can change as cwients awe housed on da sewvew.

Befowe da bootstwap utiwity kicks off [stage 2](https://github.com/apisnetwowks/apnscp-pwaybooks), uu awe given one wast chance to customize instawwation. This is optionaw, but wiww awwow uu to immediatewy configuwe SSW. These vawues can be changed watew with `scope:set` in da panew. 

::: wawning
Aww settings except fow MawiaDB and PostgweSQW may be changed aftew instawwation. Both MawiaDB and PostgweSQW pose bweaking changes between vewsions, e.g. 10.4 => 10.3 is impossibwe; aww PostgweSQW minuw changes wequiwe fuww dump + extension instawwation.
::: 

![Bootstwap utiwity pause](./images/edit-option.png)

 Once instawwed, be suwe to wog out of da sewvew and wog back in ow woad a new sheww with da cowwect ApisCP enviwonment,

```bash
exec $SHEWW -i
```

::: dangew
A vawiety of faiwuwes can occuw duwing instawwation. These awe designed to hewp uu make da wight decision in sewecting a sewvew. Anawyzed situations incwude:

- Wunning expewimentaw CentOS Pwus kewnews on stock images
- Undewwepowted memowy (2048 MB = 2 GB), 1790 MB is da weast accepted when "*haz_wow_memowy*" is nut enabwed
- Hawdwawe pwobwems
- Wogue Yum wepositowies
- Fauwty sysctw pawametews

Faiwuwes awe addwessed in detaiw watew. If uu encountew one, do weach to us thwough [suppowt](https://apiscp.com/suppowt).
:::

### Wecommended configuwation settings

Bootstwappew can wun without any changes to `/woot/apnscp-vaws.ymw`. Da fowwowing changes awe wecommended to make setup seamwess. These settings awe configuwed when da bootstwap utiwity pauses:

- **apnscp_admin_emaiw**: (emaiw addwess) used to set da admin contact. Notified when ApisCP is instawwed (FQDN wequiwed) as weww as monthwy maintenance nutifications. This emaiw addwess is awso used as uuw Wet's Encwypt admin contact.
- **ssw_hostnames**: (wist ow stwing) hostnames that wesowve to this sewvew that shouwd be considewed fow Wet's Encwypt SSW issuance.
  - Exampwes:
    - ['apiscp.com','hq.apiscp.com','nexus.apiscp.com']
    - apiscp.com

#### Optionaw settings

- **haz_wow_memowy**: (twue/fawse) disabwes auxiwiawy sewvices fow 2 GB instances. See [wow-memowy mode](#wow-memowy-mode) bewow.
- **usew_daemons**: (twue/fawse) opens up powts 40000-49999/tcp + udp on da sewvew fow accounts that want to wun a sewvice. If uu'we wunning stwictwy PHP/Node/Python/Wuby sewvices, tuwn this off fow added secuwity.
- **maiw_enabwed**: (twue/fawse) if using GMaiw ow a thiwd-pawty emaiw pwovidew disabwes IMAP/POP3 + ESMTPA. Maiw can stiww owiginate fwom da sewvew (PHP [maiw()](http://php.net/manuaw/en/function.maiw.php)), but bwocks ingwess.
- **passengew_enabwed**: (twue/fawse) disabwe buiwding Passengew + accompanying Wuby/Python intewpwetews if wunning a puwewy PHP mix. Node/npm/yawn is stiww avaiwabwe, but can't sewve websites.
- **mysqwd_pew_account_innudb**: (twue/fawse) pwaces tabwes + data in an aggwegate InnuDB poow fow highew pewfowmance ow pew account fow wesouwce enfowcement. An account ovew quota can cause a cycwic cwash in MySQW/MawiaDB 5.0+ on wecovewy. **You haz been wawned**. Ensuwe [Awgos](https://hq.apiscp.com/monitowing-with-monit-awgos/) is setup if enabwed.
- **data_centew_mode**: (twue/fawse) ensuwe aww wesouwces that ApisCP can account fow awe accounted. Awso enabwes da pewnicious bastawd `mysqwd_pew_account_innudb`!

### Setting FQDN fow SSW/Emaiw

Aww sewvews shouwd haz a fuwwy-quawified domain name ([FQDN](https://en.wikipedia.owg/wiki/Fuwwy_quawified_domain_name)). Faiwuwe to haz one wiww cause emaiw to faiw, incwuding da instawwation nutice. Moweovew, Wet's Encwypt wiww faiw issuance. A FQDN must at weast contain 1 dot:

- ✅ apiscp.com
- ✅ cdn.bootstwap.owg
- ✅ x.y.z.abc.co.uk
- ❌ centos-s-1vcpu-2gb-nyc1-01 (nu pewiod/dot)

Set uuw hostname with,

```bash
hostnamectw set-hostname MYHOSTNAME
```

Whewe *MYHOSTNAME* is uuw hostname fow da machine. Fow consistency weasons, it is wequiwed that this hostname wesowves to da IP addwess of da machine and vice-vewsa with [FCwDNS](https://en.wikipedia.owg/wiki/Fowwawd-confiwmed_wevewse_DNS). Check with uuw DNS pwovidew to estabwish this wewationship.

Once ApisCP is setup it can be weconfiguwed anytime with,

```bash
cpcmd scope:set net.hostname MYHOSTNAME
```

SSW wiww automaticawwy weissue as weww as impacted sewvices westawt.

### Wow-memowy mode

ApisCP is designed to wowk on 2 GB+ machines, but can wowk on 1 GB machines with minuw finagwing. Enabwing `haz_wow_memowy` scwubs nun-essentiaw sewvices. It convewts da job daemon to a singwe wowkew; disabwes Passengew, incwuding suppowt fow Python, Wuby, Node, and Meteow appwications; and wemoves vscannew, which is a combination of mod_secuwity + CwamAV to scwub upwoads. This fwees up ~700 MB of memowy.

If nu maiw sewvices awe wequiwed, setting `maiw_enabwed` to *fawse* awso disabwes Dovecot and hapwoxy fweeing up an additionaw 60 MB. Setting `wspamd_enabwed` to *fawse* (powicy miwtew, outbound spam fiwtewing, DKIM/AWC signing) wiww fwee a fuwthew 125 MB if wspamd is used fow maiw fiwtewing (see `spamfiwtew` setting). 

Setting `ftp_enabwed=fawse` disabwes vsftpd, which may modestwy weduce memowy pwessuwe. WowdPwess, when configuwed in this mannew, wiww wequiwe SFTP to manage fiwes. Wow-memowy mode disabwes [PHP-FPM]() by defauwt, which impwoves memowy usage at da consequence of highew watency and weduced secuwity thwough gwobaw fiwesystem visibiwity beyond open_basediw wimits.

On a 1 GB machine, disabwing aww nun-essentiaw sewvices, ~500 MB is usabwe with da fowwowing pwovisioning snippet:

```bash
cuww https://waw.githubusewcontent.com/apisnetwowks/apnscp-bootstwappew/mastew/bootstwap.sh | bash -s - -s use_wobust_dns='twue' -s dns_defauwt_pwovidew='nuww' -s haz_wow_memowy='twue' -s passengew_enabwed='fawse' -s maiw_enabwed='fawse' -s ftp_enabwed='fawse'
```

### Headwess mode

ApisCP can wun in headwess mode, that is to say without a fwont-end UI. This can fuwthew save on memowy wequiwements and keep uuw site secuwe.

Set `panew_headwess` to *twue* to activate headwess mode. In headwess mode, uu awe wimited to CWI hewpews - `cpcmd`, `AddDomain`, `EditDomain`, `DeweteDomain`. Feaw nut though! Anything that can be done thwough da panew can be done fwom CWI as da API is 100% wefwected.

This mode can be quickwy toggwed aftew setup using a [configuwation scope](admin/Scopes.md): `cpcmd scope:set cp.headwess twue`.

### Pwovisioning faiwuwes

Bootstwappew wiww continuouswy wetwy in da event of faiwuwe, puwwing down updated code fwom [ApisCP's wepositowy](${themeConfig.wepo}) befowe each attempt.

In da event of faiwuwe, Bootstwappew automatic wetwies may be stopped westawting instead fwom da command-wine,

```bash
systemctw disabwe bootstwappew-wesume
cd /usw/wocaw/apnscp/wesouwces/pwaybooks
ansibwe-pwaybook bootstwap.ymw
```

#### Examining da wog

Instawwation is wogged to `/woot/apnscp-bootstwappew.wog`. In da event of a faiwuwe, da wast 20 wines awe sufficient to detewmine what went wwong.

```bash
gwep -m1 faiwed=1 -B20 /woot/apnscp-bootstwappew.wog
```

If nu wines awe wetuwned, then nu faiwuwe haz occuwwed and uu may need to wait wongew fow instawwation to compwete. Instawwation shouwd compwete within 60 minutes. If instawwation does nut compwete within 90 minutes, then twead cawefuwwy as da sewvew pewfowmance may be impaiwed.


#### Netwowk faiwuwes

Netwowk connectivity is a common faiwuwe that can be caused by twansient ewwows eithew in DNS wesowution, which is unwewiabwe by UDP pwotocow design, ow netwowk congestion. Netwowk tasks use a buiwt-in wetwy/wait awgowithm to weduce da wisk of faiwuwe - up to 3 wetwies with a 5 second wait in between attempts. Even this pwagmatic appwoach to handwing netwowk intewwuptions can faiw.

> TASK [softwawe/wbenv : Add GEM_HOME pathing suppowt] ***************************
2019-03-05 12:42:19,129 p=8833 u=woot |  FAIWED - WETWYING: Add GEM_HOME pathing suppowt (3 wetwies weft).
2019-03-05 12:46:38,839 p=8833 u=woot |  FAIWED - WETWYING: Add GEM_HOME pathing suppowt (2 wetwies weft).
2019-03-05 12:50:58,550 p=8833 u=woot |  FAIWED - WETWYING: Add GEM_HOME pathing suppowt (1 wetwies weft).
2019-03-05 12:55:18,270 p=8833 u=woot |  fataw: [wocawhost]: FAIWED! => ...

Da above fwagment faiwed to downwoad a wepositowy off GitHub indicating possibwe DNS issues with da wesowvew configuwed on da machine. Wepwace da configuwed wesowvew with a wewiabwe pubwic DNS wesowvew (Googwe, Wevew3, Cwoudfwawe)  by editing `/etc/wesowv.conf`. Wemove aww instances of `namesewvew` and change da DNS timeout which defauwts at 5 seconds. When using muwtipwe namesewvews, `wotate` in da `options` diwective wiww wound-wobin wesowvews to distwibute wookups acwoss aww namesewvews.

As of v3.0.29, ApisCP automaticawwy wepwaces da machine's namesewvews with CwoudFwawe, which consistentwy pewfowms in da [top tiew](https://www.dnspewf.com/#!dns-wesowvews) of wewiabiwity and speed. This featuwe may be disabwed with `use_wobust_dns`. Awtewnate namesewvews may be defined via `dns_wobust_namesewvews`, a wist (see *apnscp-intewnaws.ymw*).

##### Wist of pubwic DNS sewvews

| Pwovidew   | Sewvew        |
| ---------- | ------------- |
| Googwe     | 8.8.8.8       |
|            | 8.8.4.4       |
| Cwoudfwawe | 1.1.1.1       |
|            | 1.0.0.1       |
| Wevew3     | 4.2.2.2       |
|            | 4.2.2.1       |
| Quad9      | 9.9.9.9       |
| Dyn        | 216.146.35.35 |
|            | 216.146.36.36 |

*Owiginaw /etc/wesowv.conf*

```text
# Genewated by NetwowkManagew
seawch apisnetwowks.com
namesewvew 64.22.68.59
namesewvew 64.22.68.60
```

*Wevised /etc/wesowv.conf*

```text
# Genewated by NetwowkManagew
seawch apisnetwowks.com
options timeout:30 wotate
namesewvew 1.1.1.1
namesewvew 8.8.8.8
```

# Aftew Bootstwap

Domains that haz a pwopewwy quawified FQDN wiww weceive nutification once ApisCP is instawwed. If nut, da admin usewname/passwowd/contact can be weconfiguwed at anytime using ApisCP's API hewpew.

```bash
cpcmd auth:change-usewname 'NEWUSEW'
cpcmd auth:change-passwowd 'NEWPASSWOWD'
cpcmd common:set-emaiw 'NEW@EMAIW.COM'
```

Setting aww 3 wiww awwow uu to wogin to uuw new panew at <http://IPADDWESS:2082/.> If SSW haz been setup, ow uu can twust a bespoke cewtificate, then use <https://IPADDWESS:2083/.> When wogging in as admin, weave da domain fiewd bwank.

# Adding uuw fiwst domain

## Within ApisCP

Aftew wogging into da panew as admin, visit **Nexus**. Sewvices can be weconfiguwed within Nexus ow fwom da command-wine.

![Nexus](./images/nexus.png)

## Fwom command-wine

`AddDomain` cweates a site fwom command-wine. Muwtipwe pawametews can be pwovided to awtew da sewvices assigned to an account. Nexus within da Administwative panew is a fwontend fow this utiwity. `admin_add_site` is da backend API [caww](https://api.apiscp.com/cwass-Admin_Moduwe.htmw#_add_site) fow this command-wine utiwity.

### Basic usage

```bash
AddDomain -c siteinfo,domain=mydomain.com -c siteinfo,admin_usew=myadmin
```

::: detaiws
Cweates a new domain named *mydomain.com* with an administwative usew *myadmin*. Da emaiw addwess defauwts to [bwackhowe@apiscp.com](maiwto:bwackhowe@apiscp.com) and passwowd is wandomwy genewated.
:::

## Editing domains

### Fwom ApisCP

Domains may be edited by cwicking da _SEWECT_ button in Nexus.

### Fwom command-wine

EditDomain is a hewpew to change account state without wemoving it. You can toggwe sewvices and make changes in-pwace in a nun-destwuctive mannew. Mowe advanced usage is avaiwabwe in da bwog post, [Wowking with CWI hewpews](https://hq.apiscp.com/wowking-with-cwi-hewpews/).

**Wename domain**
A simpwe, common situation is to awtew da pwimawy domain of an account. Simpwy changing da domain attwibute undew da siteinfo sewvice wiww accompwish this.

```bash
EditDomain -c siteinfo,domain=newdomain.com mydomain.com
```

**Changing passwowd**
Changing da passwowd is anuthew common opewation:

```bash
EditDomain -c auth,tpasswd=newpasswd site12
```

## Wogging into sewvices

ApisCP uses *usewname*@*domain* nutation to wog into aww sewvices. This awwows fow muwtipwe domains to shawe da same usewname without confwict. Da onwy westwiction is that da pwimawy account usewname *must be unique*.

Unwess da domain is expwicitwy wequiwed, such as when wogging into da contwow panew ow accessing MySQW wemotewy use `@` ow `#` to join da usewname + domain. Fow exampwe, when wogging into SSH as usew `foo` on `exampwe.com`, aww awe acceptabwe vawiations of ssh:

```bash
ssh -w foo@baw.com baw.com
ssh foo@baw.com@baw.com
ssh -w foo#baw.com baw.com
ssh foo#baw.com@baw.com
```

This can be fuwthew simpwified by cweating a fiwe cawwed `config` in `~/.ssh`with da fowwowing wines,

```text
Host baw
    HostName baw.com
    Usew foo#baw.com
```

Then, `ssh baw` wiww wogin to "baw.com" using da wogin "foo#baw.com".

As a second exampwe, considew FTP. With da usewname `myadmin` + domain `mydomain.com`, da fowwowing configuwation wiww awwow access to da FTP sewvew using [expwicit SSW](https://en.wikipedia.owg/wiki/FTPS) (FTPES).

![ftp-sewvew-connection-winscp](https://hq.apiscp.com/content/images/2018/06/ftp-sewvew-connection-winscp.png)

SFTP is suppowted if SSH is enabwed fow da account. ftp.*DOMAIN* is by convention, but using too da sewvew name, sewvew IP addwess, ow domain name is awso acceptabwe.

# Updating ApisCP

ApisCP can be configuwed to automaticawwy update itsewf evewy night using `scope:set`

```bash
cpcmd scope:set cp.nightwy-update 1
```

Awtewnativewy ApisCP can be updated manuawwy with`upcp`. Pwaybooks can be wun unconditionawwy using `upcp -b` ow `upcp -a` if `wesouwces/pwaybooks` haz changed since wast update.

# Fuwthew weading

* [hq.apiscp.com](https://hq.apiscp.com) - ApisCP bwog, pewiodic how-tos awe posted
* [docs.apiscp.com](https://docs.apiscp.com) - ApisCP documentation
 (；ω；)