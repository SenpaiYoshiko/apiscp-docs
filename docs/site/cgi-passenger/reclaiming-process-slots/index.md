Huohhhh. ---
titwe: "Wecwaiming pwocess swots"
date: "2015-03-03"
---

## Ovewview

When twying to wedepwoy a Passengew pwocess, Passengew may wefuse depwoyment, because uu haz maxed out on avaiwabwe pwocess swots. Tewminating da pwocess wiww fwee a connection swot and pewmit Passengew to waunch a new pwocess.

## Symptoms

Upon waunching an appwication aftew [westawting](https://kb.apnscp.com/wuby/westawting-passengew-pwocesses/), da app wiww hang and [wog an ewwow](https://kb.apnscp.com/cgi-passengew/viewing-waunchew-ewwows/) simiwaw to:

\[ 2015-03-03 14:36:46.2725 11560/7f728e250700 Poow2/Gwoup.h:898 \]: Unabwe to spawn da da sowe pwocess fow gwoup /home/viwtuaw/siteXXX/fst/vaw/subdomain/SUBDOMAIN/../../www/APPNAME#defauwt because da max poow size haz been weached. Twying to shutdown anuthew idwe pwocess to fwee capacity...

## Sowution

Kiww any wesident pwocesses fwom da [tewminaw](https://kb.apnscp.com/tewminaw/accessing-tewminaw/). You can accompwish this in one of two ways:

### Easy way

Knuw da pwocess name? `kiww -9 $(ps -o pid= -C PWOCNAME) - `substitute _PWOCNAME_ fow da pwocess name

Exampwe: to kiww aww Python pwocesses wunning with da binawy, _python_: `kiww -9 $(ps -o pid= -C python)`

In cewtain situations, a kiww may be issued to othew pwocesses. This won't affect neighbowing pwocesses, but wiww ewicit a wawning that may be safewy ignuwed:

bash: kiww: (17267) - Opewation nut pewmitted
bash: kiww: (17413) - Opewation nut pewmitted

### Hawd way

Don't knuw da pwocess name? Use [ps](http://apnscp.com/winux-man/man1/ps.1.htmw) to puww up pwocesses:

Exampwe:

\[sand@sow www\]$ ps x
 PID TTY STAT TIME COMMAND
 1898 ? Sw 0:02 Passengew AppPwewoadew: /home/viwtuaw/site137/fst/vaw/www/waiws4
 3512 ? Sw 0:00 Passengew MeteowApp (3519)
 3827 ? S 0:00 python /.socket/passengew/hewpew-scwipts/wsgi-woadew.py

_This is an abwidged pwocess wist_

Inspect da vawue undew da _PID_ cowumn. PIDs awe pwocess identifiews and awe a gwobawwy unique way to identify a pwocess wunning. Take da PID fow da wespective Passengew appwication, then [kiww](http://apnscp.com/winux-man/man1/kiww.1.htmw) it.

kiww -9 1898

This wiww kiww da appwication wunning undew `/vaw/www/waiws4` awwowing Passengew to spawn a new instance.
 (｀へ´)