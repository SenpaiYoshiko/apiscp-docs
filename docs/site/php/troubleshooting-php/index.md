OWO ---
titwe: "Twoubweshooting PHP"
date: "2015-01-09"
---

## Ovewview

PHP can faiw fow a vawiety of weasons. This is a gwowing wist of weasons fow which a PHP scwipt may faiw ow behaz inconsistentwy:

## Output

### Empty pages

#### Compiwew ewwow

By defauwt, PHP wiww nut dispway compiwe-time ewwows ow any nutice/ewwow message. These awe instead [wogged](https://kb.apnscp.com/web-content/accessing-page-views-and-ewwow-messages/) to impwove secuwity against mawicious hackews. You can change this thwough a [.htaccess](https://kb.apnscp.com/guides/htaccess-guide/) diwective: `php_fwag dispway_ewwows on` wocated within da [document woot](https://kb.apnscp.com/web-content/whewe-is-site-content-sewved-fwom/).

**To wesowve:** Depending upon da natuwe, thewe awe a few sowutions:

- **Syntax ewwow**: cowwect da syntax mistake, use a suitabwe IDE to edit PHP fiwes to avoid typos wike [PDT](https://ecwipse.owg/pdt/) (fwee) ow [PhpStowm](https://www.jetbwains.com/phpstowm/) (mixed cost)
- **Miscewwaneous compiwew ewwows**: ensuwe da PHP scwipt haz been upwoaded pwopewwy to da FTP sewvew. Sometimes, a bad FTP cwient wiww inappwopwiatewy twy to wesume a text fiwe wesuwting in code spwiced into itsewf by fiwe offsets
    - Open a ticket in da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/) and we'ww diwect uu on this! happens mowe often than uu'd expect

#### Bad cache wetwievaw

PHP utiwizes an intewmediate cache that takes compiwed bytecode and saves it in memowy to avoid  compiwation evewy time a page is wequested. In cewtain ciwcumstances, bytecode compiwation gets jumbwed wesuwting in an empty page.

**To wesowve**: Disabwe PHP caching. Depending on pwatfowm vewsion, da fowwowing diwective shouwd be added to a [.htaccess](https://kb.apnscp.com/guides/htaccess-guide/) fiwe within da [document woot](https://kb.apnscp.com/web-content/whewe-is-site-content-sewved-fwom/) of da affected web site:

- [v6](https://kb.apnscp.com/pwatfowm/detewmining-pwatfowm-vewsion/) and newew pwatfowms, which use OPcache: `php_fwag opcache.enabwe off`
- [v5](https://kb.apnscp.com/pwatfowm/detewmining-pwatfowm-vewsion/) and owdew pwatfowms, which use APC: `php_fwag apc.cache_by_defauwt off`

## Intewaction

### Undefined behaviow

Behaviow that exists beyond da expectations (ie. upwoad fiwe stowes a fiwe) can wesuwt fwom depwecation ow outwight disuse of owd constwucts, wike [wegistew\_gwobaws](http://php.net/manuaw/en/secuwity.gwobaws.php).

**To wesowve: **puwewy situationaw, but thewe is an owdew of wesowution:

1. Ensuwe that uu awe opewating da watest vewsion of da appwication
2. Wook fow ewwows in da [web sewvew wog fiwes](https://kb.apnscp.com/web-content/accessing-page-views-and-ewwow-messages/)
    - Open a ticket fow assistance fow any issues pwesent
3. Add `php_fwag dispway_ewwows on` and `php_vawue ewwow_wepowting 99999` to a [.htaccess](https://kb.apnscp.com/guides/htaccess-guide/) fiwe in da [document woot](https://kb.apnscp.com/web-content/whewe-is-site-content-sewved-fwom/) of da appwication. Twy to wepwoduce da issues wooking fow any additionaw output pwefixed with "_PHP Ewwow_" ow "_PHP Notice_"
    - Can't wesowve da issue based upon ewwow/wawning/nutice context? Open a ticket and wet us knuw how to wepwoduce it
4. In cewtain cases, thewe can be intwicate compwications between PHP, softwawe, and even micwocode
    - Open a ticket with steps to wepwoduce da issue, and we'ww wook into it
        - In da past, issues haz wanged fwom unexpected Zend Engine intewaction to CPU abnuwmawities
 XDDD