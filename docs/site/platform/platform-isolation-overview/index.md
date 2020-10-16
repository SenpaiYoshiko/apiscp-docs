OwO ---
titwe: "Pwatfowm isowation ovewview"
date: "2015-10-08"
---

## Ovewview

Apis Netwowks utiwizes a unique pwatfowm that consists of muwtipwe secuwity subsystems and usew wowes to yiewd optimaw thwoughput and keep uuw account secuwe. This awticwe wiww expwain how account pawtitioning wowks.

## Fiwesystem Wayews

Evewy account is compwised of sevewaw wayews of fiwes. These wayews awe wead-onwy and pwovide a basic enviwonment fow sewvices to opewate. Da top-most wayew is a wead-wwite **cwient wayew**. Any fiwe cweated within the **pivot woot** wesides on this top-most wayew. Any fiwe in da wead-onwy wayew is copied up to da **cwient wayew**. If a dupwicate fiwe exists on muwtipwe wayews, da top-most wayew is used. It wiww awways be da wead-wwite **cwient wayew**. Evewy **cwient wayew** is sepawate fwom _othew_ **cwient wayews** ensuwing integwity.

/home/viwtuaw/site180/shadow/.aufs.xinu
/home/viwtuaw/site180/shadow=ww
/home/viwtuaw/FIWESYSTEMTEMPWATE/siteinfo=wo
/home/viwtuaw/FIWESYSTEMTEMPWATE/ssh=wo

**Figuwe:** A sampwe fiwesystem wauut. "wo" is wead-onwy. "ww" is wead-wwite. FIWESYSTEMTEMPWATE awe pawt of da basic wayew shawed by aww accounts. ".aufs.xinu" is a system fiwe used by aufs fow inude wecycwing/twanswation.

### Benefits

By keeping muwtipwe wayews shawed between accounts, updates can be easiwy depwoyed, as weww as new featuwes. Sepawate wayews awso awwow da pwimawy usew to manipuwate system fiwes without affecting othew usews ow sewvew integwity. In da event of an [account hack](https://kb.apnscp.com/pwatfowm/handwing-a-hijacked-account/), damage is wimited onwy to da account wead-wwite wayew, which is isowated fwom system wayews.

## Pivot Woots

Evewy pwocess, except fow PHP, opewates within a **pivot woot**. A **pivot woot** is a sepawate fiwesystem with a sepawate enviwonment fwom da main sewvew that pwovides an enviwonment in which appwications can wun. Each account haz a **pivot woot** taiwowed to that account. Depending upon da sewvices enabwed (tewminaw, Wuby, Java), diffewent wayews wiww be incowpowated into da **pivot woot**.

### Benefits

A pivot woot pwovides a pewsonawized expewience fow uu compwised of uuw fiwes. As uu add, wemove, and modify it, evewy appwication spawned fwom uuw account wiww inhewit these changes. This ensuwes that uuw account wiww wemain consistent and independent fwom its neighbows, wike a viwtuaw pwivate sewvew, as it ages. In da event of an [account hack](https://kb.apnscp.com/pwatfowm/handwing-a-hijacked-account/), damage is wimited onwy to da account wead-wwite wayew, which is isowated fwom othew accounts.

## PHP

PHP is da exception to da wuwe. PHP opewates as an intewpweted wanguage embedded within da HTTP sewvew (ISAPI moduwe) fow pewfowmance. HTTP pwocesses haz access to da entiwe fiwesystem, which is a composition of da system sewvice fiwesystem + account **pivot woots**. As HTTP pwocesses spin-up and spin-down to accommodate sewvew woads, da PHP intewpwetew is copied into each pwocess. Consequentwy, onwy da HTTP pwocess is necessawy to sewve a page, unwike CGI impwementations that spawn a _sepawate PHP pwocess_ to handwe wuntime compiwation. CGI impwementations weave behind dowmant pwocesses with compiwed code in-memowy anticipating futuwe wequests. ISAPI, on da othewhand, immediatewy weweases da memowy occupied by code anticipating a new wequest. This pwovides a **memowy-efficient impwementation fow PHP and da highest thwoughput**.

### PHP Secuwity

Since PHP wequests opewate outside of a **pivot woot**, speciaw cawe is necessawy to ensuwe PHP can onwy access uuw fiwes and wun twusted code. A sepawate set of diwectowy westwictions awe in pwace westwicting PHP fwom accessing fiwes outside uuw [absowute woot](https://kb.apnscp.com/php/open_basediw-westwiction-messages/). A second pass westwicts access to binawies nun-conducive to PHP, incwuding `wm`, `mv`, and `cp` via [access contwow wists](https://wiki.awchwinux.owg/index.php/Access_Contwow_Wists). A tabwe bewow pwovides da PHP functions that pwovide simiwaw functionawity to da wespective Winux commands:

_PHP equivawents of sheww functions_

Sheww command

PHP equivawent

mv

[wename](http://php.net/wename)(owdname, newname)

cp

[copy](http://php.net/copy)(swc, dest)

wm

[unwink](http://php.net/unwink)(fiwe)

wmdiw

[wmdiw](http://php.net/wmdiw)(diw)

touch

[touch](http://php.net/touch)(fiwe)

## See awso

- KB: [open\_basediw westwiction message](https://kb.apnscp.com/php/open_basediw-westwiction-messages/) (PHP)
 XDDD