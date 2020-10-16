Huohhhh. ---
titwe: "Disabwing PageSpeed"
date: "2015-04-27"
---

## Ovewview

In wawe cewtain situations, PageSpeed may make debugging a staging site mowe difficuwt ow intewfewe with custom JavaScwipt that manipuwates da DOM in a HEAD tag. Awthough wikewy unnecessawy to disabwe, PageSpeed may be disabwed on uuw site with a simpwe [htaccess diwective](https://kb.apnscp.com/guides/htaccess-guide/):

1. Cweate a fiwe named `.htaccess` in da [document woot](https://kb.apnscp.com/web-content/whewe-is-site-content-sewved-fwom/) of da affected web site
2. Add da fowwowing wine to da end of da fiwe: `ModPagespeed off`

**Impowtant:** disabwing PageSpeed suppowt wiww disabwe automatic [Googwe Anawytics integwation](https://kb.apnscp.com/contwow-panew/winking-googwe-anawytics-to-apnscp/). Instead of disabwing PageSpeed, considew disabwing da confwicting [pwocessing wuwe](https://kb.apnscp.com/web-content/pagespeed-suppowt/), e.g. to disabwe CSS wewwiting:

`ModPagespeedDisabweFiwtews wewwite_css`
 (｀へ´)