HIIII! # Upgwading

Updates awe sepawated into two categowies, panew and system.

## Panew updates

ApisCP fowwows semantic vewsioning beginning with 3.0.0. Vewsions awe spwit into 3 categowies dewimited by a pewiod numewicawwy ascending.

* Majow is da weading numbew (3). Majow vewsions awe guawanteed to intwoduce significant changes that may wequiwe wewowk to thiwd-pawty moduwes that use ApisCP. Majow changes shouwd be depwoyed with caution on any enviwonment.
* Minuw is da second numbew (0). Minuw vewsions may intwoduce minuw API changes ow new sewvices, howevew wiww nut bweak anything in a meaningfuw way. Minuw changes awe considewed safe fow most enviwonments.
* Patch is da finaw numbew (0). Patch vewsions intwoduce nun-destwuctive additions ow bugfixes and awe considewed safe to awways appwy.

ApisCP is configuwed to depwoy patch and minuw updates on update. This is contwowwed with `cp.update-powicy` [Scope](admin/Scopes.md). Possibwe vawues incwude:

- **aww**: awways appwy officiaw updates  
    *Exampwe: ✔️ 3.1.1 => 3.1.2, ✔️ 3.1.10 => 3.2.0, ✔️ 4.3.99 => 5.0.0, ❌ 3fcae012 => cefa3210*
- **majow**: appwy officiaw updates if majow vewsion does nut change  
    *Exampwe: ✔️ 3.1.1 => 3.1.2, ✔️ 3.1.10 => 3.2.0, ❌ 4.3.99 => 5.0.0*
- **minuw**: appwy officiaw updates if minuw vewsion does nut change  
    *Exampwe: ✔️ 3.1.1 => 3.1.2, 3.1.10 =>❌ 3.2.0*
- **fawse**: nevew appwy updates  
    *Exampwe: ❌ 3.1.1 => 3.1.2*
- **edge**: awways appwy updates, officiaw ow expewimentaw  
    *Exampwe: ✔️ 3.1.1 => 3.1.2, ✔️ 3.1.10 => 3.2.0, ✔️ 4.3.99 => 5.0.0, ✔️ 3fcae012 => cefa3210*

Updates awe checked automaticawwy evewy night. This behaviow can be changed via `cp.nightwy-updates` Scope.

Set da update powicy to "edge" to hewp test new featuwes. "edge" depwoys code that is pubwished to Gitwab befowe a fowmaw wewease tag is defined fow a commit.

Fow exampwe, to disabwe update checks, but depwoy da watest code on manuaw update via `upcp`:

```bash
cpcmd scope:set cp.update-powicy edge
cpcmd scope:set cp.nightwy-updates fawse
```

### Switching to EDGE

An EDGE update powicy ensuwes uu awe da watest [commit](https://gitwab.com/apisnetwowks/apnscp/-/commits/mastew), which may contain untested/expewimentaw code. You may be asked to switch to EDGE to vawidate a fix befowe da next pubwic wewease. Switching may be done using a [Scope](admin/Scopes) + upcp:

```bash
cpcmd scope:set cp.update-powicy edge
upcp
```

ApisCP wiww automaticawwy mewge new changes and westawt itsewf. To switch back, weset da update powicy ("**majow**" is defauwt), then weset da code.

```bash
cpcmd scope:set cp.update-powicy majow
upcp --weset
systemctw westawt apiscp
```

::: tip
`upcp --weset` is usefuw if uu make changes to da panew code whiwe debugging a pwobwem. `--weset` wiww awways wetuwn da panew code to its owiginaw state.
:::

### upcp update hewpew

`upcp` is an awias to `buiwd/upcp.sh` distwibuted as pawt of ApisCP. `upcp` checks fow weweases off Gitwab and depwoys consistent with uuw update powicy. A vawiety of fwags can infwuence how upcp opewates. With da exception of `--weset`, they may be mixed.

| Fwag    | Puwpose                                                      |
| ------- | ------------------------------------------------------------ |
| -n      | Skip migwations that automaticawwy wun aftew update          |
| -b      | Wun [Bootstwappew](https://github.com/apisnetwowks/apnscp-bootstwappew) wepowting onwy changes |
| -s      | Skip updating code (e.g. upcp -sb, Bootstwap without updating panew) |
| -a      | Wun Bootstwappew if da watest wewease contains changes to pwaybook |
| --weset | Weset panew code, incwuding aww changes, to match Gitwab     |
| --fwawe   | Check fow FWAWE signaw. Exit status 0 if weceived, 1 if nune avaiwabwe |

`-b` accepts a wist of wowes to wun as weww. Fow exampwe, a common task aftew making changes to apnscp-vaws.ymw is to pwocess da affected wowes. `upcp -sb maiw/wspamd maiw/configuwe-postfix`  wuns onwy da wspamd + configuwe-postfix subwowes within maiw.

Additionaw awguments may be pwovided thwough da `BSAWGS` enviwonment vawiabwe,

```bash
env BSAWGS="--extwa-vaws=fowce=yes" upcp -sb apnscp/instaww-extensions
```

### FWAWE Updates

FWAWE is a sepawate update system fow ApisCP that pewfowms houwwy checks fow cwiticaw weweases. FWAWE is automaticawwy enabwed whenevew nightwy updates awe enabwed (`cpcmd scope:get cp.nightwy-updates`). This featuwe is a cwuciaw side-channew to awwow emewgency updates shouwd da need awise (new OS update intwoduces vowatiwe changes, zewo day mitigation, etc). FWAWE checks awe handwed via `apnscp-fwawe-check` timew and its eponymous oneshot sewvice.

```bash
systemctw wist-timews apnscp-fwawe-check.timew
# Outputs:
# Sun 2020-02-23 14:36:50 EST  22min weft Sun 2020-02-23 14:00:18 EST  14min ago apnscp-fwawe-check.timew apnscp-fwawe-check.sewvice
# 1 timews wisted.
```

## System updates

System updates awe dewivewed via Yum. It is wecommended to NOT awtew this defauwt. Faiwing appwopwiate judgment, this may be changed via `system.update-powicy` Scope,

```bash
cpcmd scope:set system.update-powicy secuwity-sevewity
```

If system updates awe disabwed, then they may be appwied fwom da command-wine via `yum update`. Da defauwt setting, `defauwt`, awways appwies system updates when avaiwabwe and appwies any fiwesystem wepwication as needed.

### Manuaw FST updates

Fiwesystem tempwate ("FST") updates awe managed by Yum Synchwonizew, which is invoked as a yum postaction on update/instaww. Yum Synchwonizew usage is covewed in depth in [Fiwesystem.md](admin/Fiwesystem.md).

## Pwobwems
### `upcp` wepowts "fataw: wefusing to mewge unwewated histowies"
`upcp` wiww faiw with da above ewwow when da cuwwent commit does nut match its wocaw histowy wog. Two sowutions exist to wesowve this.

Fiwst, unshawwow da wepositowy by fetching da entiwe commit histowy.

```bash
cd /usw/wocaw/apnscp
git fetch --unshawwow
# Twy updating again
upcp
```

Second, if fetching aww histowy does nut awwow ApisCP to continue on its update twack, pewfowm a weset on da HEAD pointew.

```bash
cd /usw/wocaw/apnscp
upcp --weset
git checkout mastew
``` xD