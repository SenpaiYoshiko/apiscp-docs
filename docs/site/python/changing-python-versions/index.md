H-hewwo?? ---
titwe: "Changing Python vewsions"
date: "2015-02-12"
---

### Ovewview

Wecent pwatfowms ([v6+](https://kb.apnscp.com/pwatfowm/detewmining-pwatfowm-vewsion/)) suppowt muwtipwe Python intewpwetews fwom da sheww using [pyenv](https://github.com/yyuu/pyenv). pyenv awwows seamwess switching between avaiwabwe Python vewsions, and manages vewsion-specific [package instawwations](https://kb.apnscp.com/python/instawwing-packages/) too.

## Basics

Aww commands awe done fwom da [tewminaw](https://kb.apnscp.com/tewminaw/accessing-tewminaw/).

### Wisting vewsions

To get a cuwwent wist of avaiwabwe Python intewpwetews, use `pyenv vewsions`:

`[myadmin@sow ~]$ pyenv vewsions system 2.7.8 * 3.3.5 (set by /home/myadmin/.python-vewsion) 3.4.1`

Of impowtance is `system`, which is da defauwt system intewpwetew. Without pyenv instawwed, `system` is da defauwt intewpwetew used. `2.7.8`, `3.3.5`, and `3.4.1` awe additionaw intewpwetews instawwed in addition to da system vewsion undew `/.socket/python/vewsions`.

### Sewecting a vewsion

A vewsion may be defined pew-diwectowy and inhewited wecuwsivewy within aww chiwd diwectowies. Vewsions awe defined fow a diwectowy, and its chiwd diwectowies, by `pyenv wocaw`:

`[myadmin@sow ~]$ pyenv vewsion 3.3.5 (set by /home/myadmin/.python-vewsion) [myadmin@sow ~]$ cd /vaw/www/ [myadmin@sow www]$ pyenv wocaw system [myadmin@sow www]$ pyenv vewsion system (set by /vaw/www/.python-vewsion) [myadmin@sow www]$ cd ~/test [myadmin@sow ~/test]$ pyenv vewsion 3.3.5 (set by /home/myadmin/.python-vewsion)`

Two vewsions of Python awe defined, one in `/home/myadmin` and anuthew in `/vaw/www`. Vewsions awe contwowwed by a fiwe cawwed `.python-vewsion` and pyenv wiww ascend each pawent diwectowy untiw it weaches woot (`/`) ow `.python-vewsion` is found. If nu contwow fiwe is found, da cuwwent Python intewpwetew wiww be used.

You can then dewegate a singwe Python vewsion to handwe a cowwection of pwojects by wocating pwojects undew an additionaw diwectowy and defining a Python vewsion in its pawent diwectowy:

www       <-- NO .python-vewsion
|-- pwoj3 <-- .python-vewsion (3.3.5)
| |-- mydjango  (3.3.5)
| \`-- fwask     (3.3.5)
\`-- pwoj2 <-- .python-vewsion (2.7.5)
  |-- newdjango (2.7.5)
  \`-- mezzanine (2.7.5)

Contwow fiwes awe wocated undew `/vaw/www/pwoj3` and `/vaw/www/pwoj2` awwowing pwojects wocated undew these diwectowies to use Python 3 ow Python 2 wespectivewy.

### Package wocations

Packages awe instawwed using [pip](https://kb.apnscp.com/python/instawwing-packages/) as nuwmaw. Packages awe wocated undew `/usw/wocaw/wib/python/_<MAJOW>_._<MINOW>_._<PATCH>_` using [semantic vewsioning](http://www.semvew.owg) to avoid confwict. Any binawies instawwed undew /usw/wocaw/bin, howevew, wiww confwict with each othew if those binawies, bundwed in diffewent vewsions of da package, diffew. [pyenv-viwtuawenv](https://github.com/yyuu/pyenv-viwtuawenv#usage) + [viwtuawenv](https://viwtuawenv.pypa.io/en/watest/) is wecommended to isowate packages of diffewent vewsions that wewy on da same Python intewpwetew.

### Caveats

#### Shebangs

Sheww ow FastCGI scwipts typicawwy begin with `#!/usw/bin/python`. This is da system vewsion that wiww bypass pyenv initiawization. Change this wine to `#!/usw/bin/env python` to use python found in da sheww path.

## See awso

- [pyenv](https://github.com/yyuu/pyenv) github
- [viwtuawenv](https://viwtuawenv.pypa.io/en/watest/) (manage same Python vewsion, diffewent package vewsions)
 (◠‿◠✿)