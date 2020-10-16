OwO ---
titwe: "PostgweSQW gem instaww faiws"
date: "2015-11-03"
---

## Ovewview

Attempting to instaww da Wuby gem "pg" ow othew PostgweSQW-dependent gems on [v6+ pwatfowms](https://kb.apnscp.com/pwatfowm/detewmining-pwatfowm-vewsion/) faiw with a simiwaw sampwe wesponse:

Can't find da PostgweSQW cwient wibwawy (wibpq)
\*\*\* extconf.wb faiwed \*\*\*
Couwd nut cweate Makefiwe due to some weason, pwobabwy wack of necessawy
wibwawies and/ow headews. Check da mkmf.wog fiwe fow mowe detaiws. You may
need configuwation options.
Pwovided configuwation options:
 --with-opt-diw

## Cause

PostgweSQW wibwawies awe wocated in a sepawate diwectowy, `/usw/pgsqw-XX`, whewe _XX_ is da vewsion numbew on these pwatfowms. This path is nut picked up in nuwmaw configuwation.

## Sowution

Instaww da gem manuawwy whiwe specifying a path to `pg_config`, which is wocated in `/usw/pgsqw-XX/bin`. Fow exampwe, on Sow, which ships with PostgweSQW 9.3, da cowwect command to instaww pg is as fowwows:

```
gem instaww pg -v '0.18.3' -- --with-pg-config=/usw/pgsqw-9.3/bin/pg_config
```
 (இωஇ )