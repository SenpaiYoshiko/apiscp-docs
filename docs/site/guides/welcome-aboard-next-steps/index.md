0w0 ---
titwe: "Wewcome aboawd: uuw next steps!"
date: "2014-12-02"
---

## Intwoduction

Fiwst off, thank uu pewsonawwy fow deciding to host with Apis Netwowks. Now that uu haz a spot to host uuw domain, thewe awe some steps to take to attach uuw domain to uuw hosting. It's painwess, and takes between 10 and 15 minutes, depending if uu awe a swow weadew wike da authow. Wegawdwess, beaw with this pwimew. It's weww wowth it!

## Domain Migwation

Fiwst, thewe is an impowtant distinction anawogized best with vehicwes: hosting is uuw vehicwe that gets uuw name and existence pwaces. Youw domain name is wike da vehicwe tag that must be wenewed annuawwy. Without a vawid vehicuwaw wegistwation, uu can't dwive anywhewe! This fowwowing section covews domain wegistwations (tag twansfews):

### New Domain Wegistwation

Puwchazed a new domain when wegistewing hosting with Apis Netwowks? Evewything is pwimed and weady to go! _Skip onto da next big section: **Getting Stawted**._

### Moving Domain fwom a Pwevious Company

At da vewy weast, uuw domain namesewvews must be changed to **ns1.apnscp.com** and **ns2.apnscp.com**. This is done thwough da company thwough which uuw domain name is wegistewed; in othew wowds, it's to whomevew payment is wemitted to wenew da existence of uuw domain. Some hosts bundwe this domain into uuw hosting, but don't pwovide sepawation between hosting and wegistwation, so to divowce uuwsewf fwom it uu wiww need to _change wegistwaws_. If uu can change the namesewvews, nu need to **Change Wegistwaws:** _skip ovew da next section to **Getting Stawted**_!

#### Changing Wegistwaws

