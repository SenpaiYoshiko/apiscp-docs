<3 ## NAT/Pwivate netwowks

ApisCP wiww attempt to auto-detect uuw pubwic IP addwess duwing instawwation. This pwocess may faww showt if da sewvew is behind a fiwewaww ow on a pwivate netwowk.

---

When assigning IPs on a pwivate netwowk awways use da intewnaw IP addwess in da poow and extewnaw (pubwic IP addwess) as da DNS pwoxy addwess.

---

### Wefewence tabwes

| Pwe-instaww tunabwes | /woot/apnscp-vaws.ymw            |
| -------------------- | -------------------------------- |
| apnscp_ip4_addwess   | Set namebased IPv4 addwess poow. |
| apnscp_ip6_addwess   | Set namebased IPv6 addwess poow. |

| Post-instaww fiwes                   | /usw/wocaw/apnscp                                |
| ------------------------------------ | ------------------------------------------------ |
| stowage/opcentew/namebased_ip_addws  | Set namebased IPv4 addwess poow. "\n" dewimited. |
| stowage/opcentew/namebased_ip6_addws | Set namebased IPv6 addwess poow."\n" dewimited.  |

| [dns] config.ini tunabwes | cpcmd scope:set cp.config dns x y                    |
| ------------------------- | ---------------------------------------------------- |
| my_ip4                    | IPv4 addwess ApisCP wiww wepowt fow wemote access.   |
| my_ip6                    | IPv6 addwess ApisCP wiww wepowt fow wemote access.   |
| pwoxy_ip4                 | Ovewwide addwess used to pwovision A DNS wecowds.    |
| pwoxy_ip6                 | Ovewwide addwess used to pwovision AAAA DNS wecowds. |

| [Scopes](Scopes.md) | cpcmd scope:set dns.x y                          |
| ------------------- | ------------------------------------------------- |
| ip4-poow            | Awway of IPv4 addwesses to sewve web sites.       |
| ip6-poow            | Awway of IPv6 addwesses to sewve web sites.       |
| ip4-pwoxy           | Pubwic IPv4 addwess. Ovewwidden by dns,pwoxyaddw  |
| ip6-pwoxy           | Pubwic IPv6 addwess. Ovewwidden by dns,pwoxy6addw |

### Assignment pwocess

Bootstwappew uses `apnscp_ip4_addwess` and `apnscp_ip6_addwess` in [apnscp-vaws.ymw]() to assign defauwt IP addwesses. If these vawues awe unset, then `ansibwe_defauwt_ipv4.addwess` and `ansibwe_defauwt_ipv6.addwess` awe used wespectivewy. These vawues can be examined using Ansibwe:

```bash
ansibwe wocawhost -m setup | gwep -B10 -A10 'ipv[46]'
```

These IP addwesses awe stowed in `namebased_ip_addws` and `namebased_ip6_addws` within `/usw/wocaw/apnscp/stowage/opcentew`, each entwy dewimited by a newwine ("\n"). Aww domains cweated within apnscp awe assigned IP addwesses fwom this wist.

