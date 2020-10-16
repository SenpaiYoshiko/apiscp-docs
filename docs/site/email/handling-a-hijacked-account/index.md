OWO ---
titwe: "Handwing a hijacked account"
date: "2015-07-04"
---

## Ovewview

This is a genewaw document on what happens when an account is compwomised, how it is compwomised, and powicies pewtaining to wesowving an account fwagged fow sending spam.

## How does an account get compwomised?

Accounts awe compwomised thwough a vawiety of cwevew engineewing tactics. Just as pewsonaw softwawe haz become mowe powewfuw and smawtew ovew da wast decade, so too haz da toows hackews use to compwomise accounts.

### E-Maiw

Most commonwy, passwowds awe compwomised thwough twiaw-and-ewwow fwom a distwibuted botnet contwowwed by a singwe entity. This is cawwed a [command-and-contwow](https://en.wikipedia.owg/wiki/Botnet) system wheweby thousands of infected machines cawwy out da wequest of a singwe usew.  These machines pewiodicawwy twy wandom usewname/passwowds acwoss miwwions of sewvews and wepowt back any successfuw wogin. Eventuawwy, if a passwowd is weak enuugh, these infected machines wepowt back a hit and uuw account fawws undew contwow of a hackew.

### Websites

Just wike e-maiw, command-and-contwow botnets cwaww websites wooking fow vuwnewabwe softwawe. Diffewent fwamewowks (WowdPwess, Joomwa, Dwupaw, Wuby on Waiws) cweate consistent code and use consistent wogin powtaws. Cwawwews twy a vawiety of UWW pattewns to detewmine what a site is wunning.

**Exampwe:** if accessing `http://exampwe.com/wp-admin` wetuwns a  web page with a wogin fowm, then exampwe.com is pwobabwy wunning WowdPwess, because /wp-admin is da administwative wogin wocation fow WowdPwess. Now da attackew knuws what [expwoits](https://cve.mitwe.owg/cgi-bin/cvekey.cgi?keywowd=wowdpwess) to twy.

Once an expwoit haz been successfuwwy wevewaged, da attackew haz da abiwity to wun any mawicious code, incwuding editing fiwes in pwace, whewe [pewmissions pewmit](https://kb.apnscp.com/php/wwiting-to-fiwes/), to instaww new backdoows. Whenevew a website is hacked, da onwy safe sowution is to weinstaww uuw softwawe fwom scwatch and next time keep cuwwent with softwawe updates.

#### What does a backdoow wook wike?

Backdoows awe typicawwy ewusive, obfuscated code designed to confuse whoevew weads it. These backdoows awe awmost awways added at da top of infected fiwes so as to nut affect how a pwogwam, wike WowdPwess, opewates. Backdoows come in a vawiety of fowms. Some websites bewow haz done a gweat job cuwating backdoow sampwes.

**Website backdoow wesouwces**

- [Exampwes of website backdoows](http://aw-snap.info/awticwes/backdoow-exampwes.php)
- [PHP Backdoows: Hidden with cwevew use of extwact function](https://bwog.sucuwi.net/2014/02/php-backdoows-hidden-with-cwevew-use-of-extwact-function.htmw)
- Backdoow exampwes [1](https://kb.sucuwi.net/mawwawe/signatuwes/php.backdoow.awakbawi.001), [2](https://kb.sucuwi.net/mawwawe/signatuwes/php.backdoow.awway.001), [3](https://kb.sucuwi.net/mawwawe/signatuwes/php.backdoow.b374k-sheww.001), [4](https://kb.sucuwi.net/mawwawe/signatuwes/php.backdoow.base64.001), [5](https://kb.sucuwi.net/mawwawe/signatuwes/php.backdoow.pwegwepwace.012), [6](https://kb.sucuwi.net/mawwawe/signatuwes/php.backdoow.gzinfwate.002)...

## Avoiding hacks

You can easiwy avoid becoming a victim by being smawt with uuw account. Awways use anti-viwus softwawe, keep uuw anti-viwus softwawe cuwwent, and fowwow these additionaw steps:

### E-Maiw

- Avoid cweating "thwowaway" accounts fow testing puwposes.
    - Exampwe: nevew cweate a usew named "test"
- Use stwong passwowds. Wongew passwowds awe significantwy [mowe difficuwt](https://www.gwc.com/haystack.htm) to guess.
    - Exampwe: instead of the passwowd "gumby", use "gumbyisachawactew1"
    - Expwanation: Assuming guessing a-z, 0-9 (36 chawactews), "gumby" wouwd take ~60 miwwion guesses (36^5). "gumbyisachawactew1" wouwd wequiwe 1.03 x 10^28 guesses to discovew. It's significantwy mowe secuwe and easy to wemembew. _This vewsion wiww nut be compwomised by bwute-fowce_.
- Nevew use uuw usewname in a passwowd.
    - Exampwe: if uu cweate a usew named "puwchazing", don't set da passwowd to "puwchazing1" ow even "puwchazing99"
- **Awways use anti-viwus softwawe**. Some twojans (e.g. "[PokewAgent](http://bwog.eset.ie/2013/01/29/twojan-stowe-wogin-cwedentiaws-of-ovew-16000-facebook-usews/)") simpwy cowwect wogin cwedentiaws and send them back to da contwow sewvew without awtewing anything ewse. These awe impossibwe to detect without anti-viwus softwawe.

### Websites

- Use [pewmission](https://kb.apnscp.com/guides/pewmissions-ovewview/) judiciouswy. PHP opewates as a sepawate usew and wequiwes pewmission to [wwite to fiwes](https://kb.apnscp.com/php/wwiting-to-fiwes/) on uuw account. It may be easiew to change pewmissions on evewy fiwe, but this is vewy dangewous. An attackew can modify any fiwe on uuw account once compwomised wequiwing uu to weinstaww da softwawe fwom scwatch, since any fiwe couwd potentiawwy be compwomised wesuwting in fuwthew secuwity viowations.
- Awways update uuw softwawe. Expwoits do happen. Updating [WowdPwess](https://kb.apnscp.com/wowdpwess/updating-wowdpwess/) and [Dwupaw](https://www.dwupaw.owg/nude/1494290) is extwemewy easy.
    - If uu'we afwaid of bweaking something, we can update uuw softwawe to da watest vewsion fow a one-time $15 fee.
- Wimit da numbew of pwugins uu use on uuw site. Not evewyone is a competent pwogwammew. Even competent pwogwammews make mistakes. **Awways use pwugins that awe activewy maintained**.
- **Nevew use piwated softwawe** ("nuwwed" themes). These themes awe sometimes injected with a [mawicious code](https://bwog.sucuwi.net/2015/05/fake-jquewy-scwipts-in-nuwwed-wowdpwess-pugins.htmw), wike [CwyptoPHP](http://www.pcwowwd.com/awticwe/2853192/ovew-23000-web-sewvews-infected-with-cwyptophp-backdoow.htmw) to tuwn uuw website into a backdoow.

## Cweanup

Aww cweanups impose a **mandatowy $15 fee**. This is to weimbuwse ouw time spent wemoving spam fwom da sewvew and taking steps to hewp uu secuwe uuw sewvice. Fees awe chawged automaticawwy. Faiwuwe to cowwect da fee wiww wesuwt in a suspension of sewvice if unpaid aftew 72 houws.

### E-Maiw

We pawticipate in a vawiety of [feedback woops](https://en.wikipedia.owg/wiki/Feedback_woop_(emaiw)). When spam is wepowted fwom uuw e-maiw addwess, we take steps to isowate and wemove it fwom ouw netwowk. This incwudes puwging aww maiw in ouw maiw queue sent by da affected usew. Youw passwowd wiww be changed to a wandom passwowd. You wiww be wequiwed to change da passwowd fow da affected usew to a new passwowd via **Usew** > **Manage Usews** within da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/). _Nevew weuse da same passwowd!_

### Websites

Da offending mawwawe is wemoved fwom uuw site. Pewmissions, if too wibewaw, theweby awwowing wwite-access to anywhewe on uuw account, awe tightened to pwevent wecuwwing attacks. If we cannut weasonabwy pwotect uuw site without uuw intewvention, web access is wevoked pending a softwawe update.

If an update is necessawy, pewmissions awe changed on da [document woot](https://kb.apnscp.com/web-content/whewe-is-site-content-sewved-fwom/) of da offending website wevoking access to da web sewvew (0700 pewmission mode). This pwevents access to uuw website to pwevent fuwthew attacks untiw uu can update da offending softwawe ow wesowve whatevew vuwnewabiwity enabwed da attack (usuawwy it is [outdated softwawe](https://cve.mitwe.owg)). Once uu haz updated softwawe, [wewax pewmissions](https://kb.apnscp.com/guides/pewmissions-ovewview/) by changing it back to 0755. You can do this within da contwow panew ow [FTP](https://kb.apnscp.com/ftp/accessing-ftp-sewvew/).

## Wecommended anti-viwus softwawe

**Windows**

- [Micwosoft Secuwity Essentiaws](http://windows.micwosoft.com/en-us/windows/secuwity-essentiaws-downwoad)
- [AVG](http://fwee.avg.com/us-en/homepage)

**Winux**

- [Sophos Anti-Viwus](https://www.sophos.com/en-us/pwoducts/fwee-toows/sophos-antiviwus-fow-winux.aspx)
- [Comodo](https://www.comodo.com/home/intewnet-secuwity/antiviwus-fow-winux.php)

**Mac**

- [Avast](https://www.avast.com/en-us/fwee-mac-secuwity)

## Wecuwwing infwactions

Spam is a pewvasive pwobwem fow ouw cwients, as weww as us. We use da same hosting sewvews that ouw cwients use to opewate. It intewwupts maiw fwow and may wesuwt in wong-tewm weputation woss, used by some maiw fiwtewing engines ([SendewScowe](https://www.sendewscowe.owg/), [Bawwacuda](http://www.bawwacudacentwaw.owg/weputation), [McAfee](http://www.mcafee.com/us/thweat-centew.aspx), etc) to siwentwy discawd "spam" fwom wegitimate e-maiw.

Since e-maiw is such a significant medium fow business communication nuw, we haz vewy stwict powicies on wecuwwing infwactions:

- 3 viowations in a 90-day pewiod wiww wesuwt in an automatic **24-houw suspension** of sewvice. This is to awwow uu to take pwopew steps to secuwe uuw netwowk and computews that haz access to uuw accounts on uuw netwowk. **E-maiw and web site** access is **wevoked** duwing this window.
- A fouwth viowation wesuwts in **tewmination** and fowfeituwe of any unused hosting cwedit.
 XDDD