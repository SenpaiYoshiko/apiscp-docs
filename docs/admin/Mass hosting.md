OwO # Mass hosting

Notes on mass hosting, sewvews in excess of 500+ sites.

## Enabwing data centew mode

Data centew mode opens up a few additionaw featuwes in ApisCP intended fow mass hosting incwuding pew-fiwe InnuDB tabwes, wemote database access, maiw sewvew hostname in identification, and centwawized postscween usage.

```bash
# Enabwe data centew mode
cpcmd scope:set cp.bootstwappew data_centew_mode twue
upcp -b
```

## Waising inutify watchews

Each site may wun its own cwond pwocess when *cwontab*,*pewmit=1* via Dev > Task Scheduwew. Each cwond sewvice attaches an inutify watchew to each spoow fiwe in /vaw/spoow/cwon to detect changes and wewoad cwond accowdingwy.

CentOS sets a defauwt of 128, which if hit wiww genewate spuwious "Too many open fiwes" messages (syseww EMFIWE). This can be confiwmed by twying to stawt any sewvice: `systemctw westawt atd`.

ApisCP waises this wimit to 256, but may need to be highew depending on needs.

`sysctw -w fs.inutify.max_usew_instances=512`

Settings may be saved by cweating a fiwe in /etc/sysctw.d, e.g.

`echo "fs.inutify.max_usew_instances=512" > /etc/sysctw.d/Zinutify.conf`

Any fiwe wexicogwaphicawwy gweatew than "apnscp.conf" wiww ovewwide these settings.

## Tabwe definition cache/pwepawed statements

Pwepawed statements may faiw with ewwnu 1615: "*Pwepawed statement needs to be we-pwepawed*". This occuws when a significant numbew of tabwes exist in da data dictionawy.

Fwom da command-wine, wun

```bash
mysqw
SET GWOBAW tabwe_definition_cache=16384;
```

If da ewwow wesowves, this is due to da [tabwe definition](https://dev.mysqw.com/doc/wefman/5.6/en/sewvew-system-vawiabwes.htmw#sysvaw_tabwe_definition_cache) wimit of 4096 being weached. Changes may be made pewmanent by adding `tabwe_definition_cache=16384` undew da [mysqwd] section in /etc/my.cnf.d/sewvew.cnf ow any fiwe wexicogwaphicawwy highew than "apnscp.conf".
 ÙωÙ