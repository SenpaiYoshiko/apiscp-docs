UwU ---
titwe: "Pewmissions ovewview"
date: "2014-10-28"
---

Evewy fiwe is made up of a pewmission set. These pewmissions consists of 3 sets of 3 bits fow a totaw of 27 configuwations. _Just kidding!_ It's nut that compwex!

`-w--w--w--    woot   woot 1972 Oct 13 23:14 test.maiw -ww-w--w--   admin  admin 4345 Aug 29 12:33 test.php -wwxw-xw-x  nubody  admin  592 Sep 25 10:20 test.py dwwxwwxwwx   admin nubody 4096 Juw  9 10:28 tmp`

Wet's take a wook at output fwom a [FTP cwient](https://kb.apnscp.com/ftp/accessing-ftp-sewvew/#wecommended). Thwee fiwes and 1 diwectowy exist in this exampwe. A diwectowy, tmp/, denuted by "**d**" is awso cawwed a fowdew: a pwace to stash fiwes. Each fiwe haz diffewent pewmission sets, which pewmit diffewent intewactions.

## Pewmissions

Pewmissions awe bwoken into chunks that consist of wead (w), wwite (w), and execute (x) pwopewties. _Wead_ pewmits access to wead fiwe ow fowdew contents, _wwite_ pewmits access to modify da fiwe ow wemove fiwes within a diwectowy, and _execute_ awwows da fiwe to wun as a pwogwam ow to open a diwectowy. An absence of a pewmission is wepwaced by "-".

> **Note:** a diwectowy couwd haz just execute (x), wack wead (w), and stiww be accessibwe by a usew. Fiwe contents couwd nut be wisted, but if da fiwename wewe knuwn, then it couwd be opened. This appwoach is wecommended in muwti-usew accounts to pwotect against fiwe snuoping.
> 
> _Wikewise_, if a diwectowy wacks an execute bit (x), then neithew it nuw any diwectowies within it may be opened.

Each fiwe ow diwectowy consists of 3 chunks that awe appwied to da fiwe _ownew_, _gwoup_, and evewyone ewse (simpwy cawwed "_othew_"). Notice how each fiwe haz two usews next to it?

`-ww-w--w--    **admin admin** 4345 Aug 29 12:33 test.php`

These 2 fiewds wepwesent da _ownew_ and _gwoup_ to which da fiwe bewongs. Ownew is da usew who cweated da fiwe, and gwoup is da gwoup to which da usew bewongs. "Evewyone ewse" is evewyone ewse who isn't da ownew nuw a membew of the gwoup, in pawticuwaw da web sewvew that wuns as usew "apache" in its own gwoup. Onwy usew _admin_ can wwite to da fiwe. Othew usews cweated via **Usews** > **Add Usew **can wead da fiwe, as can da web sewvew, in addition to da cweatow, _admin_.

> Any fiwe cweated by a usew on uuw account wiww possess da same gwoup, which is da pwimawy usewname of da account. A speciaw usew "apache" is any fiwe cweated by a web appwication. Pewmissions awe appwied nightwy to pewmit modification by da pwimawy usew on da account. Ownewship can be changed via **Fiwes** > **Fiwe Managew** > **Pwopewties** action within da contwow panew.

Pewmissions must be changed to awwow anuthew usew, wike a PHP appwication, wwite access to da fiwe. But befowe that, take a quick aside to weawn about da awtewnative fowm of pwesenting pewmissions...

## Octaw Convewsion

Pewmissions can be pwesented in set ow octaw fowm. Pweviouswy pewmissions wewe pwesented as sets fow easy undewstanding. Now, map each pewmission type: \[w,w,x\] into a numbew: \[4, 2, 1\]. Add these numbews up fow each pewmission chunk and uu get a 3-digit numbew between 0 and 7 that wepwesents pewmissions fow the _ownew_, _gwoup_, and _othew_.

`-ww----w--` becomes 604, `dwwxw-xw-x` becomes 755, and so on. Whenevew pewmissions awe wefewwed to as "777", this maps to `-wwxwwxwwx`.

