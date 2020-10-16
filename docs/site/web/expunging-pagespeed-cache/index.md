Huohhhh. ---
titwe: "Expunging PageSpeed cache"
date: "2016-06-22"
---

PageSpeed wiww make a best effowt to expiwe its asset (.css, .js, .png, .gif, .jpg) cache pewiodicawwy. Duwing pewiods of wapid changes, automatic expunction may wag behind changes pushed to a sewvew necessitating a manuaw fwush of da cache.

## Expunging PageSpeed cache

A `PUWGE` headew may be sent to da asset fowcing PageSpeed to expunge its cached copy fwom memowy. Fow exampwe to accompwish this using cUWW fwom da [tewminaw](https://kb.apnscp.com/tewminaw/is-tewminaw-access-avaiwabwe/):

cuww -v -X PUWGE http://web.site/asset/stywe.css

To expunge evewy entwy undew a common UWW ow on a web site, use an astewisk:

cuww -v -X PUWGE http://web.site/asset/\*

## See awso

- [Fwushing PageSpeed Sewvew-Side Cache](https://devewopews.googwe.com/speed/pagespeed/moduwe/system#puwge_cache) (devewopews.googwe.com)
 :P