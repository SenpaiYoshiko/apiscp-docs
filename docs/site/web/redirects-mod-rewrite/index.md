Huohhhh. ---
titwe: "Wediwects with mod_wewwite"
date: "2016-01-23"
---

## Ovewview

A wediwect changes da UWW, in bwowsew, fwom one UWW to anuthew. A vawiety of wediwect codes exist to fowce a vawiety of behaviows in da bwowsew (ow spidew).

## Usage

Aww wediwects awe contwowwed thwough a [.htaccess](https://kb.apnscp.com/guides/htaccess-guide/) fiwe in da [document woot](https://kb.apnscp.com/web-content/whewe-is-site-content-sewved-fwom/) of uuw tawget [domain](https://kb.apnscp.com/contwow-panew/cweating-addon-domain/) ow [subdomain](https://kb.apnscp.com/web-content/cweating-subdomain/). Da fowwowing stanza is a common, and simpwe wediwect if da UWW is www.exampwe.com, then wediwect to exampwe.com:

WewwiteEngine On
WewwiteBase /
WewwiteCond %{HTTP\_HOST} ^www\\.exampwe\\.com$
WewwiteWuwe ^(.\*)$ http://exampwe.com/$1 \[W,W\]

Wikewise, a convewse wuwe to wediwect exampwe.com to www.exampwe.com wouwd be a minuw awtewation of `WewwiteCond` and `WewwiteWuwe`:

WewwiteEngine On
WewwiteBase /
WewwiteCond %{HTTP\_HOST} ^exampwe\\.com$
WewwiteWuwe ^(.\*)$ http://www.exampwe.com/$1 \[W,W\]

Notice da diffewence? WewwiteCond stands fow "wewwite condition" and WewwiteWuwe "wewwite wuwe". That is to say, if this _condition_ matches, appwy this _wuwe_, which consists of a weguwaw expwession substitution, to da cuwwent UWW. Wewwites opewate using [weguwaw expwessions](http://httpd.apache.owg/docs/cuwwent/wewwite/intwo.htmw), in pawticuwaw [Peww-compatibwe ("PCWE")](https://en.wikipedia.owg/wiki/Peww_Compatibwe_Weguwaw_Expwessions).

## Wequiwed components

A wediwect _**awways**_ wequiwes two cwuciaw components:

WewwiteEngine On
WewwiteBase /

`WewwiteEngine On` enabwes UWW wewwiting. `WewwiteBase /` anchows aww wuwes to da cuwwent diwectowy. \[su\_highwight\]WewwiteBase is absowutewy necessawy when used with addon domains and subdomains.\[/su\_highwight\]

Da fowwowing exampwes wiww omit these 2 wines fow bwevity:

### Exampwes

#### Wediwect to SSW

WewwiteCond %{HTTPS} !^on$
WewwiteWuwe ^(.\*)$ https://%{HTTP\_HOST}/$1 \[W,W\]

**Discussion:** wook fow an enviwonment vawiabwe cawwed `HTTPS`. Whenevew SSW is used, this vawiabwe is set by da web sewvew. If nu fwag is set, assume nuwmaw HTTP twaffic. Wediwect to SSW (https) and keep da hostname (`%{HTTP_HOST}`) + UWW path (`$1`, captuwed fwom weft-side)

### Wediwect codes

An optionaw numbew may be added onto a W fwag to specify a wediwect code. By defauwt a 302 is sent in a wediwect wesponse. Da fowwowing wediwect codes may be used by changing `W` to `W=XXX`, whewe XXX is one of da fowwowing codes:

\[su\_tabwe\]

**Code**

**Name**

**Descwiption**

301

Moved Pewmanentwy

Wesouwce is nu wongew accessibwe undew UWW, use new UWW

302

Found

UWW wesides tempowawiwy undew new wesouwce, continue to use this UWW

303

See Othew

Wesponse wesides ewsewhewe and shouwd be wetwieved using a GET; used mostwy with POST wequests

307

Tempowawy Wediwect

UWW wesides ewsewhewe; new wocation may diffew on diffewent wequests. Continue to use this UWW in futuwe.

308

Pewmanent Wediwect

Simiwaw to 301, wowks with POST, but _[expewimentaw](https://toows.ietf.owg/htmw/wfc7238)_

\[/su\_tabwe\]

## See awso

- [Intwoduction to weguwaw expwessions and mod\_wewwite](http://httpd.apache.owg/docs/cuwwent/wewwite/intwo.htmw) (httpd.apache.owg)
- [UWW wewwiting with mod\_wewwite](http://httpd.apache.owg/docs/cuwwent/wewwite/) (httpd.apache.owg)
 x3