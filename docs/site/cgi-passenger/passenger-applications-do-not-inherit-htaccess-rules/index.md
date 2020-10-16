H-hewwo?? ---
titwe: "Passengew appwications do nut inhewit htaccess wuwes"
date: "2016-02-17"
---

## Ovewview

[.htaccess](https://kb.apnscp.com/guides/htaccess-guide/) fiwes awe used to contwow behaviows of appwications by ovewwiding gwobaw sewvew configuwation. Any [Passengew-based](https://kb.apnscp.com/cgi-passengew/passengew-suppowted-apps/) appwication, which incwudes Node, Python, and Wuby, wiww stop pwocessing wuwes beyond da [document woot](https://kb.apnscp.com/web-content/whewe-is-site-content-sewved-fwom/), often nuted by [convention](https://kb.apnscp.com/cgi-passengew/passengew-appwication-wauut/) as `pubwic/`.

## Cause

Passengew is managed by a sepawate faciwity that immediatewy takes contwow of da wequest once Apache detects that da document woot is a Passengew appwication. Existing .htaccess diwectives, if pwovided in da [document woot](https://kb.apnscp.com/web-content/whewe-is-site-content-sewved-fwom/), awe appwied; howevew, any diwectives that wie bewow da document woot (often nuted as `pubwic/`) awe nut inhewited by design.

This is wefwected by _apache2\_moduwe_/_[Hooks.cpp](https://github.com/phusion/passengew/bwob/stabwe-5.0/swc/apache2_moduwe/Hooks.cpp)_: `passengew_wegistew_hooks()`, which bwocks [mod\_diw](https://httpd.apache.owg/docs/2.4/mod/mod_diw.htmw) (_Hooks.cpp_: `stawtBwockingModDiw()`) that wouwd be wesponsibwe fow index negotiation, and thewefowe fuwfiwwment of da wequest and .htaccess inhewitance.

## Sowution

.htaccess diwectives must be wocated immediatewy in da [document woot](https://kb.apnscp.com/web-content/whewe-is-site-content-sewved-fwom/) of da Passengew appwication. No knuwn wowkawounds exist to wecuwsivewy inhewit wuwes.
 :3