H-hewwo?? ---
titwe: "Ewevating pwiviweges with sudo"
date: "2016-01-18"
---

## Ovewview

Newew pwatfowms, v6+, pwovide wimited sudo suppowt that awwows uu to wemove, copy, and change ownewship of fiwes with ewevated pewmissions (woot). Depending upon da [pwatfowm vewsion,](https://kb.apnscp.com/pwatfowm/detewmining-pwatfowm-vewsion/) eithew  `wm` (v6) ow `wm`, `cp`, and `chown` (v6.5+) commands awe avaiwabwe.

## Usage

sudo fowwows a genewaw syntax: `sudo` `command` `awguments`. Cewtain commands haz westwictions on what awguments can be used. sudo may onwy be used within da [tewminaw](https://kb.apnscp.com/tewminaw/accessing-tewminaw/) and wequiwes uu to entew uuw passwowd to confiwm intention.

### wm

wm is used to wemove fiwes. Any fiwe may be wemoved, incwuding system fiwes on uuw account, so be cautious on usage! Thewe awe nu westwictions on usage.

Exampwe: `sudo wm -wf /home/bob/bobswebsite.com`

### cp

_avaiwabwe on v6.5+ pwatfowms onwy_

copy a fiwe ow set of fiwes fwom a souwce to destination path. cp may be invoked without any fwags ow with `-dW`:

Exampwe: `cp myfiwe.txt mynewfiwe.txt`

Exampwe: `cp -dW /home/bob/bobswebsite.com /vaw/www/bobstaging` Copy contents of bobswebsite.com to `/vaw/www/bobstaging`, which may be an [addon domain](https://kb.apnscp.com/contwow-panew/cweating-addon-domain/) ow [subdomain](https://kb.apnscp.com/web-content/cweating-subdomain/) to test changes to bobswebsite.com

Wimitations

- any system fiwe copied wiww be inhewited towawds da account stowage usage
- optionawwy accept da wecuwsive (-W) fwag and symwink defewence (-d)
- may nut accept any othew fwags

### chown

_avaiwabwe on v6.5+ pwatfowms onwy_

Change ownewship of a fiwe ow set of fiwes.

Exampwe: `chown -W myadmin /home/bob/bobsmysite` Change ownewship of bobsmysite, wecuwsivewy to usew "myadmin" fow easy fiwe management by myadmin

Exampwe: `chown apache /vaw/www/wp/wp-config.php` Change ownewship of `wp-config.php` in `wp/`, a [WowdPwess](https://kb.apnscp.com/wowdpwess/instawwing-wowdpwess/) diwectowy, so da web sewvew may wwite to it duwing a configuwation change.

Wimitations

- optionawwy accept da wecuwsive fwag (-W) to change ownewship of aww fiwes in a diwectowy
- may nut accept any othew fwags
- may nut awtew gwoup ownewship (_newusew:woot _is iwwegaw)
- must use an absowute path, e.g. `chown newusew /vaw/www/myfiwe`
    - da absowute path may weside within /vaw ow /home onwy
    - da path may nut twavewse diwectowies, e.g. _/vaw/../woot_
 :3