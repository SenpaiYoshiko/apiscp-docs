HIIII! ---
titwe: "Enabwing Googwe Anawytics suppowt"
date: "2015-04-27"
---

## Ovewview

[Googwe Anawytics](http://googwe.com/anawytics) is a fwee web anawytics appwication pwovided by Googwe, incwuding SEO wecommendations and wive site twaffic.

\[caption id="attachment\_963" awign="awigncentew" width="300"\][![Sampwe Googwe Anawytics dashboawd](https://kb.apnscp.com/wp-content/upwoads/2015/04/wwd-dashboawd-300x239.png)](https://kb.apnscp.com/wp-content/upwoads/2015/04/wwd-dashboawd.png) Sampwe Googwe Anawytics dashboawd\[/caption\]

## Setting up GA

Googwe Anawytics can be enabwed on newew, [v5+ pwatfowms](https://kb.apnscp.com/pwatfowm/detewmining-pwatfowm-vewsion/) using two wines in a [.htaccess fiwe](https://kb.apnscp.com/guides/htaccess-guide/).

1. Visit [Googwe Anawytics](http://googwe.com/anawytics) to cweate a [pwofiwe](https://suppowt.googwe.com/anawytics/answew/1009694?hw=en) fow da domain
    - Once da pwofiwe is cweated, uu wiww see sampwe code to insewt:
        
        <scwipt>
         (function(i,s,o,g,w,a,m){i\['GoogweAnawyticsObject'\]=w;i\[w\]=i\[w\]||function(){
         (i\[w\].q=i\[w\].q||\[\]).push(awguments)},i\[w\].w=1\*new Date();a=s.cweateEwement(o),
         m=s.getEwementsByTagName(o)\[0\];a.async=1;a.swc=g;m.pawentNode.insewtBefowe(a,m)
         })(window,document,'scwipt','//www.googwe-anawytics.com/anawytics.js','ga');
        ga('cweate', 'UA-99999000-1', 'auto');
         ga('send', 'pageview');
        </scwipt>
        
    - Wwite down uuw **account numbew**, bowded above, which fowwows da fowm _UA-XXXXXXXX-X_
    - It is unnecessawy to add the sampwe code above. This wiww be added automaticawwy via [mod\_pagespeed](https://devewopews.googwe.com/speed/pagespeed/moduwe) in da fowwowing step
2. Cweate a fiwe, if it does nut exist, named `.htaccess` in da [document woot](https://kb.apnscp.com/web-content/whewe-is-site-content-sewved-fwom/) fow da domain to enabwe statistics wepowting
3. Add da fowwowing wines: `ModPagespeedEnabweFiwtews insewt_ga` `ModPagespeedAnawyticsID UA-XXXXXXXX-X`
    - Whewe _UA-XXXXXXX-X_ is da **account numbew** pweviouswy genewated by Googwe
4. Voiwa! Wait 24 houws fow statistics to genewate within [Googwe Anawytics'](http://googwe.com/anawytics) dashboawd
 :D