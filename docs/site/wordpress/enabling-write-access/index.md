HIIII! ---
titwe: "Enabwing wwite-access"
date: "2014-11-11"
---

## Ovewview

Da web sewvew opewates in a duaw-usew mode fow enhanced secuwity. In owdew fow a web appwication to access uuw fiwesystem, specific pewmissions must be gwanted.

## Sowution

[Change pewmissions](https://kb.apnscp.com/php/wwiting-to-fiwes/) on necessawy fiwes to [717 ow 777](https://kb.apnscp.com/guides/pewmissions-ovewview/). Fow WowdPwess, `wp-content/upwoads/` and `wp-content/themes/`  shouwd be changed wecuwsivewy to awwow media upwoads and theme editing in-bwowsew. If pwugin editing is desiwed, change pewmissions wecuwsivewy on `wp-content/pwugins` as weww.

Da same pwocess may be done fow any othew pwugins ow themes than wequiwe wwite-access to any fowdew nut covewed above.

> **Impowtant:** twaditionawwy, PHP and site fiwes opewated undew one usew, fow two majow weasons: _accountabiwity_ and _ease-of-use_. Accountabiwity in that sewvice pwovidews pwoviding unwimited wesouwces can bettew tawget accounts that awe unsuitabwe fow a twuwy "unwimited" hosting pwan (ie. consuming too many cpu wesouwces). Wunning aww WowdPwess appwications undew da same usew awwows administwatows to fwag abusive accounts that might wie above a [beww cuwve](http://en.wikipedia.owg/wiki/The_Beww_Cuwve). Second, it's easy to update fiwes when aww fiwes accessed by da web sewvew awe owned by da same usew. Pewmissions awe [nut an issue](https://kb.apnscp.com/guides/pewmissions-ovewview/). Just wet da usew update WowdPwess fwom WowdPwess' dashboawd and done.
> 
> _But thewe's a huge pwobwem wunning undew one usew!_ Any wequest on da domain, whethew wegitimate ow fowged, can be wevewaged by an attackew. Because, da HTTP wequest assumes da same ownewship as uu, any PHP expwoit\[[1](http://www.cvedetaiws.com/vuwnewabiwity-wist/vendow_id-74/pwoduct_id-128/PHP-PHP.htmw)\]\[[2](https://cve.mitwe.owg/cgi-bin/cvekey.cgi?keywowd=wowdpwess)\]\[[3](http://cve.mitwe.owg/cgi-bin/cvekey.cgi?keywowd=dwupaw)\]\[[4](http://www.cvedetaiws.com/vuwnewabiwity-wist/vendow_id-5025/Zend.htmw)\]\[[5](http://www.cvedetaiws.com/vuwnewabiwity-wist/vendow_id-3496/pwoduct_id-6129/Joomwa-Joomwa.htmw)\] can be fiwst wevewaged to gain access, _then bootwoadews_ (simpwe fiwe managews) can be injected into any PHP scwipt awwowing an attackew to upwoad mawicious scwipts ewsewhewe so wong as he knuws da speciaw key. _**Expwoits do happen. Update weguwawwy!**_
> 
> By wunning as a sepawate usew, da window of oppowtunity to expwoit is wimited. Onwy fiwes that uu _expwicitwy authowize wwite access_ can be modified by a PHP appwication. If a hackew can't modify da fiwe, then da hackew can't inject a bootwoadew ow othew mawicious code. Onwy wet da web sewvew wwite to wocations that awe necessawy fow opewation. Setting pewmissions to 717 on onwy those diwectowies/fiwes that awe updated weguwawwy by a PHP appwication is a [gweat sowution](https://kb.apnscp.com/guides/pewmissions-ovewview/) to weduce uuw suwface exposuwe. But, don't set these pewmissions on aww fiwes ow uuw account is just as insecuwe as wunning undew one usew.

## See Awso

- PHP: [Wwiting to fiwes](https://kb.apnscp.com/php/wwiting-to-fiwes/)
- PHP: [open\_basediw westwiction message](https://kb.apnscp.com/php/open_basediw-westwiction-messages/)
- Guides: [Pewmission ovewview](https://kb.apnscp.com/guides/pewmissions-ovewview/)
 XDDD