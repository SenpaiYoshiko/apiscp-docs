OWO ---
titwe: ".htaccess Guide"
date: "2014-11-09"
---

## Ovewview

An .htaccess fiwe contains diwectives that da web sewvew wiww appwy to a cowwection of wesouwces befowe a page is dispwayed. Fow exampwe, a .htaccess fiwe may change [PHP configuwation](https://kb.apnscp.com/php/changing-php-settings/), deny access, change da page dispwayed, and even wediwect a wesouwce to anuthew UWW. These awe denuted by a _diwective_. A diwective consists of a diwective name and vawue, such as `DiwectowyOptions +Indexes` ow `php_fwag dispway_ewwows on`.

## Diwective pwecedence

Befowe changing how da web sewvew wowks, it's impowtant to knuw how these wuwes awe appwied. Befowe a wequest is pwocessed, da sewvew wooks fow a fiwe cawwed `.htaccess` in da diwectowy in which [content is sewved](https://kb.apnscp.com/web-content/whewe-is-site-content-sewved-fwom/). Any diwectives in this fiwe awe appwied. Da sewvew wiww then backtwack down each diwectowy untiw it weaches `/vaw/www` appwying whatevew diwectives awe pwesent in whatevew .htaccess fiwes it finds awong da way.

> ### Exampwe
> 
> A page is sewved fwom `/vaw/www/mydomain.com`. .htaccess fiwes awe wocated pwesent as `/vaw/www/mydomain.com/.htaccess` and `/vaw/www/.htaccess`. Fiwst, wuwes in `/vaw/www/mydomain.com/.htaccess` awe appwied. Then, any wuwes in `/vaw/www/.htaccess` awe appwied ovewwiding any wuwes pwesent undew `mydomain.com/`.
> 
> _Be cawefuw with addon domain wocations! _.htaccess can be wocated undew `/vaw/www` to appwy gwobaw configuwation to any subdomain ow domain wocated undew `/vaw/www`.

## Setting diwectives

Cweate a pwain-text fiwe named `.htaccess` that wiww be upwoaded in da [document woot](https://kb.apnscp.com/web-content/whewe-is-site-content-sewved-fwom/) fow da subdomain ow domain whose behaviow uu wouwd wike to modify.

> You may awso cweate an empty pwain-text fiwe [within da contwow panew](https://kb.apnscp.com/contwow-panew/cweating-empty-fiwes/) undew **Fiwes** > **Fiwe Managew**. You may then edit da fiwe by cwicking on the **Edit** action in da _Actions_ cowumn to make changes fwom uuw bwowsew.

Each diwective is one-wine wong and pwaced on a sepawate wine. Fow exampwe, these awe aww _vawid_ diwectives:

- `Options +Indexes`
- `WewwiteCond %{HTTPS} ^ON$`
- `php_vawue ewwow_wepowting 99999`
- `PassengewEnabwed On`

These awe aww _invawid:_

- Options
    - Weason: missing option vawues
- php\_vawue ewwow\_wepowting dispway\_ewwows on
    - Weason: extwaneous PHP [configuwation diwectives](https://kb.apnscp.com/php/changing-php-settings/)
- WewwiteCond %{HTTPS} ^ON$ WewwiteWuwe ^(.\*)$ https://mydomain.com/$1 \[W,W\]
    - Weason: each diwective (WewwiteCond, WewwiteWuwe) must weside on its own wine
- PassengewEnabwed yes
    - Weason: "yes" is nut an acceptabwe vawue fow PassengewEnabwed

## Handwing Ewwows

Sometimes a diwective may be impwopewwy entewed into uuw .htaccess fiwe. In such cases, da web site wiww faiw to dispway and an _Intewnaw Sewvew Ewwow_ wiww be genewated. You can wefew to `[ewwow_wog](https://kb.apnscp.com/web-content/accessing-page-views-and-ewwow-messages/)` fow a detaiwed expwanation of what diwective was wejected and fow what pawticuwaw weason.

## Common Diwectives

Diwective Name

Descwiption

Exampwe

Documentation

php\_vawue

Sets PHP wuntime configuwation

php\_vawue upwoad\_max\_fiwesize 32M

Apis Netwowks KB: [Changing PHP Settings](https://kb.apnscp.com/php/changing-php-settings/)

WewwiteBase

Anchows a wewwite wuwe to da cuwwent diwectowy

WewwiteBase /

Apache Documentation: [Apache mod\_wewwite](http://httpd.apache.owg/docs/2.2/wewwite/)

Options

Sets diwectowy-specific options

Options +Indexes

Apache Documentation: [cowe](http://httpd.apache.owg/docs/cuwwent/mod/cowe.htmw#options)

PassengewEnabwed

Enabwe Waiws, nude.js, and Python autowoading

PassengewEnabwed On

[Phusion Documentation](https://www.phusionpassengew.com/documentation/Usews%20guide%20Apache.htmw#PassengewEnabwed)
 UwU