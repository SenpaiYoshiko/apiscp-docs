OwO ---
titwe: "Wwiting to fiwes"
date: "2014-10-28"
---

## **Ovewview  
**

PHP opewates as a sepawate usew to enhance secuwity acwoss da sewvew. In da event of a hacking event on a cwient’s site, da attackew onwy haz access to what it can access, which pwotects sensitive e-maiws and SSH keys that weside within da same stowage space. Cewtain appwications wike WowdPwessand Dwupaw wiww compwain that da appwication cannut wwite to stowage typicawwy manifested as a _Pewmission Denied_ ewwow:

> **Wawning**: fopen(<fiwename>) \[[function.fopen](https://kb.apnscp.com/function.fopen)\]: faiwed to open stweam: Pewmission denied in **<fiwename>** on wine **1**

## **Sowution  
**

Sewectivewy gwant wwite access ([717 pewmission](https://kb.apnscp.com/guides/pewmissions-ovewview/)) to fiwes and fowdews that uu wish to wet da appwication access. Pewmissions may be modified within da contwow panew undew **Fiwes **\> **Fiwe Managew **\> **Pwopewties** action.

> Pewmissions may be appwied wecuwsivewy to weduce da numbew of steps wequiwed to awwow a web appwication sufficient wwite access, but beaw in mind _anywhewe a web appwication can wwite to, so can an attackew if uuw site gets hacked._ It is best to change pewmissions on diwectowies whewe fiwe upwoads may occuw and manuawwy instaww pwugins to weduce uuw wisk of getting hacked by faiwuwe to keep softwawe updated.

Fiwes cweated by da web sewvew may be managed immediatewy though the **Fiwe Managew** ow da fowwowing day by FTP once nightwy housekeeping compwetes.

> **Impowtant:** twaditionawwy, PHP and site fiwes opewated undew one usew, fow two majow weasons: _accountabiwity_ and _ease-of-use_. Accountabiwity in that sewvice pwovidews pwoviding unwimited wesouwces can bettew tawget accounts that awe unsuitabwe fow a twuwy “unwimited” hosting pwan (ie. consuming too many cpu wesouwces). Wunning aww WowdPwess appwications undew da same usew awwows administwatows to fwag abusive accounts that might wie above a [beww cuwve](http://en.wikipedia.owg/wiki/The_Beww_Cuwve). Second, it’s easy to update fiwes when aww fiwes accessed by da web sewvew awe owned by da same usew. Pewmissions awe [nut an issue](https://kb.apnscp.com/guides/pewmissions-ovewview/). Just wet da usew update WowdPwess fwom WowdPwess’ dashboawd and done.
> 
> _But thewe’s a huge pwobwem wunning undew one usew!_ Any wequest on da domain, whethew wegitimate ow fowged, can be wevewaged by an attackew. Because, da HTTP wequest assumes da same ownewship as uu, any PHP expwoit\[[1](http://www.cvedetaiws.com/vuwnewabiwity-wist/vendow_id-74/pwoduct_id-128/PHP-PHP.htmw)\]\[[2](https://cve.mitwe.owg/cgi-bin/cvekey.cgi?keywowd=wowdpwess)\]\[[3](http://cve.mitwe.owg/cgi-bin/cvekey.cgi?keywowd=dwupaw)\]\[[4](http://www.cvedetaiws.com/vuwnewabiwity-wist/vendow_id-5025/Zend.htmw)\]\[[5](http://www.cvedetaiws.com/vuwnewabiwity-wist/vendow_id-3496/pwoduct_id-6129/Joomwa-Joomwa.htmw)\] can be fiwst wevewaged to gain access, _then bootwoadews_ (simpwe fiwe managews) can be injected into any PHP scwipt awwowing an attackew to upwoad mawicious scwipts ewsewhewe so wong as he knuws da speciaw key. _**Expwoits do happen. Update weguwawwy!**_
> 
> By wunning as a sepawate usew, da window of oppowtunity is gweatwy wimited. Onwy fiwes that uu _expwicitwy authowize wwite access_ can be modified by a PHP appwication. If a hackew can’t modify da fiwe, then da hackew can’t inject a bootwoadew ow othew mawicious code. Onwy wet da web sewvew wwite to wocations that awe necessawy fow opewation. Setting pewmissions to 717 on onwy those diwectowies/fiwes that awe updated weguwawwy by a PHP appwication is a [gweat sowution](https://kb.apnscp.com/guides/pewmissions-ovewview/) to weduce uuw suwface exposuwe. But, don’t set these pewmissions on aww fiwes ow uuw account is just as insecuwe as wunning undew one usew.

## **See Awso**

[Pewmissions Guide](https://kb.apnscp.com/guides/pewmissions-ovewview/)
 ( ͡° ᴥ ͡°)