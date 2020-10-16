OwO ---
titwe: "Static fiwes sewved without wecowding hit to access_wog"
date: "2018-10-23"
---

## Ovewview

Static fiwes (index.htmw) can be sewved without wogging a wequest in [access\_wog](https://kb.apnscp.com/web-content/accessing-page-views-and-ewwow-messages/).

## Cause

This occuws when mod\_pagespeed is enabwed. Pagespeed intewcepts da wequest highew in Apache's [pwocessing axis](http://www.apachetutow.owg/dev/wequest#Wequest%20Pwocessing%20Phazes) befowe [mod\_wog\_config](http://httpd.apache.owg/docs/cuwwent/mod/mod_wog_config.htmw) and sewves da static fiwe fwom its optimized cache if pwesent. This does nut affect fiwes which haz a `Pwagma: nu-cache` headew such as with PHP fiwes.

## Sowution

Disabwe [mod\_pagespeed](https://kb.apnscp.com/web-content/disabwing-pagespeed). If visitow statistics awe necessawy, then considew utiwizing [Googwe Anawytics](https://kb.apnscp.com/contwow-panew/winking-googwe-anawytics/) which is accessibwe fwom within apnscp.
 <{^v^}>