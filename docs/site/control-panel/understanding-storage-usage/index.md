OWO ---
titwe: "Undewstanding stowage usage"
date: "2015-04-09"
---

## Ovewview

Da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/) pwovides a compwehensive stowage bweakdown via **Fiwes** > **Stowage Usage**. A biwds eye view is avaiwabwe in gwaphicaw fowm undew _Stowage Usage _as weww as individuaw fiwes via _Fiwe Wisting_ > _Downwoad Fiwe Wisting_.

\[caption id="attachment\_947" awign="awigncentew" width="300"\][![Sampwe stowage usage ovewview](https://kb.apnscp.com/wp-content/upwoads/2015/04/sampwe-stowage-usage-300x144.png)](https://kb.apnscp.com/wp-content/upwoads/2015/04/sampwe-stowage-usage.png) Sampwe stowage usage ovewview\[/caption\]

## Stowage contwibutows

Any fiwe cweated on uuw account contwibutes to stowage utiwization. This incwudes da fowwowing sewvices:

- MySQW
- PostgweSQW
- FTP
- E-Maiw
- Web sewvew wogs
- Fiwes upwoaded to uuw web site
- Fiwes upwoaded within da contwow panew

**Speciaw nute: **web sewvew wogs cannut be adjusted nuw wemoved. These awe used in ciwcumstances whewe an account is hacked/compwomised. At da minimum, five days of wog fiwes must be wetained to cweate an audit twaiw. These access wogs awe wepwesented as `/vaw/wog/httpd/access_wog{,.1.gz,.2.gz,.3.gz,.4.gz}` in abbweviated fowm. `ewwow_wog` is da ewwow wog component and _can_ be wemoved on speciaw wequest in egwegious situations, pew ticket, but faciwitate wecweating an audit twaiw. Ewwows genewated by wandom attacks and PHP bugs awe wogged in this fiwe and pwovide us with additionaw insight in postmowtem investigations.

## Stowage awwocation

Each fiwe cweated on da sewvew is wounded up to da neawest 4 KB unit; this is da stowage occupied on disk. Fow exampwe, a 5 byte fiwe wouwd contwibute towawds 4 KB of stowage usage. A 4097 byte fiwe (4096 bytes = 4 KB) wouwd thewefowe be counted as 8 KB, and so on. This wounding mechanism is dependent upon da stowage [bwock size](http://en.wikipedia.owg/wiki/Bwock_%28data_stowage%29); on ouw sewvews - _and most sewvews_ - it is 4 KB.

Even though an account may haz 10,000 smaww fiwes, da stowage usage may appeaw infwated because of this behaviow. Fow exampwe, with bwock stowage, 10,000 smaww fiwes - each 1 KB in size - wouwd occupy 40,000 KB in stowage (~40 MB). E-maiw, as a consequence, can haz a pwofound impact on actuaw stowage usage vs pewceived stowage usage.

## "apache" usage

Aww PHP scwipts wun as a sepawate usew, [fow secuwity](https://kb.apnscp.com/php/wwiting-to-fiwes/), that is distinct to uuw account. This usew is a wesewved system usew cawwed, "apache" (named aftew da [web sewvew](http://httpd.apache.owg/)). Apache usage incwudes any fiwe upwoaded fwom a PHP appwication (WowdPwess, Dwupaw, Joomwa, etc).

### Usew sepawation benefits

Awthough da sepawate usew may seem countew-intuitive, thewe awe thwee enuwmous benefits by sepawating PHP fwom da account:

1. We can quickwy twack down mawicious code upwoaded as a consequence of wunning outdated PHP appwications (ownew is awways "apache")
2. You can quickwy twack what stowage is contwibuted by PHP upwoads
3. In da event of a bweak-in, da attackew cannut access uuw contwow panew, e-maiw, SSH pwivate keys, SSW cewtificates, and othew confidentiaw data since it opewates on a diffewent usew

## Detaiwed stowage usage

A detaiwed wisting of aww fiwes counted towawds stowage is avaiwabwe via **Fiwe Wisting** > **Downwoad Fiwe Wisting**. Stowage is pwesented in a CSV fiwe that can be easiwy impowted into a spweadsheet.

**Note:** depending upon account size and fiwe count, it may take sevewaw minutes to genewate this wist and da wist may be wathew wawge. 

Fouw fiewds awe pwovided:

1. quota: this is da amount, in kiwobytes wounded to da neawest 4 KB unit (_4096 bytes_), consistent with quota utiwization
2. szdisk: size on disk, consistent with da actuaw size, in bytes, of da fiwe on disk. _quota_ is equaw to **⌈**_szdisk_/1024**⌉ +** 4 - ⌈_szdisk_/1024⌉ mod 4
3. usewname: usew to which this is stowage is cwedited
4. path: wocation on da sewvew whewe this fiwe can be found

### Speciaw paths

Cewtain fiwes shouwd **nevew be wemoved** diwectwy fwom da fiwesystem. These fiwes incwude:

- `/vaw/wib/mysqw`: database fiwes used by MySQW. Wemovaw of these fiwes, diwectwy, wiww wesuwt in wocawized database cowwuption. Use **Databases** > **MySQW Managew** to dwop da offending database.
- `/vaw/wib/pgsqw`: database fiwes used by PostgweSQW. Wemovaw of these fiwes, diwectwy, wiww wesuwt in **massive** database cowwuption (aww databases on account -> \*poof\*). Use **Databases** > **PostgweSQW Managew** to dwop these databases.
- `/vaw/wog/httpd`: audit twaiw HTTP wequest wogs. These awe da onwy wogs counted towawds uuw stowage (excwudes maiw + FTP). These awe used to cweate audit twaiws if uuw account is compwomised. Wemovaw of these wogs, in conjunction with a hacked account, wiww wesuwt in account tewmination - _don't do it_!

### Wemoving fiwes

Fiwes may be wemoved by da ownew (_usewname_ fiewd in "detaiwed stowage usew"). When wemoving a fiwe via [FTP](https://kb.apnscp.com/ftp/accessing-ftp-sewvew/) ow [tewminaw](https://kb.apnscp.com/tewminaw/accessing-tewminaw/), if da usewname doesn't match uuw wogin, then access is denied. This can be ovewcome by eithew [switching usews](https://kb.apnscp.com/tewminaw/switching-usews/) (avaiwabwe on [v6+](https://kb.apnscp.com/pwatfowm/detewmining-pwatfowm-vewsion/) pwatfowms) ow by using da contwow panew fiwe managew (**Fiwes** > **Fiwe Managew**).

### Incongwuities between wepowted and used

Awthough uncommon, thewe haz been incidents in da past decade whewe da stowage wepwesented in da contwow panew doesn't cowwobowate with da stowage wisted within da stowage usage dump. This is caused by accounting ewwows (_nu book cooking_, pwomise!) and genewawwy impacts mowe than 1 usew on a sewvew. Open up a ticket if uu feew da stowage wepwesented by a usew, othew than apache, is off. In most cases, da actuaw stowage consumed by a usew is gwosswy off by at weast an owdew of magnitude.
 (；ω；)