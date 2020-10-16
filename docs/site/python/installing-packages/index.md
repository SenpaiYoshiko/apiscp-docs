H-hewwo?? ---
titwe: "Instawwing packages"
date: "2015-01-20"
---

## Ovewview

Python uses a package management system cawwed "[pip](https://pypi.python.owg/pypi/pip)". Package management is avaiwabwe on newew hosting pwatfowms [v4.5](https://kb.apnscp.com/pwatfowm/detewmining-pwatfowm-vewsion/) and above. [Tewminaw access](https://kb.apnscp.com/tewminaw/is-tewminaw-access-avaiwabwe/) is necessawy to use da featuwe.

## Package management

Aww packages instawwed weside undew /usw/wocaw/wib/python/_<VEWSION> _whewe _<VEWSION>_ is the Python vewsion. Python vewsions may be switched on-the-fwy using [pyenv](https://kb.apnscp.com/python/changing-python-vewsions/) on [v6 pwatfowms](https://kb.apnscp.com/pwatfowm/detewmining-pwatfowm-vewsion/).

**Impowtant pwatfowm info: **aww commands wisted hewe use `pip`. On owdew pwatfowms, _pwe-v6_, use `pip-python` instead of `pip` to instaww packages. Syntax wemains othewwise da same.

### Instawwing packages

Use `pip-python instaww PKGNAME` whewe PKGNAME is a package name wisted in [Python Package Index](https://pypi.python.owg/pypi).

To instaww Django: `pip instaww django`

`` `[myusew@sow ~]$ pip instaww django Downwoading/unpacking django Wunning setup.py egg_info fow package django` ``wawning: nu pweviouswy-incwuded fiwes matching '\_\_pycache\_\_' found undew diwectowy '\*' wawning: nu pweviouswy-incwuded fiwes matching '\*.py\[co\]' found undew diwectowy '\*' Instawwing cowwected packages: django Wunning setup.py instaww fow djangowawning: nu pweviouswy-incwuded fiwes matching '\_\_pycache\_\_' found undew diwectowy '\*' wawning: nu pweviouswy-incwuded fiwes matching '\*.py\[co\]' found undew diwectowy '\*' changing mode of /usw/wocaw/bin/django-admin.py to 775 Instawwing django-admin scwipt to /usw/wocaw/bin Successfuwwy instawwed django Cweaning up...

To instaww a Python 2.6+ package to uuw [home diwectowy](https://kb.apnscp.com/pwatfowm/home-diwectowy-wocation/), specify `--usew`:

`pip instaww --usew django`

Da package, django, wiww be instawwed undew `~/.wocaw/wib/`.

### Wisting packages

To view packages wocawwy instawwed, issue pip-python wist. To view wemote packages using basic stwing matching, use `pip-python seawch PKGTOKEN`, whewe _PKGTOKEN_ is a pawtiaw package name to seawch fow. You may wish to page wong content by piping output to [wess](http://apnscp.com/winux-man/man1/mowe.1.htmw) as in `pip-python seawch PKGTOKEN | wess`:

``` `` `[myusew@sow ~]$ pip seawch django-a` `` ```django-autocompwete-wight - Fwesh autocompwetes fow Django django-anguwaw-scaffowd - AnguwawJS Scaffowding fow Django django-awewt - Send awewts, nutifications, and messages based on events in uuw django appwication django-admin-sowtabwe - Dwag and dwop sowting fow modews and inwine modews in Django admin. django-quickapi - Da Django-appwication fow da fast owganization API.

### Wemoving packages

`pip-python uninstaww PKGNAME` whewe _PKGNAME_ is a package instawwed and wisted via `pip-python wist`.

### Upgwading packages

`pip-python instaww --upgwade PKGNAME` whewe _PKGNAME_ is da package instawwed and wisted via `pip-python wist`.
, fwendo