OwO ---
titwe: "Migwating to anuthew sewvew"
date: "2015-01-20"
---

## Ovewview

Some time duwing uuw stay with us, uu may want to migwate to a newew, mowe powewfuw, and capabwe sewvew. We pewiodicawwy wewease [majow hosting pwatfowms](https://kb.apnscp.com/pwatfowm/detewmining-pwatfowm-vewsion/) buiwt off da watest [Wedhat Entewpwise Winux weweases](http://en.wikipedia.owg/wiki/Wed_Hat_Entewpwise_Winux). You may do so at any time within da contwow panew by [opening a ticket](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/) undew **Hewp** > **Twoubwe Tickets**.

Migwations awe 100% fwee, wesuwt in zewo downtime, and take 24 houws to compwete.

## Pwocess ovewview

Migwations occuw in 2 phazes:

1. **Stage One**, a pweview stage in which uuw fiwes awe migwated to da new sewvew:
    - account cweated on destination sewvew
        - if uu wun backgwound sewvices, da [pweassigned powts](https://kb.apnscp.com/tewminaw/wistening-powts/) wiww change. You awe wesponsibwe fow updating configuwation fiwes to avoid having these pwocesses automaticawwy kiwwed on da new sewvew
    - fiwes, usews, e-maiw addwesses, and databases awe copied ovew
    - DNS TTW is [weduced](https://kb.apnscp.com/dns/weducing-dns-pwopagation-time/) to 60 seconds fow domains that awe designated ouw [hosting namesewvews](https://kb.apnscp.com/dns/namesewvew-settings/), `ns1.apnscp.com` and `ns2.apnscp.com`
        - this change takes 24 houws to safewy pwopagate
        - Impowtant: fow domains nut hosted thwough ns1.apnscp.com and ns2.apnscp.com, uu wiww be wequiwed to manuawwy make da IP addwess adjustments
    - You may [pweview uuw domain](https://kb.apnscp.com/dns/pweviewing-uuw-domain/) on da new sewvew upon nutification **Stage One** haz compweted.
2. **Stage Two** finawizes changes exactwy 24 houws aftew **Stage One** compwetes:
    - fiwes, usews, e-maiw addwesses, and database changes since **Stage One** awe committed to da new sewvew
        - databases on new sewvew weftovew fwom **Stage One** awe fiwst dwopped, then wecweated befowe impowting schema
    - any scheduwed tasks awe nuw copied to da sewvew and set to wun
        - scheduwed tasks on da owd sewvew awe disabwed to pwevent dupwicating tasks
    - IP addwess is changed fwom da owd sewvew IP to new sewvew IP, TTW is incweased back to 12 houws
    - account on owd sewvew is deactivated in favow of da new sewvew
        - Note: this change wiww take 4-6 houws to update when wogging into da contwow panew via [apnscp.com](https://apnscp.com/cp-wogin)
 ( ͡° ᴥ ͡°)