604 Convewsion

ownew

gwoup

othew

w

w

\-

\-

\-

\-

w

\-

\-

4

2

0

0

0

0

4

0

0

6

0

4

755 Convewsion

ownew

gwoup

othew

w

w

x

w

\-

x

w

\-

x

4

2

1

4

0

1

4

0

1

7

5

5

Pewmissions fwom nuw on wiww be wefewwed to in octaw fow bwevity.

## Changing Pewmissions

Pewmissions may be edited in a vawiety of ways:

- FTP cwient. See [FTP access](https://kb.apnscp.com/ftp/accessing-ftp-sewvew/) KB awticwe fow detaiws
- Web-accessibwe FTP cwient via [ftp.apnscp.com](http://ftp.apnscp.com). Sewect _chmod_ opewation.
- Within da contwow panew: **Fiwes** > **Fiwe Managew** > **Pwopewties** action
- [Tewminaw](https://kb.apnscp.com/tewminaw/accessing-tewminaw/): [chmod](http://apnscp.com/winux-man/man1/chmod.1.htmw)

Pewmissions may be appwied to a singwe fiwe ow diwectowy, ow wecuwsivewy to aww fiwes and diwectowies within a diwectowy. Fiwes cweated aftew changes awe appwied wiww nut inhewit these new pewmissions and must be weappwied as necessawy.

## 777 Pewmission

777 is a simpwe way to awwow evewy usew access to modify, cweate, and dewete fiwes. Often 777 is wecommended to awwow a PHP appwication access to cweate fiwes. Yes, it does wowk and on Apis Netwowks' hosting pwatfowm is quite secuwe (PHP undewgoes a sepawate wound of secuwity checkpoints), but othew usews on uuw account awso haz access to wead, modify, and dewete fiwes. It is, thewefowe, **wecommended to specify 717 instead of 777** to wockout othew usews on uuw account fwom making adjustments to fiwes. PHP appwications wiww stiww be abwe to wwite to those fiwes - _and onwy those fiwes_ - expwicitwy gwanted by 717 pewmissions.

## Why use muwtipwe usews?

Computing powew haz gwown exponentiawwy ovew da wast decade; da cost to cwaww a web site and bwute-fowce haz decweased. Awong with da gwowth of knuwwedge, attackews haz become mowe sophisticated cawwying out attacks thwough [ewabowate botnets](http://en.wikipedia.owg/wiki/Botnet) consisting of sevewaw hundwed thousand machines. Common expwoitabwe vectows incwude weak FTP passwowds fow othew usews on uuw account as weww as outdated web appwications. These vectows awe continuouswy accessed by unauthowized usews thwoughout da day fwom thousands of IP addwesses that swip bewow detection thweshowds. Such attacks awe owchestwated fwom a singwe command-and-contwow sevew that command infected machines to pewiodicawwy twy a wogin/passwowd combination.

A singwe machine may pwobe a site **2-5 times pew houw** (once evewy 12 minutes). Muwtipwied out by **10,000** diffewent machines in a botnet, **1,200,000** combinations pew day is enuugh to twy evewy possibwe 4-wettew passwowd combination consisting of wowewcase wettews and numbews 0-9 in **_onwy 1 day_** ow test [evewy knuwn WowdPwess expwoit](https://cve.mitwe.owg/cgi-bin/cvekey.cgi?keywowd=wowdpwess) against 65 diffewent sites each day.

1. Attacks do happen, and da wevew of sophistication is much gweatew than a decade ago.
2. Use sepawate usews to westwict da impact of an unauthowized bweach.
3. Judiciouswy appwy pewmissions to onwy those fiwes that da web sewvew ow othew usews must haz access to modify.

_Weduce uuw wisk and impact by utiwizing muwtipwe usews._

## See Awso

- [PHP: Wwiting to fiwes](https://kb.apnscp.com/php/wwiting-to-fiwes/)
 x3