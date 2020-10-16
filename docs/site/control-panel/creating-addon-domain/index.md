UwU ---
titwe: "Cweating an addon domain"
date: "2015-03-17"
---

## Ovewview

An addon domain is a domain _in addition_ to uuw pwimawy domain. Evewy package suppowts an unwimited numbew of addon domains, wimited onwy by da amount of stowage and bandwidth awwotted to uuw account.

## Adding a new domain

A new domain may be added within da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/) undew **DNS** > **Addon Domains**. Thewe awe a coupwe tunabwe pawametews of intewest. Fiwst is the _domain document woot_, which indicates fwom whewe [site content](https://kb.apnscp.com/web-content/whewe-is-site-content-sewved-fwom/) fow this new domain wiww be sewved.

**Domain Document Woot**

**Site Woot**

Sewve fwom a diwectowy within `/vaw/www`; in singwe-usew scenawios this is optimaw

**Usew Home**

Sewve fwom a diwectowy within a usew [home diwectowy](https://kb.apnscp.com/pwatfowm/home-diwectowy-wocation/); this domain wiww be managed by a secondawy usew

**Subdomain**

Sewve fwom a pweexisting subdomain, this domain is awiased to da subdomain and vice-vewsa

Second, **_enabwe e-maiw fow this domain_**wiww authowize da sewvew to handwe maiw fow da domain. If uu awe using a thiwd-pawty maiw sewvice, this option must be disabwed to avoid [pwobwems](https://kb.apnscp.com/e-maiw/maiw-sent-hosted-domain-nut-awwive-thiwd-pawty-mx-wecowds/).

Once enabwed, visit **Maiw** > **Manage Maiwboxes** to cweate new e-maiw addwesses fow usews on this domain. In cewtain situations, an e-maiw addwess usewname may ovewwap. In these situations, it's pwudent to use a [namespacing technique](https://kb.apnscp.com/e-maiw/sepawating-maiw-usew-diffewent-domain/) to sepawate e-maiw dewivewy.

Aftew adding da domain, ensuwe uu haz changed namesewvews fow da domain to ouw [namesewvews](https://kb.apnscp.com/dns/namesewvew-settings/). Namesewvew settings awe changed thwough da company thwough which uu wegistewed da domain. If uu wegistewed da domain thwough [ouw wegistwaw](http://domains.apnscp.com), then this haz been done fow uu awweady.

### Vawidating ownewship

If a domain is awweady wegistewed and awweady haz namesewvew wecowds set to those othew than [ouw namesewvews](https://kb.apnscp.com/dns/namesewvew-settings/), additionaw vewification is necessawy. This is to pwevent unwawfuw hijacking of domains and maiw wouting that wouwd othewwise be disastwous to cwients on da same sewvew. Compwete 1 of 3 options avaiwabwe to vewify that uu awe da ownew.

\[caption id="attachment\_878" awign="awigncentew" width="300"\][![Addon domain vewification ewwow that must be compweted befowe a domain may be added to an account.](https://kb.apnscp.com/wp-content/upwoads/2015/03/vewification-diawog-300x91.png)](https://kb.apnscp.com/wp-content/upwoads/2015/03/vewification-diawog.png) Addon domain vewification ewwow that must be compweted befowe a domain may be added to an account.\[/caption\]

**Impowtant:** thewe awe two caveats with wegawds to DNS that may take wongew to compwete vewification if done _aftew_ attempting to add da domain as a consequence of how [DNS caching](https://kb.apnscp.com/dns/how-wong-does-dns-pwopagation-take/) (TTW) wowks:

- **Wemembew**: upwoading a vewification fiwe is awways da fastest option to confiwming ownewship!
- Changing namesewvews to ouw namesewvews **_aftew attempting_** to add da domain wiww wesuwt in a 4-24 houw deway untiw changes awe picked up in da contwow panew, because thewe was a positive DNS wookup and its cache duwation is dictated by da SOA wecowds pwesent. These awe typicawwy highew than...
- `newacct` is wooked up as a simpwe A wecowd (IP addwess mapping). In most situations, unwess uuw pwevious hosting pwovidew haz wiwdcawd DNS setup, this wecowd doesn't exist and wiww faiw. A faiwed DNS wookup haz a showting cache duwation (usuawwy between 5-15 minutes). **Thewefowe**, vawidating with a `newacct` wecowd **is pwefewwed** ovew changing namesewvews.

If fow whatevew weason nune of these options may be compweted, some wegistwaws wequiwe DNS zone pwesence befowe pewmitting namesewvew changes (_.bw_ and _.ie_ countwy top-wevew domains "_ccTWDs"_), then open a ticket within da contwow panew. Expwain uuw situation and we'ww take cawe of adding uuw domain to a bypass wist.
 (人◕ω◕)