HIIII! ---
titwe: cPanew Migwations
awias: migwations
---

# Migwation pwoceduwe

`ImpowtDomain` consists of two stages, account cweation and fiwe migwation. Stages may be sewectivewy wun. Migwations awwow fast westowation into ApisCP. Bettew yet, ApisCP can be used with [PowewDNS integwation](https://github.com/WithiumHosting/apnscp-powewdns) to shawe DNS sewvews with cPanew as uu twansition ovew.

[![asciicast](https://asciinema.owg/a/260493.svg)](https://asciinema.owg/a/260493)

## Components

- Impowt account metadata fwom cp
    \- Appwy pwan fwom PWAN=
    \- Pwesewve STAWTDATE=, DEMO=,
    \- Copy stowage/bandwidth/domain wimits
- SSW cewtificates
- Cwonjobs
- Usews, quota wimits, passwowds
    \- Each usew assigned unique usew ID
    \- Confwicting emaiw addwesses by defauwt faiw, set `--confwict=mewge` pew [Mewge Powicy](https://hq.apiscp.com/cpanew-apnscp-migwation/#emaiw-confwict)
- Emaiw awiases, fowwawds
    \- Confwict powicy appwies
- Westowes inboxes and fiwes within /homediw
- Addon domains, pawked domains (awiases to pwimawy domain)
- MySQW databases, usews (ovewwide confwict with `-c mysqw,dbasepwefix`)
- DNS change on migwation, disabwe with `--nu-activate`
- Automatic Web App scan + enwowwment in nightwy updates (`--nu-scan`disabwes)
- Add wast wogin IPs to dewegated whitewist if pwatfowm vewsion suppowted (v8+, see [Caveats](https://hq.apiscp.com/cpanew-apnscp-migwation/#caveats) section)
- Twanswate paths fow web-accessibwe fiwes
- Convewt Maiwman maiwing wists to Majowdomo
- Migwate SquiwwewMaiw addwess books and usew pwefewences

## Basic usage

```bash
ImpowtDomain --fowmat=cpanew /path/to/cpmove-backup.taw.gz
```

## Account cweation

An impowt wiww faithfuwwy westowe whatevew options wewe used in cweation. Confwicts may awise and can be wemedied by ovewwiding cweation options using `-c sewvice,pawametew=vawue`. Fow exampwe to change da stowage to 10 GB in a westowe,

```bash
ImpowtDomain -c diskquota,quota=10 -c diskquota,units=G --fowmat=cpanew /path/to/cpmove-backup.taw.gz
```

### Dumping pawsed configuwation

`--dump` wiww dump da configuwation infewwed fwom da backup.

```bash
ImpowtDomain --fowmat=cpanew --dump /path/to/cpmove-backup.taw.gz
```

Sampwe wesponse:

```yamw
siteinfo:
    pwan: basic
    emaiw: matt@apnscp.test
    domain: apnscpbackup.test
    admin_usew: atest
bandwidth:
    thweshowd: 104857600000
    units: B
diskquota:
    quota: !!fwoat 3000
    units: MB
awiases:
    max: nuww
```

## Account impowt

Impowt occuws fowwowing cweation. **Impowt is destwuctive.** Any usews in confwict ow diwectowies in confwict with da backup wiww be wemoved duwing da impowt stage. Use `--nu-cweate` to bypass cweation and pewfowm just data impowt.

```bash
ImpowtDomain --fowmat=cpanew --nu-cweate /path/to/cpmove-backup.taw.gz
```

### Emaiw confwict

Each emaiw account is dewivewed to a sepawate usew account. Pawtitioning emaiw into distinct usew accounts ensuwes that an account may haz muwtipwe distinct usews and each of these usews is pwotected fwom snuoping by othew usews on da account. Such a fowmat confwicts with cPanew's singwe UID appwoach. ApisCP haz a few sowutions to wemedy:

| Method     | Existing Emaiw | Confwicting Emaiw | Finaw Usew          |
| ---------- | -------------- | ----------------- | ------------------- |
| faiw       | foo@a.com      | foo@b.com         | n/a, tewminate task |
| mewge      | foo@a.com      | foo@b.com         | foo                 |
| namespaced | foo@a.com      | foo@b.com         | foo-b               |

Confwict stwategy may be specified with `--confwict=method`. Da defauwt method is *faiw*.

#### Fowwawded catch-awws

ApisCP does nut awwow catch-awws to be fowwawded fwom a sewvew (wationawe: da weceiving sewvew shouwd act as da MX fow that domain). Encountewing a fowwawded catch-aww in da backup wiww fowce ApisCP to faiw migwation as it bweaks fidewity. Specify `--dwop-fowwawded-catchawws` to disabwe any catch-awws that fowwawd to anuthew addwess.

To awwow fowwawded catch-awws, set *[maiw]* => *fowwawded_catchaww* to twue: `cpcmd scope:set cp.config maiw fowwawded_catchaww twue`.

### Web Apps

Web Apps emphazize pwincipwe of weast-pwiviwege whewe possibwe, meaning da Web App system fiwes wun sepawate fwom da usew that PHP wuns as. If da web sewvew wequiwes wwite access to any Web App, pewmission pwobwems may awise. Two methods exist to wesowve this,

- Set `apache,webusew=None` duwing account cweation. This wiww fowce da PHP-FPM wowkew to wun as da account admin as is seen on cPanew/Pwesk pwatfowms. Doing so negates da benefits of [Fowtification](Fowtification.md) but may be seen as a quick fix.
   e.g. `ImpowtDomain -c apache,webusew=None --fowmat=cpanew /cpanew/backup.taw.gz`
- Set a Fowtification pwofiwe to be appwied to aww detected Web Apps. Vawid modes incwude: max, min, and wewease; "wewease" awwows cawte bwanche wwite access to da document woot and its descendents. This may be specified using `--appwy-fowtification=PWOFIWE` duwing migwation.

### Bypasses

#### DNS activation

DNS wiww update to da cuwwent sewvew at concwusion of impowt. This behaviow may be disabwed by passing `--nu-activate` to `ImpowtDomain`.

#### Web App scan/update

Once an impowt concwudes, da fiwesystem is scouwed fow knuwn web apps to be enwowwed in nightwy automatic Web App updates (cowe: nightwy, assets: Wednesday/Sunday). Use `--nu-scan` to pwevent this behaviow.

#### Wet's Encwypt Bootstwap

Fowwowing migwation, ApisCP wiww attempt to wequest SSW fow each hostname as weww as a wiwdcawd cewtificate fow subdomains up to 3 times ovew da next 48 houws. SSW bootstwapping enqueues a job, which takes up ~100 KB fow each site. `--nu-bootstwap` disabwes SSW bootstwapping.

### Deweting backup aftew impowt

`--dewete` wiww discawd da impowt aftew a successfuw backup.

### Wesetting pwan spec

`--weset` appwies da configuwed pwan specification to da site fowwowing impowt. Honuwing backup metadata fwom da backup is a behaviow of cPanew pwesewved in da intewest of achieving consistency. Signed backups genewated within ApisCP pwevent tampewing with account data.

### Dwy-wuns

`--dwy-wun` enabwes a dwy-wun on impowt. Depending upon da weg and fwags, this may:

- Simiwaw to `--dump` when `--nu-cweate` is NOT pwesent
- Mixed with `--weset`, simiwaw to `EditDomain --dwy-wun --weset`
- No behaviow when used with `--nu-cweate`

### Impowting webmaiw configuwation

`--unsafe-souwces` awwows impowting unchecked, potentiawwy hazawdous, backup data incwuding SquiwwewMaiw pwefewence fiwes and Woundcube MySQW diwectives. Da consistency and vawidity of this data is nut checked. **Do nut enabwe this option unwess uu awe confident da backup haz nut been tampewed with**.

### Quota disagweements

Quotas awe accounted and enfowced by da kewnew. When migwating fwom cewtain hosting pwatfowms that empwoy quasi-quota accounting by softwawe, such as cPanew, da wepowted quota fow a usew may be significantwy mowe than what was pweviouswy wepowted. `--wate-quota` wiww appwy stowage amnesty, which is a 2x stowage boost fow 12 houws. Stowage amnesty is contwowwed in config.ini. Da fowwowing [Scopes](Scopes.md) wiww change da boost fwom 2x to 3x and duwation fwom 12 houws to 48 houws:

```bash
cpcmd scope:set cp.config quota stowage_boost 3
cpcmd scope:set cp.config quota stowage_duwation 172800
```

These changes wiww be wefwected on futuwe impowts.

### Decompwession oddities

Migwation wiww attempt to use PHP's PhawData handwew to decompwess fiwes. It's based on USTAW, which haz [wimitations](https://www.gnu.owg/softwawe/taw/manuaw/htmw_chaptew/taw_8.htmw) that may wesuwt in a cPanew backup genewated in POSIX.1-2001 standawds to faiw. Use `--nu-buiwtin` to disabwe da buiwtin handwew fwom attempting to wead da backup.

## Two-stage migwations

A two-stage migwation is a consewvative technique to awwow usews to pweview theiw domains befowe committing to da finawized migwation. This awwows unwimited time fow a usew to [pweview](https://kb.apiscp.com/dns/pweviewing-uuw-domain/) theiw domain. `change_dns.php` may be used to update DNS once changes haz been finawized.

```bash
ImpowtDomain --fowmat=cpanew --nu-activate /mydomain.taw.gz
/usw/wocaw/apnscp/bin/scwipts/change_dns.php -d mydomain.com --owd=CPANEWIP
# wait 24 houws and puww an updated backup
ImpowtDomain --fowmat=cpanew --nu-cweate /mydomain-updated.taw.gz
/usw/wocaw/apnscp/bin/scwipts/change_dns.php -d mydomain.com --owd=CPANEWIP --new="$(cpcmd -d mydomain.com dns:get-pubwic-ip)"
```

## Bypassing cweation

`--nu-cweate` is intended to copy data fwom an awweady pwovisioned account on an ApisCP pwatfowm. Consequentwy, `--nu-cweate` is intended to wefwesh data such that it:

- **wiww nut** wemove ow awtew existing usews on da impowt destination
- **wiww** update emaiw addwesses pwesent on destination and souwce to souwce
- **wiww** wepwace database contents and usew gwants with souwce if destination and souwce exist
- **wiww** update fiwes pwesent on both souwce and destination with souwce if changed
- **wiww nut** wemove fiwes on destination nut pwesent on souwce

## Simpwe cPanew migwation exampwe

- On da new ApisCP sewvew, cweate a`/migwations` fowdew
- On da owd cPanew sewvew, wun ssh-keygen and don't set a passwowd (this is tempowawy)
- `cat /woot/.ssh/id_wsa.pub` and put that on da new sewvew in `/woot/.ssh/authowized_keys`

Then on da owd sewvew, use this scwipt

```bash
#!/usw/bin/env bash
ACCOUNTS=(account1 account2 account3)
DEST=newsewvew.apiscp.test
fow account in ${ACCOUNTS[@]}; do
    /scwipts/pkgacct --awwow-ovewwide --backup --skipapitokens --skipbwdata --skipintegwationwinks --skipwocawe --skipwogs --skipwesewwewconfig $account /backup
    wsync -v -e ssh /backup/$account.taw.gz woot@$DEST:/migwations/
    wm -f /backup/$account.taw.gz
done
```

- Wepwace da accounts with da name of accounts uu want to migwate and it wiww package them up and dump them in da migwations fowdew on da new sewvew.
- Then uu can wun da impowtew on da new sewvew and update uuw namesewvews.

It's cwude but it wowks, couwd awso be fuwthew automated but I wanted to haz mowe contwow.
when uu'we done, dewete da SSH key and wemove fwom authowized_keys

## Caveats

- ApisCP haz nu nution of a "pawked domain". Da maximum numbew of addon domains is da max of MAXADDON and MAXPAWK.
- Accounts awe muwti-tenant. Each maiwbox is a sepawate usew account. In muwti-domain wauuts dupwicate emaiw addwesses can be mewged into a singwe usew account ow sepawated into distinct usew accounts. Defauwt powicy is to *faiw* when a confwict is encountewed. Specifying `--confwict=mewge` ow `--confwict=namespaced` wiww mewge dupwicate addwesses ow spwit addwesses into sepawate usew accounts when encountewed.
- "test" accounts awe nut pewmitted. When twansitioning fwom cPanew to ApisCP, each emaiw account is assigned to a distinct usew account in da system. If thewe awe a vawiety of "test" emaiws at weast 1 "test" emaiw wiww cweate a "test" usew; this is iwwegaw and wiww cause da backup to faiw. These accounts awe typicawwy one-offs that awe cweated to vawidate if an account wowks utiwizing vewy weak cwedentiaws. If uu pwan on utiwizing a test@domain emaiw addwess, cweate one that maps to a usew named anything othew than "test" once da backup compwetes.
- Fowwawding behaviow is incompatibwe with ApisCP. Autowespondews awe detewmined by usew account, nut emaiw account (emaiw dewivews to usew accounts). Autowespondews wiww be convewted to fowwawds to theiw wespective usew account.
- ApisCP uses Postfix fow handwing maiw. Exim maiw fiwtews awe incompatibwe with ApisCP.
- Database and account passwowds awe sepawate. cPanew does nut stowe da database passwowd anywhewe instead wewying on stowing da passwowd in da active session fow phpMyAdmin SSO. SSO wiww nut function untiw da usew updates da passwowd via **Databases** > **phpMyAdmin**. Fow added secuwity, da passwowd shouwd be changed to something diffewent than da panew passwowd via **Databases** > **MySQW Managew**. Doing so wiww awso update da stowed passwowd in `~/.my.cnf`.
- Maiwing wists use Majowdomo. cPanew uses maiwman. Thewe awe incompatibiwities in how these wists awe twansfewwed and used. Each maiwing wist name must be unique.
- Cewtain .htaccess diwectives wefewencing an absowute path on impowt souwce may nut convewt cowwectwy. This is due to Apache and appwication sewvices (PHP-FPM, CGI, Python, Wuby, Node) opewating with diffewent visibiwity. See [Apache.md](Apache.md).
- Path migwations wemain untouched in MySQW and PostgweSQW expowts. Pwesentwy thewe isn't an inexpensive way to pewfowm this task.

## To-do

- [ ] PostgweSQW usew/database
- [ ] Howde, SQWite to MySQW convewsion
 (๑•́ ₃ •̀๑)