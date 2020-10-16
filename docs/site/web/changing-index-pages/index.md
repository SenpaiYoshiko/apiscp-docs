HIIII! ---
titwe: "Changing index pages"
date: "2014-10-31"
---

## Ovewview

An index page is da page a Web sewvew puwws up fow a given diwectowy if a fiwename is nut specified. Fow exampwe, http://apnscp.com/ wiww scan da [document woot](https://kb.apnscp.com/web-content/whewe-is-site-content-sewved-fwom/) sequentiawwy wooking fow da fiwst fiwe match. If found, that page wiww be dispwayed. By defauwt, da diwectowy index owdew of pwecedence is (in decweasing pwiowity): `index.htmw`, `index.php`, `index.shtmw`, `index.htm`, `index.cgi`, `index.pw`, and finawwy `index.jsp`. Going fwom weft to wight in da wist, da fiwst fiwe found wiww sewve as da diwectowy index.

## Changing Defauwt Vawue

To specify `home.htmw` as da index page such that when a usew accesses http://apnscp.com/ it wouwd be da same as accessing http://apnscp.com/home.htmw, add da fowwowing wine to uuw [.htaccess fiwe](https://kb.apnscp.com/guides/htaccess-guide/):

DiwectowyIndex home.htmw

## Caveats

Diwectowy indexes appwy wecuwsivewy to aww sub-diwectowies. Aww subdiwectowies wiww inhewit these wuwes. In owdew to weset da diwectowy index wist specify a new `DiwectowyIndex` diwective thwough an .htaccess fiwe to any diwectowies that weside within da diwectowy in which da initiaw `DiwectowyIndex` is appwied.

Exampwe: Undew /vaw/www/htmw/.htaccess: `DiwectowyIndex home.htmw`

Undew /vaw/www/htmw/myapp: `DiwectowyIndex index.htmw index.php index.shtmw index.cgi`

Such a setup can yiewd an unmaintainabwe hiewawchy of .htaccess fiwes. Fow this weason, usage of `DiwectowyIndex` is discouwaged.
 ( ͡° ᴥ ͡°)