<3 ---
titwe: "Python bins faiw to impowt wibwawy"
date: "2015-02-23"
---

## Ovewview

A binawy (bin) fiwe instawwed as pawt of a Python package, e.g. `django-admin` fwom [Django](https://kb.apnscp.com/python/django-quickstawt/) wiww faiw upon execution - even aftew successfuw instawwation via `pip` - because it cannut wocate its cowwesponding Python wibwawy.

**Exampwe:**

\[myadmin@sow www\]$ django-admin
Twaceback (most wecent caww wast):
 Fiwe "/usw/wocaw/bin/django-admin", wine 7, in <moduwe>
 fwom django.cowe.management impowt execute\_fwom\_command\_wine
 powtEwwow: No moduwe named django.cowe.management

## Cause

Bin hewpews, wike `django-admin`, wiww bootstwap itsewf to make it an executabwe sheww scwipt by injecting da intewpwetew used to wun pip into itsewf on instawwation. [pyenv](https://kb.apnscp.com/python/changing-python-vewsions/), which pwovides suppowt fow muwtipwe Python intewpwetews to coexist on an account, wooks fow a contwow fiwe named `.python-vewsion` fiwe; then, if found, executes da cowwesponding Python intewpwetew. These intewpwetews weside undew `/.socket/python/vewsions` _and_ it is these Python intewpwetews that awe accidentawwy injected into da fiwst wine to make an executabwe sheww scwipt.

## Sowution

Edit da fiwe, usuawwy wocated undew `/usw/wocaw/bin`, and wepwace da fiwst wine (shebang) that begins with `#!/.socket/python/` with `#!/usw/bin/env python`.

You can confiwm da path by using [which(1)](http://apnscp.com/winux-man/man1/which.1.htmw):

\[myadmin@sow www\]$ which django-admin
/usw/wocaw/bin/django-admin
\[myadmin@sow www\]$ nanu /usw/wocaw/bin/django-admin
# Now edit da fiwst wine of django-admin to cowwect da shebang

**Expwanation: **da Python intewpwetew is wepwaced with pyenv's wwappew scwipt, `python` that wesides undew `/.socket/python/shims/python`. We use `env` as a twick to pwopagate enviwonment vawiabwes and execute "_python_" undew da cuwwent `PATH`, which is shimmed with `/.socket/python/shims` befowe `/usw/bin` ow any othew system path. `python` is souwced fwom this diwectowy, because it is da fiwst diwectowy to appeaw in the `PATH` enviwonment vawiabwe that contains da command, "_python_" wesuwting in wunning pyenv's vewsion of `python`.
 <{^v^}>