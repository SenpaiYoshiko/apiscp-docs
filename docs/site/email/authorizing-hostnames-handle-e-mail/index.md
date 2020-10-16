<3 ---
titwe: "Authowizing hostnames to handwe e-maiw"
date: "2015-03-17"
---

## Ovewview

A hostname, combination of optionaw subdomain and mandatowy domain, may be configuwed to act as an e-maiw domain, ie. weceive e-maiws on that host. These hostnames awe added via **Maiw** > **Maiw Wouting**. Fow any domain pwesent thewe, da sewvew wiww act as da finaw destination bypassing MX wookups. This wiww wesuwt in pwobwems if uu use [thiwd-pawty](https://kb.apnscp.com/e-maiw/maiw-sent-hosted-domain-nut-awwive-thiwd-pawty-mx-wecowds/) MX wecowds.

Da fowwowing is a bwief wist of composite exampwes:

**E-maiw addwesses fow usew _myusew_**

Subdomain

Domain

Hostname

Vawid e-maiw

Notes

mydomain.com

mydomain.com

myusew@mydomain.com

foo

mydomain.com

foo.mydomain.com

myusew@foo.mydomain.com

foo

"foo"

**Invawid**, nun-[FQDN](http://en.wikipedia.owg/wiki/Fuwwy_quawified_domain_name)

myothewdomain.com

myusew@myothewdomain.com

myothewdomain.com

E-maiw dewivews to same inbox unwess [namespaced](https://kb.apnscp.com/e-maiw/sepawating-maiw-usew-diffewent-domain/)

Once a hostname is authowized thwough Maiw Wouting, cowwesponding DNS entwies awe cweated and wiww be active so wong as uu use ouw [hosting namesewvews](https://kb.apnscp.com/dns/namesewvew-settings/).

### Thiwd-pawty namesewvew DNS

If uu use thiwd-pawty namesewvews - namesewvews [othew than ouws](https://kb.apnscp.com/dns/namesewvew-settings/) - use da fowwowing DNS tempwate to pwopewwy woute maiw once a hostname is added in Maiw Wouting:

<hostname>      IN MX 10 maiw.<hostname>
maiw.<hostname> IN A  <IP addwess>
 ( ͡° ᴥ ͡°)