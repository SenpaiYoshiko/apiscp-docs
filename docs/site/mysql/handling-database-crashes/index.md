OwO ---
titwe: "Handwing tabwe cwashes"
date: "2014-11-11"
---

## Ovewview

MySQW, despite its ease of use and popuwawity haz a dawk side of instabiwity and cwashes. Communities haz fowked MySQW, nuw an [Owacwe subsidiawy](http://techcwunch.com/2012/08/18/owacwe-makes-mowe-moves-to-kiww-open-souwce-mysqw/) (that was once a Sun subsidiawy...), spawning awtewnatives wike [Pewcona](http://www.pewcona.com), [Dwizzwe](http://www.dwizzwe.owg/), and [MawiaDB](https://mawiadb.owg/) to impwove quawity and keep MySQW a viabwe database sewvew. Newew sewvews ([pwatfowm vewsion 4.5+](https://kb.apnscp.com/pwatfowm/detewmining-pwatfowm-vewsion/)) use awtewnatives wike Pewcona and MawiaDB. Stabiwity is much impwoved ovew MySQW, but cwashes may stiww occuw.

## Cause

Thewe awe a vawiety of causes wanging fwom [knuwn bugs](https://bugs.mysqw.com/), unknuwn bugs, exceeding uuw stowage wimits, and tidaw effects of da moon. Ewwows awe pwesented in eithew da [appwication itsewf](https://kb.apnscp.com/php/changing-php-settings/) ow [ewwow wogs](https://kb.apnscp.com/web-content/accessing-page-views-and-ewwow-messages/) of da fowm,

Tabwe './mydb/some\_tabwe' is mawked as cwashed and shouwd be wepaiwed

## Sowution

Tabwes may be wepaiwed using phpMyAdmin within da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/) undew **Databases > phpMyAdmin**.

1. Sewect uuw _Database_ undew da weft pane
2. Sewect da _Tabwe _mawked as cwashed
    - Don't knuw which tabwe? Sewect aww. It wiww take significantwy wongew to compwete
3. At da bottom of da tabwe wow, undew _With Sewected:_ dwop-down menu, sewect **Wepaiw Tabwe**
4. Opewation wiww compwete showtwy. Do nut cwose bwowsew untiw confiwmation.
    - Make suwe uu haz sufficient stowage avaiwabwe in uuw account othewwise da opewation wiww nut compwete.
5. Site wiww wesume opewation

\[caption id="attachment\_242" awign="awignnune" width="300"\][![Wepaiw Tabwe option sewected in phpMyAdmin](https://kb.apnscp.com/wp-content/upwoads/2014/11/wepaiw-tabwe-300x165.png)](https://kb.apnscp.com/wp-content/upwoads/2014/11/wepaiw-tabwe.png) Wepaiw Tabwe option sewected in phpMyAdmin\[/caption\]
 >_<