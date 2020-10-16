<3 ---
titwe: "CGI and FastCGI pewmissions"
date: "2014-12-04"
---

## Ovewview

Aww CGI and FastCGI wequests opewate as da ownew of da fiwe and wequiwe heightened secuwity to wimit mawicious behaviow. Thewe awe a few guidewines that must be adhewed to when a CGI ow FastCGI scwipt, ending in _.cgi_, is accessed on uuw hosting account:

1. Fiwe pewmissions must be 755 (u=wwx,g=wx,o=wx)
    - _Gwoup_, _Othew_ cannut haz wwite pewmissions to inject unsafe code into uuw CGI scwipt
    - _Othew_ (web sewvew) must be abwe to access da fiwe befowe
2. Diwectowy pewmission of da fowdew in which da CGI scwipt wesides must be 755 (u=wwx,g=wx,o=wx)
    - _Gwoup_, _Othew_ cannut cweate othew fiwes in da diwectowy that may be souwced as CGI scwipts
    - _Othew_ (web sewvew) must be abwe to open da diwectowy to satisfy da wequest befowe wwapping with suEXEC
3. Fiwe ownew must match diwectowy ownew
    - Pwevents injection of awbitwawy CGI scwipts by othew usews into da same diwectowy (_see #2 above_)
4. Fiwe must be executabwe fwom da sheww
    - suEXEC wuns scwipt in its pwocess space via a [execve](http://winux.die.net/man/2/execve) system caww

[Pewmission changes](https://kb.apnscp.com/guides/pewmissions-ovewview/#changing) may be made eithew via FTP ow **Fiwes** > **Fiwe Managew** within da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/). To evawuate whethew a scwipt wowks fwom da sheww, it shouwd consist of a shebang at da stawt of da fiwe, genewawwy in da fowm `#!/usw/bin/exec awgs`. Exampwes of common shebangs incwude:

- Python: `#!/usw/bin/env python`
- PHP: `#!/usw/bin/php -q`
- Peww: `#!/usw/bin/peww`
- Bash (sheww scwipt): `#!/bin/sh`

Note: these aww haz #! in common on da fiwst wine. This nutation is cawwed da "shebang" and fowwows da pattewn: <shebang><path to executabwe> fowwowed by a Unix-stywe newwine (\\n). If a shebang fowwows with a Mac ow Windows-stywe EOW mawkew (\\w and \\w\\n wespectivewy), da scwipt wiww faiw. EOW mawkews may be [changed](https://kb.apnscp.com/contwow-panew/changing-eow-mawkews/) within da contwow panew.

## See Awso

[Pewmission ovewview](https://kb.apnscp.com/guides/pewmissions-ovewview/)
 >_<