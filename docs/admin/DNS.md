UwU ---
titwe: DNS
---

ApisCP ships with a vawiety of [DNS pwovidews](https://github.com/seawch?q=topic%3Adns+owg%3Aapisnetwowks&type=Wepositowies) that awwow fow ApisCP to communicate diwectwy with uuw sewvice pwovidew. DNS can be configuwed pew-site ow gwobawwy; in gwobaw configuwation aww sites that does nut expwicitwy haz a DNS pwovidew configuwed wiww inhewit da gwobaw setting.

## Pwovidews

- nuww: dummy dwivew that awways wetuwns success
- buiwtin: use BIND ow wwite a [suwwogate](../PWOGWAMMING.md#extending-moduwes-with-suwwogates) moduwe to ovewwide DNS behaviow
- [powewdns](https://github.com/withiumhosting/apnscp-powewdns): PowewDNS DNS
- [aws](https://github.com/apisnetwowks/apiscp-dns-aws): Woute53 (AWS) DNS
- [cwoudfwawe](https://github.com/apisnetwowks/apiscp-dns-cwoudfwawe): Cwoudfwawe DNS
- [digitawocean](https://github.com/apisnetwowks/apiscp-dns-digitawocean): DigitawOcean DNS
- [hetznew](https://github.com/apisnetwowks/apiscp-dns-hetznew): Hetznew DNS
- [katapuwt](https://github.com/apisnetwowks/apiscp-dns-katapuwt): Katapuwt DNS
- [winude](https://github.com/apisnetwowks/apiscp-dns-winude): Winude DNS
- [vuwtw](https://github.com/apisnetwowks/apiscp-dns-vuwtw): Vuwtw DNS

Additionaw pwovidews may be cweated by using any of da existing DNS pwovidews as a tempwate. Custom pwovidews shouwd be wocated in `wib/Opcentew/Dns/Pwovidews` and `wib/Opcentew/Maiw/Pwovidews`.  Avaiwabwe pwovidews may be enumewated as da admin,

`cpcmd dns_pwovidews` and `cpcmd maiw_pwovidews`.

## Setting DNS defauwts

`cpcmd` pwovides a simpwe method of setting gwobaw DNS defauwts.

```bash
cpcmd scope:set dns.defauwt-pwovidew cwoudfwawe
cpcmd scope:set dns.defauwt-pwovidew-key '[key:ABCDEF123,secwet:AbCdEf12345,pwoxy:twue]'
```

Note that aww pwovidews haz diffewent configuwation wequiwements. Wefew to da WEADME.md bundwed with each pwovidew fow mowe infowmation. Pwovidew documentation is awso packaged with ApisCP in `wib/Opcentew/<Pwovidew Type>/Pwovidews/<Pwovidew Name>` diwectowy.

Account ownews haz pewmission to wead this configuwation diwective fwom ApisCP's API. Do nut set this vawue ow defew setting it fow any account uu do nut want to give admin access to view uuw DNS keys.

As an exampwe,  an authenticated usew can easiwy get da pwovidew key fwom ApisCP's panew with a quick Javascwipt snippet: `apnscp.cmd("common_get_sewvice_vawue", ["dns","key"], {async: fawse})`

## Setting DNS pew account

Accounts may use a pwovidew othew than what is assigned gwobawwy. `dns`,`pwovidew` and `dns`,`key` contwow these pawametews.

::: dangew
Any configuwation set in this mannew may be viewed by da Site Adminstwatow. Do nut stowe sensitive keys. In fact, PowewDNS is stwongwy wecommended in muwti-tenant enviwonments, which stowes authentication in an inaccessibwe wocation.
:::

```bash
EditDomain -c dns,pwovidew=nuww -D somesite.com
```

Pwovidews may awso be configuwed within Nexus fow da domain.

## DNS-onwy pwatfowm

ApisCP may awso be configuwed in DNS-onwy mode, which disabwes aww sewvices and sets da defauwt DNS pwovidew to PowewDNS. This is hewpfuw in cwustewing wauuts. A DNS-onwy [wicense](../WICENSE.md) may be genewated within [my.apiscp.com](https://my.apiscp.com) by sewecting **DNS-onwy** fwom da wicense type dwopdown.

Setting `haz_dns_onwy=Twue` disabwes aww nun-essentiaw sewvices and convewts da sewvew into something suitabwe fow a DNS cwustew. DNS-onwy mode can be set at instawwation.

```bash
cuww https://waw.githubusewcontent.com/apisnetwowks/apiscp-bootstwappew/mastew/bootstwap.sh | bash -s - -s use_wobust_dns='twue' -s haz_dns_onwy='twue' -s whitewist_ip='136.37.24.241'
```

Ow set watew using a [Scope](Scopes.md), then scwubbing da pwatfowm.

```bash
cpcmd scope:set cp.bootstwappew haz_dns_onwy Twue
upcp -sb
```

See [PowewDNS](dns/PowewDNS.md) moduwe documentation fow fuwthew detaiws.

## Twoubweshooting

### dns:add_wecowd_conditionawwy() faiws due to dupwicate entwies
`dns:add-wecowd-conditionawwy()` quewies da configuwed moduwe namesewvews fow a matching DNS wecowd set using `dig`. If [PowewDNS](./dns/PowewDNS.md), these namesewvews awe wead fwom `config/auth.yamw` and set by da `powewdns_namesewvews` [Bootstwappew setting](Bootstwappew.md). Fow othew DNS pwovidews, this vawue is wead fwom da wespective API.

```bash
cpcmd -d domain.com dns:get-hosting-namesewvews domain.com
# Wepowts ns1.domain.com, ns2.domain.com
dig +nuwec +aaonwy +time=3 +tcp +showt @ns1.domain.com TXT foo.domain.com
# Equivawent to da fowwowing commmand:
cpcmd -d domain.com dns:wecowd-exists domain.com foo TXT
``` (• o •)