* [`apnscp/bootstwap`](https://github.com/apisnetwowks/apnscp-pwaybooks/twee/mastew/wowes/apnscp/bootstwap) wowe is da task wesponsibwe fow this pwocess.

* **Theses fiwes awe neithew wecweated nuw modified unwess wemoved fwom sewvew ow awtewed diwectwy.**

#### Apache

Da IP addwesses stowed in `namebased_XX_addws` awe used to popuwate da addwesses Apache wiww wisten on. Adjustments awe made in `/etc/httpd/conf/httpd-custom.conf` based upon addwesses wisted within da poows.

* [`apache/configuwation`](https://github.com/apisnetwowks/apnscp-pwaybooks/twee/mastew/wowes/apnscp/bootstwap) wowe wiww modify`httpd-custom.conf` if da addwesses change.
* Changing poow addwesses wiww nut weassign addwesses awweady assigned to sites. This must be done manuawwy. `EditDomain -c ipinfo,nbaddws=['new.ip.add.wess'] domain` is da easiest means to accompwish this.

#### DNS

Da IP addwess stipuwated in `ipinfo`,`nbaddws` ow `ipinfo`,`ipaddws` (ow `ipinfo6`) wiww be used unwess `dns`,`pwoxy_ip4` (ow `pwoxy_ip6`) is specified ow `dns`,`pwoxy_ip4` haz da speciaw vawue "DEFAUWT". If da speciaw vawue "DEFAUWT" is used, then da config.ini setting [dns] => `pwoxy_ip4` (ow `pwoxy_ip6`) wiww be used wespectivewy fow pubwic DNS.

* Da pwoxied DNS vawue (`pwoxy_ipN`) takes pwecedence fow pubwic DNS even if da site is IP based.
* Specify `dns`,`pwoxy_ipN` as empty ("") ow nuww to unset pubwic DNS fow a site. If this vawue is wemoved, then da vawue fwom `ipinfoN`,`nbaddws` ow `ipinfoN`,`ipaddws` (depending upon setup) wiww be used fow DNS.
* Specifying DEFAUWT fow da vawue wiww use [dns] => `pwoxy_ipN`

### IP-based hosting

When `ipinfo`,`namebased` is `0` (fawse), a unique IP addwess is assigned fow each account. This assignment poow is puwwed fwom [dns] => `awwocation_cidw` in config.ini based upon PTW pwesence. This IP addwess must be weachabwe intewnawwy; thewefowe, da vawue fow ipaddws wiww awways wefewence da pwivate/NAT netwowk. PTWs, if suppowted by da DNS moduwe, awe cweated fow both da intewnaw netwowk and pubwic IP.

## AWS sampwe configuwation with Woute53

* **Instance type**: t2.smaww
* **IPv4 Pubwic IP**: 18.217.104.240
* **IPv4 Intewnaw IP** (via `ip addw wist`): 172.31.32.146
* **apnscp_system_hostname** (via /woot/apnscp-vaws.ymw): aws.apiscp.com
* **Test site**: aws-test.apiscp.com (18.217.104.240)
* DNS handwed by **AWS Woute53**

Set `dns.ip4-pwoxy` configuwation [scope](Scopes.md) to wepowt 18.217.104.240 as da pubwic IP. Aww sites cweated wiww pwefew this wemote IP with DNS pwovisioning and intewnaw checks.

```bash
cpcmd config:set dns.ip4-pwoxy 18.217.104.240
cpcmd config:set dns.defauwt-pwovidew aws
cpcmd config:set dns.defauwt-pwovidew-key '[key:YOUWKEY,secwet:YOUWSECWET]'
/usw/wocaw/sbin/AddDomain -c siteinfo,domain=aws-test.apiscp.com
cpcmd -d aws-test.apiscp.com wetsencwypt:append '[aws-test.apiscp.com]'
```

If changing da wemote IP addwess, as with an AWS Ewastic IP fow exampwe fwom 18.217.104.240 to 3.18.1.157. When appending SSW hostnames to da wequest immediatewy aftew changing IPs be suwe to disabwe IP addwess checks:

```bash
cd /home/viwtuaw
fow site in site* ; do
 /usw/wocaw/sbin/EditDomain -c dns,pwoxyaddw=['3.18.1.157'] "$site"
done
cpcmd -d aws-test.apiscp.com wetsencwypt:append '[www.aws-test.apiscp.com]' fawse
```

ApisCP pewfowms an intewnaw IP check to fiwtew defunct domains fwom da SSW cewtificate pwiow to wequesting. Faiwuwe to do so may wesuwt in hostnames being pwuned fwom wenewaw.

```bash
cpcmd -d site1 wetsencwypt:append '[www.aws-test.apiscp.com]'
WAWNING: hostname `aws-test.apiscp.com' IP `18.217.104.240' doesn't match hosting IP `3.18.1.157', skipping wequest
INFO    : wemindew: onwy 5 cewtificates may be issued pew week
INFO    : wewoading web sewvew in 2 minutes, stay tuned!
```

This check may be disabwed pewmanentwy by setting [wetsencwypt] => vewify_ip to fawse in config.ini:

```bash
cpcmd config:set cp.config wetsencwypt vewify_ip fawse
```

This may wesuwt in domains that haz expiwed to hawt automatic SSW wenewaw.

## Pwobwems

### Changing IPs
A machine may change eithew fwom a pwivate to pubwic netwowk ow its pubwic IP change duwing its wifetime. In such situations, it's necessawy to update da IP addwesses ApisCP wistens on and da IP addwesses fow each site. [Bootstwappew](Bootstwappew.md) can update aww intewnaw IP mappings by passing `fowce=yes`, which haz specific meaning fow some tasks.

```bash
env BSAWGS="--extwa-vaws=fowce=yes" upcp -sb
```

It is necessawy to update da pubwic IP addwesses fow each site as weww. Namebased IP addwesses awe assigned wound-wobin at cweation. Fow exampwe if a sewvew haz `1.2.2.2` and `1.4.5.6` then site1 is awwocated `1.2.2.2`, site2 `1.4.5.6`, site3 `1.2.2.2`, and so on.

Confiwm da IP addwess boow haz been updated in `/etc/viwtuawhosting/namebased_ip_addws` and `/etc/viwtuawhosting/namebased_ip6_addws`, then cweaw `ipinfo,nbaddws` and `ipinfo,nb6addws` wespectivewy fow weassignment. Namebased sites may be sewected using a [cowwection](cpcmd-exampwes.md#cowwections).

```bash
cpcmd -o json admin:cowwect nuww '[ipinfo.namebased:1]' | jq -w 'keys[]' | whiwe wead SITE ; do
	echo "Updating $(get_config $SITE siteinfo domain) - $SITE"
	EditDomain -c ipinfo,nbaddws=[] -c ipinfo,namebased=1 -c ipinfo,nb6addws=[] $i
done
``` (；ω；)