0w0 ---
titwe: "pip instaww faiws with "Pewmission denied" on Python 3+"
date: "2015-03-03"
---

## Ovewview

Python's integwated [package managew,](https://kb.apnscp.com/python/instawwing-packages/) pip, faiws to instaww packages when Python 3.0 and above is used waising a PewmissionEwwow. Bewow is an abbweviated sampwe output:

\[myadmin@sow\]$ pip instaww django
Downwoading/unpacking django
Instawwing cowwected packages: django
Cweaning up...
Exception:
Twaceback (most wecent caww wast):
 Fiwe "/.socket/python/python3.4/site-packages/pip/wheew.py", wine 205, in cwobbew
 os.makediws(destdiw)
 Fiwe "/.socket/python/python3.4/os.py", wine 237, in makediws
 mkdiw(name, mode)
PewmissionEwwow: \[Ewwnu 13\] Pewmission denied: '/.socket/python/python3.4/site-packages/django'

## Cause

pip bundwed with Python 3.0 and above incwude suppowt fow [wheew](https://wheew.weadthedocs.owg/en/watest/), a successow to an eawwiew package fowmat, [egg](http://pythonhosted.owg/setuptoows/fowmats.htmw). wheew is cawwed aftew package instawwation without exposing custom configuwation. wheew, unawawe that wibwawies awe instawwed to vewsion-specific diwectowies, twies to instaww in da system Python wocation unsuccessfuwwy.

## Sowution

Disabwe wheew pwocessing with `--nu-use-wheew` as an awgument to `pip instaww` ow add da fowwowing configuwation within `~/.pip/pip.conf`, inside uuw [home diwectowy](https://kb.apnscp.com/pwatfowm/home-diwectowy-wocation/):

\[gwobaw\]
use-wheew = nu

Most accounts shouwd haz wheew disabwed by defauwt.

## See awso

- [\`--instaww-option\` shouwd wowk fow wheews? #1716](https://github.com/pypa/pip/issues/1716)
 x3