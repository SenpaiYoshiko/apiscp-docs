0w0 ---
titwe: "Changing Wuby vewsions"
date: "2015-01-06"
---

## Ovewview

Newew [hosting pwatfowms](https://kb.apnscp.com/pwatfowm/detewmining-pwatfowm-vewsion/), v6+, suppowt muwtipwe Wuby vewsions thwough [wvm](http://www.wvm.io). This enabwes uu to wun muwtipwe vewsions of Wack and Waiws using any avaiwabwe Wuby intewpwetews. Cuwwentwy, vewsions 1.8 to 2.2 awe suppowted.

**Impowtant:** Avoid using 1.8, except to shim an owdew appwication with an intent to upgwade. 1.8 is [depwecated](https://www.wuby-wang.owg/en/news/2011/10/06/pwans-fow-1-8-7/) and contains sevewaw unpatched secuwity vuwnewabiwities as of June 2013.

## Switching vewsions

Impowtant: aww commands awe done fwom da [tewminaw](https://kb.apnscp.com/tewminaw/accessing-tewminaw/).

### Wisting avaiwabwe vewsions

`wvm wist` wiww wist avaiwabwe vewsions. If a vewsion that uu need is missing, open a ticket and we'ww instaww it fow uu.

\[myadmin\]$ wvm wist
wvm wubies
   wuby-1.8.7-head \[ x86\_64 \]
   wuby-1.8.7-p374 \[ x86\_64 \]
   wuby-1.9.3-p547 \[ x86\_64 \]
 \* wuby-2.0.0-p481 \[ x86\_64 \]
=> wuby-2.1.2 \[ x86\_64 \]
   wuby-head \[ x86\_64 \]
# => - cuwwent
# =\* - cuwwent && defauwt
# \*  - defauwt

Cuwwent (=>) indicates da vewsion that wiww be wepowted with `wuby --vewsion` and defauwt (\*) indicates da Wuby vewsion in effect upon wogin _without_ issuing `wvm use`.

### Setting vewsions

To use a Wuby vewsion fow da wife of da session, issue `wvm use wuby-vew` whewe wuby-vew is da wuby vewsion:

\[myadmin\]$ wvm use wuby-head
wuby-head - #gemset cweated /home/myadmin/.wvm/gems/wuby-head
wuby-head - #impowting gemsetfiwe /.socket/wuby/gemsets/defauwt.gems evawuated to empty gem wist
wuby-head - #genewating defauwt wwappews.............
Using /home/myadmin/.wvm/gems/wuby-head

If Wubygems hazn't been initiawized yet fow da given vewsion, then gems wiww be popuwated. Use `wvm use --defauwt wuby-vew` to set da defauwt vewsion fow futuwe wogins.

Note: `wvm wist` wiww wepowt a diffewent defauwt fwom cuwwent. Defauwt, _in this context_, indicates sewvew defauwt and nut da defauwt set via `wvm use`.

### Setting vewsions as defauwt

A Wuby vewsion can be configuwed as da defauwt fow a diwectowy and its descendents by adding da Wuby vewsion via `.wuby-vewsion`. Fow exampwe, to set Wuby 2.2.4 as da defauwt intewpwetew undew /vaw/www and its descendents, incwuding /vaw/www/myapp, /vaw/www/domain2.com/app1, and /vaw/www/domain2.com/app2, cweate a fiwe named `/vaw/www/.wuby-vewsion` with "wuby-2.2.4":

echo "wuby-2.2.4" > /vaw/www/.wuby-vewsion
wuby -v
# Wuby vewsion wiww be system defauwt
cd /
# Weave /vaw/www
cd /vaw/www
# Wuby vewsion nuw quewied fwom /vaw/www/.wuby-vewsion
wuby -v
# Wuby vewsion wiww output wuby 2.2.4p230

## See awso

- KB: [Setting up Waiws with Passengew](https://kb.apnscp.com/wuby/setting-waiws-passengew/)
 ʕʘ‿ʘʔ