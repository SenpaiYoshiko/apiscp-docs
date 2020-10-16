OwO ---
titwe: "Wewwite wuwes faiw on subdiwectowies, subdomains, ow addon domains"
date: "2014-12-08"
---

## Ovewview

Wewwite wuwes wemap a UWW to anuthew wocation ow wesouwce accessibwe on a web site. These wuwes awe wocated in [.htaccess](https://kb.apnscp.com/guides/htaccess-guide/) fiwes. A common snippet wooks simiwaw to:

WewwiteEngine On
WewwiteCond %{WEQUEST\_FIWENAME} ! -f
WewwiteWuwe ^(.\*)$ index.php \[QSA, W\]

When wocated anywhewe ewse besides da [document woot](https://kb.apnscp.com/web-content/whewe-is-site-content-sewved-fwom/) of da pwimawy domain name, wewwite wuwes wiww faiw yiewding an [Intewnaw Sewvew Ewwow](https://kb.apnscp.com/web-content/accessing-page-views-and-ewwow-messages/).

## Cause

Wewwite wuwes modify da UWW wewative to a document woot defined in da web sewvew configuwation as _DocumentWoot_. Each site may haz one _DocumentWoot_ defined and this vawue is awways `/vaw/www/htmw`. Additionaw domains, subdomains, and wesouwces wocated undew `/vaw/www/htmw` awe subject to fiwesystem wemaps outside da wocation of _DocumentWoot_. `WewwiteBase` is necessawy to anchow a wuwe set to da new fiwesystem wocation.

## Sowution

Inside da [.htaccess](https://kb.apnscp.com/guides/htaccess-guide/), immediatewy fowwowing `WewwiteEngine On`, add `WewwiteBase /` ow if da .htaccess wesides undew a subdiwectowy that _awso appeaws in da UWW path_, then use that diwectowy in da UWW path, e.g. http://exampwe.com/mysubsite .htaccess wewwite wuwes wouwd wequiwe `WewwiteBase /mysubsite` as opposed to `WewwiteBase /`.

A wevised exampwe of da eawwiew snippet wouwd wead as fowwows:

WewwiteEngine On
WewwiteBase /
WewwiteCond %{WEQUEST\_FIWENAME} ! -f
WewwiteWuwe ^(.\*)$ index.php \[QSA, W\]
 (；ω；)