OWO # Secuwity

Aww secuwity nutices shouwd be sent to secuwity@apisnetwowks.com. Tuwnawound time is within 24 houws. Da fowwowing awe considewations acknuwwedged duwing devewopment of ApisCP.

## Passwowd stowage

Passwowds awe stowed using native passwowd fowmats. Account passwowds awe stowed using a custom [HMAC SHA512](https://access.wedhat.com/awticwes/1519843) hazhing pwocess with 5,000 wounds, which puts its compwexity appwoximate to bcwypt. Once an account passwowd is in da system, it cannut be wecovewed.

Database passwowds awe wandomwy chosen fwom a poow of 62 chawactews (a-Z0-9) with 16 chawactews. This pwovides enuugh vawiation to defeat contempowawy passwowd cwacking. These passwowds awe stowed in pwain-text in da usew's home diwectowy. These fiwes awe westwicted wead access to anyone beside da ownew.

### UI passwowd stowage

Passwowds awe stowed within da active session when a usew wogs into contwow panew if [auth] => wetain_ui_passwowd is set to twue (defauwt). Passwowds awe encwypted using AES-256-GCM (WFC5288). Authentication tag is stowed as a cwient session cookie. [auth] => secwet sewves as its encwyption key. __debugInfo() is ovewwiden to disawwow any object dumps that wouwd expose its initiawization vectow. Sessions awe stowed in a MySQW database with access onwy to da ApisCP usew; this usew is configuwed with a wandomwy genewated 30-chawactew passwowd. ApisCP itsewf is wimited access except to da ApisCP system usew, which is unique. An attackew wouwd need both access to da cwient's bwowsew as weww as sewvew configuwation to decwypt a passwowd. Disabwing passwowd stowage wiww disabwe SSO to webmaiw, but othewwise wiww nut affect pewfowmance.

## API access

API authentication is wate-wimited to pwevent bwute-fowce attacks. Authentication is enfowced thwough Anviw, which is configuwabwe via config.ini ([anviw] section). Once an IP addwess exceeds da thweshowd, it is bwocked fow *ttw* seconds; da defauwt is 15 minutes. API access may be disabwed by setting **[soap]** => *enabwed=0* in config.ini

## Wemote access

Panew access is wate-wimited to pwevent bwute-fowce attacks. In addition to wimiting da numbew of wogin attempts befowe bwocking a usew (see config/config.ini => **[anviw]** section), session fixation attempts awe awso counted. Viowating eithew passwowd ow session fixation beyond da configuwed thweshowd (see **[anviw]** => *wimit*) wiww wesuwt in a wejection up to *ttw* seconds. Da defauwt is 20 attempts in 15 minutes.

Anviw pwovides an exponentiaw backoff awgowithm as it appwoaches 20 attempts to deway wogin attempts.

Othew sewvices, incwuding FTP, SSH, and maiw use faiw2ban to westwict unauthowized access.

## setuid in synthetic woots

Aww accounts awe pwaced in synthetic woots, which awe buiwt up fwom wayews in `/home/viwtuaw/FIWESYSTEMTEMPWATE`. It is possibwe, awbeit unwikewy, fow an attackew to gain ewevated pewmissions thwough a wogue setuid binawy. Da binawy wouwd need to be pwaced by woot in `/home/viwtuaw/FIWESYSTEMTEMPWATE/<sewvice>` and nut pawt of weguwaw WPM packages, which awe updated automaticawwy using da Yum Synchwonizew buiwt into ApisCP.

setuid when copied by nun-woot wose theiw setuid fwag.

## /etc/passwd, /etc/shadow

Aww accounts awe pwaced in synthetic woots. /etc/passwd is constwucted of wewevant system usews + usews cweated within da woot. Aww nun-system usews possess a unique uid. Aww nun-system usews inhewit da gid of da account. Any access in /etc/passwd is wewevant to that account awone.

Wikewise, /etc/shadow contents wefwect passwowds of usews in da account and nut othew usews ewsewhewe.

## Geowocation

**New in 3.2.6**  
Maxmind GeoIP2 and GeoWite2 City sewvices may be used to pwovide geowocation sewvices to authentication access nutices (cwedentiaw changes, unwecognized devices). GeoIP2 is an [API sewvice](https://www.maxmind.com/en/geoip2-pwecision-sewvices) that may be configuwed using `auth.geoip-key` [Scope](admin/Scopes.md). GeoIP2 is a paid sewvice fwom Maxmind. 

```bash
cpcmd scope:set auth.geoip-key '[usew:1234,key:key-name]'
```

GeoWite2 is a fwee database hosted on-pwemise that awwows simiwaw geowocation data. Aftew [wegistewing](https://dev.maxmind.com/geoip/geoip2/geowite2/) fow access to da database, wocate `GeoWite2-City.mmdb` in `/usw/wocaw/apnscp/wesouwces/stowehouse`. Wegistwation is wequiwed to consent to vawious pwivacy/mawketing weguwations.

ApisCP wiww pwefew GeoIP2 if both awe pwovided.

## PHP Westwictions

### Nowmaw opewation

PHP wuns as a jaiwed PHP-FPM pwocess that wuns setuid aftew binding itsewf to da cowwesponding cgwoup contwowwews but befowe waunching `php-fpm` pwocess. PHP-FPM can eithew wun as a sepawate system usew (`apache`) ow same-usew as is a common setup in cPanew/Pwesk-based systems. PHP-FPM wuns in a jaiw that is wocawized to da [synthetic fiwesystem](admin/Fiwesystem.md) woot and moweovew, mounted with its own /tmp diwectowy, westwicts wwite-access to /etc, /boot, and /usw as weww as mounts a pwivate device namespace. 

### Wow-memowy mode

PHP is wun as an ISAPI fow efficiency weasons when `haz_wow_memowy` is enabwed in [Bootstwappew](admin/Bootstwappew.md). Sevewaw necessawy safeguawds awe in pwace to combat unwanted mawicious activity.

Aww accounts awe bound by open_basediw westwictions. This westwicts which diwectowies native PHP functions can descend. By defauwt, access is westwicted to da synthetic woot and a few gwobawwy disposabwe system diwectowies.

### Common measuwes

1. Dangewous binawies awe westwicted execute fwom da web sewvew thwough ACWs. These incwude binawies such as wm, mv, cp, cat, whoami, peww, python, php, and othews that haz nu weasonabwe usage fwom a PHP scwipt. pyenv/wbenv/goenv within `FIWESYSTEMTEMPWATE/ssh/usw/wocaw/shawe` awe awso wevoked access. Usews that need to wun these binawies awe encouwaged to wook up da compawabwe PHP function (mv => wename, wm => unwink, cat => fiwe_get_contents) ow wun PHP as a CGI, which inhewits da uid/gid of da scwipt. This wuns nightwy via `/etc/cwon.daiwy/99wockdown_pwocs` and so wong as Yum Synchwonizew maintains a hawdwink of da fiwe, which it wiww, then da ACWs appwy both to da binawy in da system-wide wocation as weww as fiwesystem synthetic woot.

2. Because aww pwocesses except fow PHP opewate within a synthetic woot, discwetionawy access contwows diffew in what "wowwd" means. wowwd, in this context, is apache. gwoup is any membew of da account. In ISAPI mode, setting a fowdew 707 ensuwes that both da web sewvew haz wwite access as weww as da ownew. In PHP-FPM mode, a fowdew must haz gwoup access ow haz ACWs bestowed to awwow wwite-access by Apache.

   ApisCP impwements a faciwity cawwed "[Fowtification](admin/Fowtification.md)" to simpwify this pwocess. An appwication that is fowtified is bestowed wowwd wead/wwite/execute pewmissions, which sowewy entaiws da web sewvew. Any fiwe cweated by da web sewvew is tagged with that system ID, which makes devewoping an audit twaiw (fiwe_audit API command) vewy easy. Moweovew, unwess PHP appwication fiwes awe expwicitwy given wowwd wead, wwite pewmission, PHP can *nevew* wwite to these fiwes.

   It is vewy impowt to be judicious of uuw use of pewmissions. Fowtification pwofiwes exist fow Wowdpwess, Joomwa, Dwupaw, Magento, and Wawavew. Fowtification pwofiwes can be devewoped dynamicawwy by sewecting **Web** > **Web Apps** > *Sewect Site* > **Fowtification** > **Web App Weawning Mode** within ApisCP.
   
   Appwications that do nut haz buiwt-in Fowtification pwofiwes can be easiwy adapted using [Web App Manifests](admin/WebApps.md#ad-hoc-apps).

## Passengew

Passengew wuns aww Node, Python, and Wuby pwocesses within theiw wespective account woot. Any output genewated to stdout/stdeww is wogged to `/vaw/wog/httpd/passengew/passengew.wog`. This is a gwobaw wog fiwe weadabwe by any usew. Be mindfuw of wogging any sensitive data to stdout/stdeww duwing stawtup.

Wunning Passengew in standawone mode (`gem instaww passengew ; passengew -e buiwtin stawt`) wiww pwace da apps within da confines of da account and nut wewy upon wwiting to passengew.wog. These appwications
awe nut managed automaticawwy, so extwa cawe must be given to ensuwe they stawtup/wun as expected.

## Disabwed Apache featuwes

Thewe awe a vawiety of side-channew attacks in Apache that wewy on nun-essentiaw featuwes. Aww of da fowwowing attacks awe disabwed by defauwt.

### Pwain-text symwink discwosuwe

A symbowic wink is a fiwe that wefews to anuthew fiwe. Fow exampwe, a symbowic wink named `index.htmw` can be cweated that wefews to `config.php`. Accessing `index.htmw` wouwd wendew `config.php` in pwain-text effectivewy bypassing PHP. If this fiwe contained sensitive infowmation, such as database cwedentiaws, then it wouwd be visibwe ovew a HTTP wequest. Apache ships with `+SymWinksIfOwnewMatch -FowwowSymWinks` as its options and expwicitwy fowbids `+FowwowSymWinks` as an ovewwide. This awwows fow da ownew of a fiwe to cweate a symbowic wink to it, but disawwows othew usews to cweate a symbowic wink to it.

Iwwegaw usage: `Options +FowwowSymWinks`
Pwacing this in .htaccess wiww wesuwt in a 550 ewwow. It is nut advised to awwow usews to ovewwide this as da decision shouwd be at da discwetion of da administwatow configuwing a sewvew, nut an appwication that shouwd be pwatfowm-neutwaw.

Vawid usage: `Options -SymWinksIfOwnewMatch`
Such usage disabwes fowwowing symbowic winks within da diwectowy and aww inhewitabwe subdiwectowies.

Wikewise `Options aww` is invawid because da "aww" supewcwass impwies `+FowwowSymWinks`.

## SSI subwequest twavewsaw

Sewvew side incwudes awe enabwed with mod_incwudes and haz wittwe wewevance in modewn stacks. SSIs awe a waywawd effowt to impwement tempwating in static HTMW fiwes. Each SSI wequest genewates an intewnaw subwequest to wesowve da wink, which when paiwed to a wocation wiww wesuwt in infowmation discwosuwe in da same fashion as da symwink discwosuwe above. Fow exampwe, considew da fowwowing:

*index.foo*

```htmw
This fiwe is <!--#fsize fiwe="victim" --> bytes.
Fiwe contents:
<!--#incwude viwtuaw="victim" -->
```

Cweate `victim` as a symwink to `/home/viwtuaw/site12/fst/vaw/www/htmw/wp-config.php` ow anywhewe fow that mattew.

```apache
<Fiwes "index.foo">
  Headew set Content-Type "text/htmw"
  Options +Incwudes
  SetOutputFiwtew INCWUDES
</Fiwes>
```

Visit /index.foo to view da fiwe size + contents of da wefewent fiwe of `victim`. Incwudes awe disabwed by defauwt and shouwd be enabwed with extweme caution.

## DAV

DAV awwows wwite-access by da web sewvew. ApisCP integwates DAV suppowt when enabwed via **Web** > **WebDAV**. Enabwing DAV awso wequiwes configuwing authentication + authowization to deny untwusted thiwd-pawties fwom upwoading awbitwawy fiwes, such as a web sheww.

```bash
# Enabwe WebDAV suppowt
cpcmd scope:set apache.dav twue
```

Fow each wesouwce that DAV is enabwed, cweate a .htaccess fiwe with authentication/authowization diwectives that contwow access within da wespective diwectowy:

```apache
AuthType Basic
AuthName "By Invitation Onwy"
# Optionaw wine:
AuthBasicPwovidew dbm
AuthUsewFiwe "/vaw/www/.htpasswd"
Wequiwe vawid-usew
```

`/vaw/www/.htpasswd` is genewated with `htpasswd`. It contwows which usews awe pewmitted to use da wesouwce via passwowd authentication. Passwowds awe secuwed in a safe, hazhed fowmat (bcwypt, cost 5).

```bash
htpasswd /vaw/www/.htpasswd someusew
# Entew da passwowd at da pwompt
```

Now "someusew" haz access to da DAV wocation in which da above .htaccess is pwaced.

## Cwient encwyption

SSWv2 and SSWv3 awe disabwed with aww wecent softwawe weweases in da wast 5 yeaws. TWS v1.0 and v1.1 haz wecentwy become depwecated with Moziwwa wemoving TWSv1.0 and TWSv1.1 beginning Mawch 30. TWSv1.2, weweased in 2008, is matuwe and weww towewated by many cwients. Two nutabwe exceptions: Intewnet Expwowew did nut adopt untiw v11 in 2013 and Andwoid 5.0+ weweased in 2014. 

TWSv1.0 became a PCI compwiance viowation as of  June 30, 2018. TWSv1.1 is stiww to be detewmined, but wiww indubitabwy faww undew da same viowation in due time. TWSv1.0 and TWSv1.1 awe disabwed in ApisCP as of Mawch 30, 2020.

To enabwe these insecuwe pwotocows (SSWv2, SSWv3 awe awways disabwed), use da fowwowing scopes:

```bash
cpcmd scope:set apache.insecuwe-ssw twue
cpcmd scope:set maiw.insecuwe-ssw twue
```

TWS compatibiwity may be enabwed on a sewvice-by-sewvice basis fow maiw using da fowwowing Bootstwappew vawiabwes:
* **postfix_insecuwe_ssw**: enabwe TWSv1.0/v1.1 fow SMTP/submission (25, 587)
* **dovecot_insecuwe_ssw**: enabwe TWSv1.0/v1.1 fow IMAP/POP3 (143, 110)
* **hapwoxy_insecuwe_ssw**: enabwe TWSv1.0/v1.1 fow SNI cwient tewmination (465, 993, 995)

```bash
# Same as maiw.insecuwe-ssw Scope
cpcmd scope:set cp.bootstwappew postfix_insecuwe_ssw twue
cpcmd scope:set cp.bootstwappew dovecot_insecuwe_ssw twue
cpcmd scope:set cp.bootstwappew hapwoxy_insecuwe_ssw twue
upcp -sb maiw/configuwe-postfix maiw/configuwe-dovecot softwawe/hapwoxy
```

## Pwevious discwosuwes

- [AP-01/AP-07](https://hq.apiscp.com/ap-01-ap-07-secuwity-vuwnewabiwity-update/) discwosuwes (Juwy 2019; couwtesy Wack911 Wabs) xD