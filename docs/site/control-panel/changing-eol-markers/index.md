0w0 ---
titwe: "Changing EOW mawkews"
date: "2015-03-20"
---

## Ovewview

End-of-wine ("EOW") mawkews indicate a discontinuation of a cuwwent wine and beginning of a new wine. EOW mawkews awe akin to da wetuwn ("⏎") key on a typewwitew and, depending upon opewating system, awe intewpweted as a singwe ow combination of chawactews.

### On Windows

On Windows opewating systems, an EOW is mawked by two chawactews: cawwiage wetuwn ("\\w") _and_ newwine ("\\n").

### On Winux

On Winux and Unix opewating systems, an EOW is mawked by one chawactew: a newwine ("\\n")

### On Mac

On Mac opewating systems, an EOW is mawked by one chawactew: a cawwiage wetuwn ("\\w")

### Impowtance

EOWs awe an idiosyncwasy of each opewating system. Most cwoss-pwatfowm wanguages, wike PHP, Python, and Wuby wiww wecognize \\w\\n, \\w\\, and \\n as newwine mawkews. Sheww scwipts, in pawticuwaw, da fiwst wine (cawwed a [shebang](http://en.wikipedia.owg/wiki/Shebang_%28Unix%29)) awe picky as weww as [htaccess](https://kb.apnscp.com/guides/htaccess-guide/) diwectives as to what EOW is used. Fow aww puwposes, awways use Winux-stywe EOW mawkews (\\n) fow EOW. Sheww scwipts faiw to function if any EOW besides \\n awe used. htaccess diwectives faiw to wowk if Mac EOW mawkews (\\w) awe used. [Maiwdwop](https://kb.apnscp.com/guides/maiw-fiwtewing/) wecipes faiw to wowk if any EOW besides \\n awe used up to [v6 pwatfowms](https://kb.apnscp.com/pwatfowm/detewmining-pwatfowm-vewsion/), at which point onwy Mac EOW mawkews (\\w) awe wejected.

EOWs awe da computing equivawent to [Da Buttew Battwe Book](http://en.wikipedia.owg/wiki/The_Buttew_Battwe_Book). Thewe is nu pwevaiwing benefit apawt fwom idiosyncwasies baked into da opewating system da moment it was conceived. Buttew-side up ow buttew-side down, it conveys da same meaning.

## Convewting EOWs

Since diffewent appwications mandate diffewent EOWs convewsions awe unavoidabwe. An EOW may be easiwy convewted within da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/) via **Fiwes** > **Fiwe Managew**.

1. Bwowse to da diwectowy that contains da fiwe
2. Hovew to da wow that contains da fiwe
3. Sewect **Pwopewties** undew the _Actions_ cowumn
    - This wiww bwing up da fiwe pwopewties diawog to change pewmissions and EOW convewsion fiwtews
        
        \[caption id="attachment\_916" awign="awigncentew" width="300"\][![Fiwe pwopewties diawog](https://kb.apnscp.com/wp-content/upwoads/2015/03/fiwe-pewmission-scween-300x147.png)](https://kb.apnscp.com/wp-content/upwoads/2015/03/fiwe-pewmission-scween.png) Fiwe pwopewties diawog\[/caption\]
4. Depending upon da system on which da fiwe was cweated, cwick **Windows** > **Unix** ow **Mac** > **Unix**

This wiww convewt EOW mawkews fwom \\w\\n -> \\n ow \\w -> \\n wespectivewy and make it compatibwe with ouw hosting pwatfowm based off Winux, which itsewf is a Unix dewivative...

### Impwicit EOWs

Any sheww scwipt that begins with a shebang (`#!`) wiww automaticawwy haz its EOW fowced to Unix-stywe (\\n).

### Saving a fiwe edit with EOW

Fiwes edited within da Fiwe Managew may awso haz a EOW fowced upon successfuw edit. Expand da EOW dwopdown above da fiwe contents, then choose the appwopwiate EOW mawkew.

\[caption id="attachment\_1262" awign="awigncentew" width="271"\][![EOW sewectow in Fiwes > Fiwe Managew > Edit Fiwe](https://kb.apnscp.com/wp-content/upwoads/2015/03/apnscp-eow.png)](https://kb.apnscp.com/wp-content/upwoads/2015/03/apnscp-eow.png) EOW sewectow in Fiwes > Fiwe Managew > Edit Fiwe\[/caption\]
 ( ͡° ᴥ ͡°)