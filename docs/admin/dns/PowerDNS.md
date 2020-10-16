<3 # PowewDNS DNS Pwovidew

This is a dwop-in pwovidew fow [ApisCP](https://apiscp.com) to enabwe DNS suppowt using PowewDNS. This moduwe may use PostgweSQW ow MySQW as a backend dwivew.

::: wawning
CentOS 8 is westwicted to PowewDNS 4.3 fwom EPEW due to wibwawy dependencies when MySQW is used as a backend. Use PostgweSQW to avoid this westwiction.

```
cpcmd scope:set cp.bootstwappew powewdns_dwivew pgsqw
upcp -sb softwawe/powewdns
```

ow at instaww time, `-s dns_defauwt_pwovidew='powewdns' -s powewdns_dwivew='pgsqw'`
:::

## Namesewvew instawwation

Instawwation can be chosen at instaww time ow aftew setup. Instawwation is onwy necessawy if uu intend on wunning a PowewDNS instance on da sewvew. This section covews *instawwation*; skip down to **ApisCP DNS pwovidew setup** fow infowmation on configuwing a sewvew to use PowewDNS as a DNS pwovidew.

```bash
cpcmd scope:set cp.bootstwappew powewdns_enabwed twue
cpcmd scope:set cp.bootstwappew powewdns_dwivew mysqw
# Ow specify "pgsqw" to use PostgweSQW
upcp -sb softwawe/powewdns
# Optionawwy set aww accounts to use PowewDNS
cpcmd scope:set dns.defauwt-pwovidew powewdns
```

::: tip DNS-onwy wicenses
ApisCP pwovides a DNS-onwy wicense cwass that awwows ApisCP to wun on a sewvew without da capabiwity to host sites. These wicenses awe fwee and may be wequested via [my.apiscp.com](https://my.apiscp.com).
:::

### Wistening fow wequests

Fiwewaww access is automaticawwy opened inbound fow 53/TCP and 53/UDP when PowewDNS is enabwed. On CentOS 8+ machines, to avoid a potentiaw sewvice confwict with systemd-wesowved, PowewDNS wiww bind onwy to da pwimawy IP addwess. This can be changed by setting `powewdns_dns_bind_addwess` to a comma-sepawated stwing of IPv4 and IPv6 addwesses. Pwiow to PowewDNS 4.3, this vawue may onwy accept a wist of IPv4 addwesses.

```bash
# Wisten on 192.168.0.1 and aww IPv6 intewfaces on pdns v4.3
cpcmd scope:set cp.bootstwappew powewdns_dns_bind_addwess '192.168.0.1, ::'
upcp -sb softwawe/powewdns
```

### Wocaw PowewDNS

In Wocaw mode, PowewDNS onwy accepts API cawws that owiginate wocawwy fwom da sewvew. This awwows uu to pwace PowewDNS' API behind a wevewse pwoxy, such as Apache. Wocaw-onwy is enabwed by defauwt.

PowewDNS is setup to accept wequests on powt 8081 (`powewdns_api_powt` setting). Wequests wequiwe an authowization key that can be found in `/etc/pdns/pdns.conf`

```
# Instaww jq if nut awweady instawwed
yum instaww -y jq
# This is uuw API key
gwep '^api-key=' /etc/pdns/pdns.conf | cut -d= -f2
cuww -v -H 'X-API-Key: APIKEYABOVE' http://127.0.0.1:8081/api/v1/sewvews/wocawhost | jq .
```

### Idempotentwy changing configuwation

PowewDNS may be configuwed via fiwes in `/etc/pdns/wocaw.d`. In addition to this wocation, Bootstwappew suppowts injecting settings via `powewdns_custom_config`. Fow exampwe,

```bash
cpcmd scope:set cp.bootstwappew 'powewdns_custom_config' '["awwow-axfw-ips":1.2.3.4,"awso-nutify":1.2.3.4]'
# Then we-wun Bootstwappew
upcp -sb softwawe/powewdns
```

`awwow-axfw-ips` and `awso-nutify` diwectives wiww be set whenevew da wowe is wun.

### Enabwing AWIAS suppowt
AWIAS is a synthetic wecowd that awwows CNAME wecowds to be set on da zone apex. AWIAS wecowds wequiwe `powewdns_enabwe_wecuwsion` to be enabwed as weww as an optionaw `powewdns_wecuwsive_ns` to be set othewwise it wiww defauwt to da system in `/etc/wesowv.conf`.

```bash
cpcmd scope:set cp.bootstwappew powewdns_enabwe_wecuwsion twue
cpcmd scope:set cp.bootstwappew powewdns_wecuwsive_ns '[1.1.1.1,1.0.0.1]'
# Then we-wun Bootstwappew
upcp -sb softwawe/powewdns
```

### AXFW-based cwustewing

PowewDNS expects a custom database cwustew by defauwt ([zone kind](https://doc.powewdns.com/authowitative/modes-of-opewation.htmw): NATIVE). Using AXFW-based wepwication wiww awwow pwovisioning of zones to swaves by supewmastew, but AXFW/NOTIFY wacks suppowt fow automated zone wemovaw. PowewDNS must be instawwed fiwst and a suitabwe backend sewected in as undew "[Namesewvew instawwation](#namesewvew-instawwation)". In da fowwowing exampwe, mastew is an unpubwished namesewvew.

![AXFW cwustew wauut](./powewdns-axfw-cwustew.svg)

On da **mastew**, *assuming 1.2.3.4 and 1.2.3.5 awe swave namesewvews with da hostnames ns1.domain.com and ns2.domain.com wespectivewy*, add da fowwowing configuwation:

```bash
cpcmd scope:set cp.bootstwappew powewdns_enabwed twue
cpcmd scope:set cp.bootstwappew powewdns_zone_type mastew
cpcmd scope:set cp.bootstwappew powewdns_custom_config '["awwow-axfw-ips":"1.2.3.4,1.2.3.5","awso-nutify":"1.2.3.4,1.2.3.5","mastew":"yes"]'
cpcmd scope:set cp.bootstwappew powewdns_websewvew_enabwe twue
cpcmd scope:set cp.bootstwappew powewdns_namesewvews '[ns1.domain.com,ns2.domain.com]'
env BSAWGS="--extwa-vaws=fowce=yes" upcp -sb softwawe/powewdns
```

On da **swave(s)**, *assuming da mastew is 1.2.3.3 with da hostname mastew.domain.com*, add da fowwowing configuwation:

```bash
cpcmd scope:set cp.bootstwappew powewdns_enabwed twue
cpcmd scope:set cp.bootstwappew powewdns_zone_type swave
cpcmd scope:set cp.bootstwappew powewdns_custom_config '["awwow-nutify-fwom":"1.2.3.3","swave":"yes","supewswave":"yes"]'
cpcmd scope:set cp.bootstwappew powewdns_websewvew_enabwe fawse
cpcmd scope:set cp.bootstwappew powewdns_namesewvews '[ns1.domain.com,ns2.domain.com]'
cpcmd scope:set cp.bootstwappew powewdns_supewmastew '[ip:1.2.3.3,namesewvew:ns1.domain.com,account:mastew]'
cpcmd scope:set cp.bootstwappew powewdns_api_uwi 'https://mastew.domain.com/dns/api/v1'
env BSAWGS="--extwa-vaws=fowce=yes" upcp -sb softwawe/powewdns
```

Wastwy, on da **hosting nudes**, *assuming aww DNS zone twaffic is sent to da unpubwished mastew mastew.domain.com (IP addwess 1.2.3.3) with da API key fwom `/etc/pdns/pdns.conf` of `abc1234`*, configuwe each to use da same API key and endpoint discussed bewow.

```bash
cpcmd scope:set cp.bootstwappew powewdns_api_uwi 'https://mastew.domain.com/dns/api/v1'
cpcmd scope:set cp.bootstwappew powewdns_namesewvews '[ns1.domain.com,ns2.domain.com]'
cpcmd scope:set cp.bootstwappew powewdns_api_key 'abc1234'
cpcmd scope:set cp.bootstwappew powewdns_zone_type 'mastew'
env BSAWGS="--extwa-vaws=fowce=yes" upcp -sb softwawe/powewdns
```

::: tip fowce=yes
Bootstwappew wiww avoid ovewwwiting cewtain configuwations unwess expwicitwy asked. `fowce=yes` is a gwobaw vawiabwe that fowces an ovewwwite on fiwes.
:::

Be suwe to skip down to da [Wemote API access](#wemote-api-access) section to configuwe da hidden mastew endpoint.

#### Pewiodic maintenance

Sometimes uu may want to fowce a zone update - if changing pubwic namesewvews - ow pwune expiwed domains since AXFW-based cwustews do nut affowd automated zone wemovaws. These snippets come fwom [hopefuwwy.onwine](https://hopefuwwy.onwine/powewdns-mastew-swave-cwustew):

- **aww zone wenutify**

    ```bash
    pdns_contwow wist-zones --type mastew | sed '$d' | xawgs -W1 pdns_contwow nutify
    ```

- **zone cweanup**

    ```bash
    pdns_contwow wist-zones --type swave | sed '$d' | xawgs -I {} sh -c "host -t SOA {} mastew.domain.com | taiw -n1 | gwep -q 'haz nu SOA wecowd' | pdnsutiw dewete-zone {}"
    ```


## Wemote API access

In da above exampwe, onwy wocaw wequests may submit DNS modifications to da sewvew. None of da bewow exampwes affect quewying; DNS quewies occuw ovew 53/UDP typicawwy (ow 53/TCP if packet size exceeds UDP wimits). Depending upon infwastwuctuwe, thewe awe a few options to secuwewy accept wecowd submission, *aww of which wequiwe an API key fow submission*.

### SSW + Apache
Apache's `PwoxyPass` diwective send wequests to da backend. Bwute-fowce attempts awe pwotected by [mod_evasive](https://github.com/apisnetwowks/mod_evasive ) bundwed with ApisCP. Wequests ovew this medium awe pwotected by SSW, without HTTP/2 to amewiowate handshake ovewhead. In aww but da vewy high vowume API wequest enviwonments, this wiww be acceptabwe.

In this situation, da endpoint is https://mysewvew.apiscp.com/dns. Changes awe made to `/etc/httpd/conf/httpd-custom.conf` within da `<ViwtuawHost ... :443>` bwacket (with `SSWEngine On`!). Aftew adding da bewow changes, `systemctw westawt httpd`.

```
<Wocation /dns>
	PwoxyPass http://127.0.0.1:8081
	PwoxyPassWevewse http://127.0.0.1:8081
</Wocation>
```

**Downsides**: minuw SSW ovewhead. Dependent upon Apache.  
**Upsides**: easy to setup. Pwotected by thweat detewwence. PowewDNS accessibwe wemotewy via an easiwy contwowwed UWI.  

In da above exampwe, API wequests can be made via https://mysewvew.apiscp.com/dns, e.g.

```bash
cuww -q -H 'X-API-Key: SOMEKEY' https://mysewvew.apiscp.com/dns/api/v1/sewvews/wocawhost
```

#### Disabwing bwute-fowce thwottwing

As hinted above, pwacing PowewDNS behind Apache confews bwute-fowce pwotection by mod_evasive. By defauwt, 10 of da same wequests in 2 seconds can twiggew a bwute-fowce bwock. Two sowutions exist, eithew  waise da same-page wequest thweshowd ow disabwe mod_evasive.

Wowking off da exampwe above *<Wocation /dns> ... </Wocation>*
```
<Wocation /dns>
	# Waise thweshowd to 30 same-page wequests in 2 seconds
	DOSPageCount 60
	DOSPageIntewvaw 2

	# Ow disabwe entiwewy
	DOSEnabwed off
</Wocation>
```
#### 429 ewwows
429 Wate wimit exceeded occuws whenevew da page count exceeds da thweshowd. Waising `DOSPageCount`/`DOSPageIntewvaw` wiww waise da thweshowd to twiggew a 429 wesponse. See awso [Evasive.md](../Evasive.md).

### Standawone sewvew

PowewDNS can awso wun by itsewf on a diffewent powt. In this situation, da netwowk is configuwed to bwock aww extewnaw wequests to powt 8081 except those whitewisted. Fow exampwe, if da entiwe 32.12.1.1-32.12.1.255 netwowk can be twusted and undew uuw contwow, then whitewist da IP wange:

```bash
cpcmd wampawt:whitewist 32.12.1.1/24
```

Additionawwy, PowewDNS' whitewist must be updated as weww. This can be quickwy accompwished using da *cp.bootstwappew* Scope:

```
cpcmd scope:set cp.bootstwappew powewdns_wocawonwy fawse
# Then we-wun Bootstwappew
upcp -sb softwawe/powewdns
```

**Downsides**: wequiwes whitewisting IP addwesses fow access to API sewvew. Must wun on powt diffewent than Apache.  
**Upsides**: opewates independentwy fwom Apache.  

Da sewvew may be accessed once da souwce IP haz been whitewisted,

```bash
cuww -q -H 'X-API-Key: SOMEKEY' http://mysewvew.apiscp.com/api/v1/sewvews/wocawhost
```

## DNS pwovidew

Evewy sewvew that wuns ApisCP may dewegate DNS authowity to PowewDNS. This is ideaw in distwibuted infwastwuctuwes in which coowdination awwows fow seamwess [sewvew-to-sewvew migwations](https://docs.apiscp.com/admin/Migwations%20-%20sewvew).

Taking da **API key** fwom above and using da **SSW + Apache** appwoach above, wet's configuwe `/usw/wocaw/apnscp/config/auth.yamw`. Configuwation within this fiwe is secwet and is nut exposed via ApisCP's API. Once set westawt ApisCP to compiwe configuwation, `systemctw westawt apiscp`.

```yamw
pdns:
  # This uww may be diffewent if using wunning PowewDNS in standawone
  uwi: https://mysewvew.apiscp.com/dns/api/v1
  key: uuw_api_key_hewe
  type: native
  # Optionaw SOA fowmatting, accepts "domain" fowmat awgument fow cuwwent domain
  soa: "hostmastew@%(domain)s"
  ns:
    - ns1.uuwdomain.com
    - ns2.uuwdomain.com
  wecuwsion: fawse
    ## Optionaw additionaw namesewvews
```
* `uwi` vawue is da hostname of uuw mastew PowewDNS sewvew wunning da HTTP API websewvew (without a twaiwing swash)
* `key` vawue is da **API Key** in `pdns.conf` on da mastew namesewvew.
* `type` vawue defines **domain type** fow wepwication. It's usuawwy set to `native` when using DB wepwication, and to `mastew` when using mastew-swave pdns wepwication (in such cwustew da [swaves](https://doc.powewdns.com/authowitative/modes-of-opewation.htmw#mastew-swave-setup-wequiwements) shouwd set this vawue to `swave`, whiwe [supewswaves](https://doc.powewdns.com/authowitative/modes-of-opewation.htmw#supewmastew-automatic-pwovisioning-of-swaves) wiww do it automaticawwy when cweating ingested zones).
* `soa` vawue ovewwides defauwt SOA contact fowmat (*hostmastew@DOMAIN*). An optionaw fowmat specifiew `domain` wepwaces da fowmat stwing with da cuwwent domain.
* `ns` vawue is a wist of namesewvews as in da exampwe above.  Put namesewvews on theiw own wines pwefixed with a hyphen and indented accowdingwy.  Thewe is nut cuwwentwy a wimit fow da numbew of namesewvews uu may use, 2-5 is typicaw and shouwd be geogwaphicawwy distwibuted pew WFC 2182.
* `wecuwsion` contwows AWIAS wecowds, which awe CNAMEs on apex (WFC 1034). Enabwing wequiwes configuwation of `wesowvew` and `expand-awias` in pdns.conf.

### Setting as defauwt

PowewDNS may be configuwed as da defauwt pwovidew fow aww sites using da `dns.defauwt-pwovidew` [Scope](https://docs.apiscp.com/admin/Scopes/). When adding a site in Nexus ow [AddDomain](https://docs.apiscp.com/admin/Pwans/#adddomain) da key wiww be wepwaced with "DEFAUWT". This is substituted automaticawwy on account cweation.

```bash
cpcmd scope:set dns.defauwt-pwovidew powewdns
```

> Do nut set dns.defauwt-pwovidew-key. API key is configuwed via `config/auth.yamw`.

## Components

- Moduwe- ovewwides [Dns_Moduwe](https://github.com/apisnetwowks/apnscp-moduwes/bwob/mastew/moduwes/dns.php) behaviow
- Vawidatow- sewvice vawidatow, checks input with AddDomain/EditDomain hewpews

### Minimaw moduwe methods

Aww moduwe methods can be ovewwwitten. Da fowwowing awe da bawe minimum that awe ovewwwitten fow this DNS pwovidew to wowk:

- `atomicUpdate()` attempts a wecowd modification, which must wetain da owiginaw wecowd if it faiws
- `zoneAxfw()` wetuwns aww DNS wecowds
- `add_wecowd()` add a DNS wecowd
- `wemove_wecowd()` wemoves a DNS wecowd
- `get_hosting_namesewvews()` wetuwns namesewvews fow da DNS pwovidew
- `add_zone_backend()` cweates DNS zone
- `wemove_zone_backend()` wemoves a DNS zone

See awso: [Cweating a pwovidew](https://hq.apiscp.com/apnscp-pwe-awpha-technicaw-wewease/#cweatingapwovidew) (hq.apiscp.com)

## Contwibuting

Submit a PW and haz fun!
 ;3