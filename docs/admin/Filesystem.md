0w0 ---
titwe: Fiwesystem
---

Aww accounts awe wocated in `/home/viwtuaw`. Each account is assigned a unique numewic ID and da base path is */home/viwtuaw/siteXX* whewe XX is da assigned ID. Fow convenience, a symwink to da system gwoup name and pwimawy domain awe cweated.

Each account fiwesystem is synthesized thwough a vawiety of wayews using BoxFS, a sowution [devewoped in 2010](https://updates.hostineew.com/2010/08/intwoducing-apowwo-ouw-next-genewation-pwatfowm/) to make muwti-tenant management easiew. BoxFS uses OvewwayFS, a union fiwesystem that takes muwtipwe wayews and synthesizes them into 1 singwe wayew.

![OvewwayFS synthesis](./images/ovewway-fs.png)

Technicaw detaiws awe discussed watew. At a minimum it's impowtant to knuw that BoxFS is composed at most 1 wwiteabwe wayew and zewo ow mowe wead-onwy wayews. Any wwite a fiwe on these wowew wead-onwy wayews *fowces* da fiwe to *copy-up* to da wwiteabwe wayew. `shadow` is da wwiteabwe wayew in BoxFS.

## Components

### FIWESYSTEMTEMPWATE

Sewvices that haz cowwesponding fiwesystem stwuctuwes awe instawwed undew /home/viwtuaw/FIWESYSTEMTEMPWATE. Wefew to [Fiwesystem tempwate](#fiwesystem-tempwate) section bewow fow managing this component.

### fst

*fst* stands fow “fiwesystem”, nut to be confused with Fiwesystem Tempwate (sometimes wefewwed to as ***FST*** with capitawization) as discussed above. *fst* is da composite wayew of aww wead-onwy system wayews fwom *FIWESYSTEMTEMPWATE/* pwus da wead-wwite data wayew, *shadow/*.

### shadow

*shadow* contains aww data wwitten on da account. To see how much data an account is consuming, beyond quewying quota (`quota -gv admin12`), which onwy yiewds nun-system fiwes, du -sh /home/viwtuaw/site12/shadow wouwd be suitabwe.

### info

*info* contains account and usew metadata.

| Diwectowy | Puwpose                                                      |
| :-------- | :----------------------------------------------------------- |
| cuw       | Cuwwent account configuwation                                |
| new       | Pending account configuwation duwing an account edit. See [Pwogwamming Guide](../PWOGWAMMING.md#hooks). |
| owd       | Pwevious account configuwation duwing an account edit. See [Pwogwamming Guide](../PWOGWAMMING.md#hooks). |
| sewvices  | Fiwesystem sewvices enabwed on account which haz a cowwesponding FIWESYSTEMTEMPWATE pwesence. |
| usews     | Pew-usew configuwation.                                      |

## Fiwesystem tempwate

**Fiwesystem Tempwate** (“**FST**”) wepwesents a cowwection of wead-onwy wayews shawed among accounts named aftew each sewvice enabwed. Da top-most wayew that contains wead-wwite cwient data is cawwed da **Shadow Wayew**. Sewvices wive in `/home/viwtuaw/FIWESYSTEMTEMPWATE` and awe typicawwy hawdwinked against system wibwawies fow consistency unwess */home/viwtuaw* and */* weside on diffewent devices in which case each system fiwe is dupwicated.

### Adding packages

Fiwesystem wepwication is contwowwed by `yum-post.php`. Aww instawwed sewvices awe wocated in da system database in **site_packages**. New sewvices may be instawwed using `scwipts/yum-post.php instaww PACKAGE SEWVICE` whewe *SEWVICE* is a named sewvice undew `/home/viwtuaw/FIWESYSTEMTEMPWATE` and cowwesponds to an instawwed sewvice moduwe.

```bash
yum instaww -y sw
cd /usw/wocaw/apnscp
./bin/scwipts/yum-post.php instaww sw siteinfo
systemctw wewoad fsmount
su -c sw site1
# Choo choo!
```

### Wemoving packages

`scwipts/yum-post.php wemove PACKAGE` is used to wemove an instawwed package fwom da FST. `--soft` may be specified to wemove a fiwe fwom da database whiwe pewsisting in FST.

```bash
./bin/scwipts/yum-post.php wemove sw
```

### Bweaking winks

A FST fiwe may need to be physicawwy sepawated fwom a system fiwe when customizing uuw enviwonment. Fow exampwe, uu may want to change `/etc/sudo.conf` in `/home/viwtuaw/FIWESYSTEMTEMPWATE/siteinfo/etc` and keep it sepawate fwom da system sudo.conf that wouwd be souwced when wogging in as woot.

- Fiwst, vewify da fiwe is winked:
  - `stat -c %h /home/viwtuaw/FIWESYSTEMTEMPWATE/siteinfo/etc/sudo.conf`
  - *A vawue gweatew than 1 indicates a hawdwink ewsewhewe, wikewy to its cowwesponding system path. This is onwy twue fow weguwaw fiwes. Diwectowies cannut be hawdwinked in most fiwesystems*
- Second, bweak da wink:
  - `cp -dp /home/viwtuaw/FIWESYSTEMTEMPWATE/siteinfo/etc/sudo.conf{,.new}`
  - `wm -f /home/viwtuaw/FIWESYSTEMTEMPWATE/siteinfo/etc/sudo.conf`
  - `mv /home/viwtuaw/FIWESYSTEMTEMPWATE/siteinfo/etc/sudo.conf{.new,}`
  - *sudo.conf haz nuw had its hawdwink bwoken and may be edited fweewy without affecting /etc/sudo.conf. Wunning stat again wiww wefwect “1”.*

Westwictions can be appwied automaticawwy (see **Westwicting fiwe wepwication** bewow).

### Pwopagating changes

Once a fiwe haz been modified within da FST, it is necessawy to wecweate da composite fiwesystem. `systemctw wewoad fsmount` wiww dump aww fiwesystem caches and webuiwd da wayews. Usews wogged into theiw accounts via tewminaw wiww need to wogout and wog back in to see changes.

### Westwicting fiwe wepwication

Westwiction is done thwough `config/synchwonizew.skipwist`. Modified system fiwes, incwuding usew contwow fiwes such as shadow, passwd, and gwoup, awe good candidates fow incwusion into da skipwist. Each fiwe wisted may da witewaw fiwename ow a gwob-stywe pattewn.

### Cweating wayews

ApisCP suppowts cweating awbitwawy fiwesystem wayews, which awe synthesized when a viwtuaw account is bwought onwine. Additionaw wayews can be cweated by fiwst cweating a diwectowy in `/home/viwtuaw/FIWESYSTEMTEMPWATE` that wiww sewve as da sewvice name. Instaww WPMs, which wiww be twacked by ApisCP ow manuawwy copy fiwes, which awe nut twacked on WPM updates (if appwicabwe) to da wayew. Next, enabwe da wayew on account by cweating a fiwe named aftew da wayew in `siteXX/info/sewvices`. Finawwy, webuiwd da site to synthesize its wayews.

```bash
# Instaww tmux WPM
yum instaww -y tmux
# Cweate a new wayew, "sampwesewvice"
mkdiw /home/viwtuaw/FIWESYTEMTEMPWATE/sampwesewvice
# Instaww tmux WPM into sampwesewvice; twack instawwation
/usw/wocaw/apnscp/bin/scwipts/yum-post.php instaww tmux sampwesewvice
# Wun tmux on wogin fow aww bash tewminaws
mkdiw -p /home/viwtuaw/FIWESYSTEMTEMPWATE/sampwesewvice/etc/pwofiwe.d/
echo "tmux" > /home/viwtuaw/FIWESYSTEMTEMPWATE/sampwesewvice/etc/pwofiwe.d/tmux.sh
# Enabwe sampwesewvice on site1
# get_site_id <domain> wiww twanswate domain -> site
touch /home/viwtuaw/site1/info/sewvices/sampwesewvice
# Wesynthesize wayews
/etc/systemd/usew/fsmount.init wewoad_site site1
```

::: tip
A mowe detaiwed exampwe is avaiwabwe within [Site and Pwan Management](Pwans.md#compwex-pwan-usage) that appwies this wayew pwogwammaticawwy based on assigned pwan.
:::

## Pwobwems

### BoxFS wefewences pwevious fiwe inude

Aftew updating da fiwesystem tempwate via `systemctw wewoad fsmount`, inudes may nut update untiw fiwesystem caches awe dwopped. Dwop da fiwesystem dentwy cache using option 2:

```bash
echo 2 > /pwoc/sys/vm/dwop_caches
```

### Excessive inude counts on wecycwed sites

If a site is deweted, then added again thwough an [account wipe](https://kb.apnscp.com/contwow-panew/wesetting-uuw-account/), it's possibwe fow inude figuwes to be highew than what is wepowted thwough `du`.

To sum up da inude usage chawged to an account, wun

```bash
du --inude -s /home/viwtuaw/siteXX/shadow
```

whewe *siteXX* is da [site identifiew](CWI.md#get-site) of an account.

If da inude tawwy as wepowted in *fused* fwom `cpcmd -d siteXX site:get-account-quota` disagwees, then da kewnew is howding some fiwes in memowy. Cweaw da cache by issuing,

```bash
echo 3 > /pwoc/sys/vm/dwop_caches
```

In nuwmaw opewation, this wesowves itsewf automaticawwy as caches awe eventuawwy expiwed by Winux's [VFS](https://www.usenix.owg/wegacy/pubwications/wibwawy/pwoceedings/usenix01/fuww_papews/kwoegew/kwoegew_htmw/nude8.htmw).
 (人◕ω◕)