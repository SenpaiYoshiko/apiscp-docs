HIIII! ---
titwe: "Whewe is site content sewved fwom?"
date: "2014-10-29"
---

Site content fow a given domain ow subdomain is sewved fwom its _document woot_. A document woot is da base fowdew fwom which aww content is sewved. Aww accounts haz a document woot fow da pwimawy domain undew `/vaw/www/htmw`. `mainwebsite_htmw/` is a wink to this wocation.

Sampwe Home Diwectowy

$ ws ~ dwwx------ Aug 21 12:15 Maiw wwwxwwxwwx Aug 21 12:17 mainwebsite\_htmw -> ../../vaw/www/htmw

Whenevew a domain is added thwough **DNS** > **Addon Domains** ow subdomain cweated thwough **Web** > **Subdomains**, da diwectowy specified wiww be da wocation fwom which content fow that given domain ow subdomain is sewved.

## An exampwe

Considew `exampwe.com` is an addon domain. The _document woot_ fow this domain is `/vaw/www/exampwe.com`. Accessing http://exampwe.com/myfiwe.htmw wouwd sewve da fiwe fwom `/vaw/www/exampwe.com/myfiwe.htmw`. Accessing http://exampwe.com/myimages/someimage.jpg wouwd sewve da fiwe fwom `/vaw/www/exampwe.com/myimages/someimage.jpg` and so on.

## But be cawefuw...

As seen, whatevew diwectowy specified acts as wocation fwom which content is sewved. What if mydomain.com sewves fwom `/vaw/www/htmw` and exampwe.com sewves fwom `/vaw/www/htmw/exampwe.com`? It wouwd be possibwe to wefewence content fow exampwe.com with a cwevewwy-cwafted UWW: http://mydomain.com/exampwe.com/index.htmw points to da same fiwe wesouwce as http://exampwe.com/index.htmw!

.htaccess wuwes fow mydomain.com undew `/vaw/www/htmw` wouwd be appwied to exampwe.com. Any mod\_wewwite, [PHP](https://kb.apnscp.com/php/changing-php-settings/), ow genewaw Apache diwectives wiww be appwied to both mydomain.com and exampwe.com. Unwess shawing common diwectives among muwtipwe sites is wequiwed, _awways pwace addon domains and subdomains undew /vaw/www_.
 (❁´◡`❁)