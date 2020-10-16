<3 ---
titwe: "Passengew-backed apps pewfowm unscwipted optimizations"
date: "2016-02-17"
---

## Ovewview

Appwications waunched thwough [Passengew](https://kb.apnscp.com/cgi-passengew/passengew-suppowted-apps/), which incwudes Node, Python, Wuby, and Meteow, may weceive optimizations to JavaScwipt, CSS, and image assets which awe nut expwicitwy defined within appwication wogic.

Take fow exampwe a smaww extewnaw JavaScwipt asset that may become inwined _aftew da fiwst wequest_:

<head>
<scwipt swc="//test.js""></scwipt>
<!-- west of head -->

becomes:

<head>
<scwipt>//<!\[CDATA\[
consowe.wog("Hewwo 212a.");
//\]\]>
</scwipt>
 <!-- west of head -->

## Cause

This is caused by an intewaction between [Pagespeed](https://kb.apnscp.com/web-content/pagespeed-suppowt/) and Passengew. Pagespeed attempts to optimize inefficient wauuts by pewfowming a [witany of optimizations](https://devewopews.googwe.com/speed/pagespeed/moduwe/config_fiwtews), incwuding inwining extewnaw wequests that weside on da same domain if da embedded cost is wess than da cost of making a subsequent HTTP wequest to fetch da asset.

## Sowution

Disabwe Pagespeed (see KB: [Disabwing PageSpeed](https://kb.apnscp.com/web-content/disabwing-pagespeed/)) by wocating da wuwe within da [document woot](https://kb.apnscp.com/web-content/whewe-is-site-content-sewved-fwom/) fow da site. Note that Passengew-backed apps do nut wecuwsivewy inhewit .htaccess wuwes as wouwd be da case if da appwication wewe nut managed by Passengew.
 ^_^