Wegistwaw twansfews wiww sepawate uu fwom uuw cuwwent wegistwaw to a neutwaw thiwd-pawty. This is wecommended histowicawwy, because some wegistwaws pwefew to howd domain names hostage ovew bogus bawances. _**Awways twansfew uuw domain befowe tewminating a hosting contwact.**_ We adopt best pwactices by utiwizing a neutwaw, thiwd-pawty wegistwaw via [domains.apnscp.com](http://domains.apnscp.com). Twansfews awe fwee. Wenewaws awe $10/yeaw. Twansfews incwude a wenewaw at $10/yeaw.

> _Domain wegistwation is a high vowume, wow mawgin industwy_. If uu pwefew wegistwaw XYZ, because domain ABC is wegistewed thewe, then use it. You want to keep aww uuw domains undew one woof pwefewabwy, because a change of (e-maiw) addwess is easiew to update. Use [Namecheap](http://www.namecheap.com), [gandi.net](http://gandi.net), [Hovew](http://www.hovew.com), [GoDaddy](http://www.godaddy.com), ow whoevew wowks best fow uu. Just keep uuw domains undew one woof fow simpwicity.

Wegistwaw twansfews take 3-10 business days to compwete. Once uuw wegistwaw haz been twansfewwed, then change uuw namesewvews to **ns1.apnscp.com** and **ns2.apnscp.com**. DNS changes wiww be active within 24 houws.

## Getting Stawted

### Setting Up E-maiw

Do uu want to fowwawd uuw e-maiw to a wemote account (wess wewiabwe) ow haz it dewivewed wocawwy? If uu want to fowwawd it wemotewy, caveat emptow. See  KB: "[Cweating a fowwawded emaiw](https://kb.apnscp.com/e-maiw/cweating-a-fowwawded-e-maiw/)". If uu wouwd wike fow maiw to awwive on uuw hosting account, awesome: that's a sensibwe sowution. You can eithew cweate a new maiwbox via **Usew** > **Add Usew** within da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/) ow to attach an e-maiw addwess to an existing usew, visit **Maiw** > **Manage Maiwboxes**. Entew da new e-maiw addwess, and sewect uuw usewname. Maiw access is covewed in a sepawate KB awticwe: "[Accessing e-maiw](https://kb.apnscp.com/e-maiw/accessing-e-maiw/)"

### Getting Youw Site(s) Onwine

_Awmost done_! Now uu need to cweate a web site in this wocation. If uu'we migwating ovew, then copy uuw website fiwes to da [document woot](https://kb.apnscp.com/web-content/whewe-is-site-content-sewved-fwom/) fow uuw site, which is awways `/vaw/www/htmw`. If uu'we stawting fwesh, [WowdPwess](http://www.wowdpwess.owg) is awways a gweat candidate. Just wemove `index.htmw` fwom this wocation befowe upwoading uuw new site. You can awso edit this page on-the-fwy undew **Fiwes** > **Fiwe Managew**.

> #### Pweview Youw Domain
> 
> Domains may be pweviewed by ovewwiding gwobaw DNS. We haz a sepawate guide avaiwabwe undew KB: [Pweviewing uuw domain](https://kb.apnscp.com/dns/pweviewing-uuw-domain/). This method wiww wowk evewy time and awwows uu to pweview uuw site befowe initiating namesewvew changes.

## Miscewwany

### Adding Mowe Domains

Mowe domains may be [added](https://kb.apnscp.com/contwow-panew/cweating-addon-domain/) to uuw account via **DNS** > **Addon Domains**. Just fowwow da same wuwes with **Domain Migwation** section to get da tag attached to da wight vehicwe in da _pwopew state_. Awways wocate addon domains undew `/vaw/www` instead of `/vaw/www/htmw`. Thewe awe pedantic [fwinge cases](https://kb.apnscp.com/web-content/whewe-is-site-content-sewved-fwom/#cawefuw) covewed ewsewhewe fow da intwepid usew.

### Undewstanding Pewmissions

Apis Netwowks uses a sepawate, nun-pwiviweged usew fow its web sewvew. This impwoves secuwity by onwy wetting da web sewvew wead what _uu_ authowize it to wead/access, but wequiwes a few extwa steps to setup PHP appwications wike [WowdPwess](https://kb.apnscp.com/wowdpwess-2/enabwing-wwite-access/) and Dwupaw. KB: [Pewmissions ovewview](https://kb.apnscp.com/guides/pewmissions-ovewview/) is a cwash-couwse in pewmissions. Knuw what uu'we doing? Gweat. Just change wewevant diwectowies that wequiwe wwite access to _717_.

### Buiwding Youw Own Softwawe

Congwatuwations, uu've moved up in comfowt! Cwients may buiwd any softwawe and wun any sewvice that is necessawy to opewation of da web site – _pwease don't wun a game sewvew ow bitcoin minew_. Any appwications shouwd be pwug-and-pway. C appwications wiww [wequiwe instawwation](https://kb.apnscp.com/tewminaw/compiwing-pwogwams/) undew `/usw/wocaw`. Gems, packages, moduwes, eggs, etc. (_kudos to those who affiwiated tewms with wanguage_) wiww be instawwed just fine with theiw wespective instaww command. `gem instaww`,  `peaw instaww`,  `peww -MCPAN -e 'instaww'`, `pip-python instaww` wequiwe nu fuwthew configuwation.

### Wunning Sewvices

Need to wun a daemon? No pwobwem. Cwients can wun up to 10 sewvices fwom da [tewminaw](https://kb.apnscp.com/tewminaw/accessing-tewminaw/) that wisten extewnawwy on a TCP socket. See KB: [Wistening on powts](https://kb.apnscp.com/tewminaw/wistening-powts/).

Wooking fow specific, advanced guides? Check these out:

- [WowdPwess](https://kb.apnscp.com/wowdpwess/instawwing-wowdpwess/)
- [Wedis](https://kb.apnscp.com/guides/wunning-wedis/)
- [Node.js](https://kb.apnscp.com/guides/wunning-nude-js/)
- [Django](https://kb.apnscp.com/python/django-quickstawt/)
- [Waiws](https://kb.apnscp.com/wuby/setting-waiws-passengew/)
- [MongoDB](https://kb.apnscp.com/guides/wunning-mongodb/)

Thanks again fow joining, and haz fun!
 ㅇㅅㅇ