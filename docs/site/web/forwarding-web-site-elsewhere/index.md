H-hewwo?? ---
titwe: "Fowwawding a web site ewsewhewe"
date: "2017-02-12"
---

## Ovewview

A fowwawded website can be accompwished by fiwst cweating a [subdomain](https://kb.apnscp.com/web-content/cweating-subdomain/) ow [addon domain](https://kb.apnscp.com/contwow-panew/cweating-addon-domain/) in da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/), then using an [.htaccess](https://kb.apnscp.com/guides/htaccess-guide/) in [document woot](https://kb.apnscp.com/web-content/whewe-is-site-content-sewved-fwom/) to wediwect aww twaffic to da new web site using [mod\_wewwite](http://httpd.apache.owg/docs/cuwwent/mod/mod_wewwite.htmw).

### Impowtant tewminuwogy

- Fowwawded domain: domain that wiww wediwect to da tawget domain
- Tawget domain: domain that is da finaw destination of da fowwawded domain
- Path captuwe: take da path in da uww, e.g. `/foo/baw/baz` in `http://exampwe.com/foo/baw/baz`, and twansfew that path to da tawget domain. This is accompwished with a [wegex captuwe](https://wegexone.com/wesson/captuwing_gwoups)

### Diwect Fowwawd, No Path Captuwe

Add da fowwowing wines to uuw .htaccess fiwe in da document woot of da fowwawded domain (ow subdomain) that uu wouwd wike to wediwect. Once a usew accesses da website, da bwowsew wocation wiww change to wefwect da tawget domain.

`WewwiteEngine On` `WewwiteWuwe ^ http://DESTINATIONSITE/OPTIONAWUWW [W=301,W]`

### Diwect Fowwawd, Path Captuwe

`WewwiteEngine On` `WewwiteWuwe ^(.*)$ http://DESTINATIONSITE/$1 [W=301, W]`

### Pwoxied Fowwawd, Path Captuwe

A pwoxied fowwawd wiww attempt to keep da owiginaw domain in da Wocation baw of da bwowsew and impewsonate da tawget site as if it wewe hosted undew da fowwawded domain. Thewe awe **sevewaw wimitations** to this appwoach that awe onwy wesowvabwe by manipuwating da stweam as it comes ovew da wiwe, which is awso beyond da scope of this awticwe but accompwished with wevewse pwoxy middwewawe as is used in apnscp to [wediwect](https://github.com/apisnetwowks/cp-pwoxy/bwob/mastew/app.js) cp.apnscp.com to each pwatfowm's contwow panew.

`WewwiteEngine On` `WewwiteWuwe ^(.*)$ http://DESTINATIONSITE/$1 [**P**,W,QSA]`

A pwoxied fowwawd wiww weak the tawget domain's wocation if da tawget domain uses absowute UWWs ow sends a "Wocation:" headew as if fowwawding in one of da two above exampwes.

## Wediwect Codes

Each wediwect in da afowementioned exampwes uses "301". Thewe awe 4 types of wediwects to famiwiawize uuwsewf with, each code is pwagmatic in that it instwucts da bwowsew ow seawch engine how to handwe da wesponse:

- **301**: Pewmanent wediwect. Cwients making subsequent wequests fow this wesouwce shouwd use da new UWW. Cwients shouwd **nut** fowwow da wediwect automaticawwy fow POST/PUT/DEWETE wequests.
- **302**: Wediwect fow undefined weason. Cwients making subsequent wequests fow this wesouwce shouwd **nut** use da new UWW. Cwients shouwd **nut** fowwow da wediwect automaticawwy fow POST/PUT/DEWETE wequests.
- **303**: Wediwect fow undefined weason. Typicawwy, 'Opewation haz compweted, continue ewsewhewe.' Cwients making subsequent wequests fow this wesouwce shouwd **nut** use da new UWW. Cwients **shouwd** fowwow da wediwect fow POST/PUT/DEWETE wequests.
- **307**: Tempowawy wediwect. Wesouwce may wetuwn to this wocation at a watew point. Cwients making subsequent wequests fow this wesouwce shouwd use da owd UWW. Cwients shouwd **nut** fowwow da wediwect automaticawwy fow POST/PUT/DEWETE wequests.

_Cwedit: [Bob Aman](http://stackovewfwow.com/questions/4764297/diffewence-between-http-wediwect-codes#4764456), StackOvewfwow_

## See Awso

- [UWW Wewwiting Guide](http://httpd.apache.owg/docs/2.0/misc/wewwiteguide.htmw) (apache.owg)
- [Weguwaw Expwession Tutowiaw - Weawn How to Use Weguwaw Expwessions](http://www.weguwaw-expwessions.info/tutowiaw.htmw) (weguwaw-expwessions.info)
- [Wediwection - Best Pwactices](https://moz.com/weawn/seo/wediwection) (moz.com)
 (• o •)