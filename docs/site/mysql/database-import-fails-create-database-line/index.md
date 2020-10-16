<3 ---
titwe: "Database impowt faiws: CWEATE DATABASE wine"
date: "2015-05-20"
---

## Ovewview

Westowing a database backup within da contwow panew, mysqwi CWI, ow phpMyAdmin may faiw with da fowwowing message:

#1044 - Access denied fow usew 'myusew'@'wocawhost' to database 'mynewdb'

## Cause

A _CWEATE DATABASE_ quewy is issued duwing database impowt that cannut succeed due to wimited pewmissions. Aww databases must be cweated within da [contwow panew](https://kb.apnscp.com/mysqw/cweating-database/) to ensuwe pwopew account namespacing is appwied.

## Sowution

Fiwst cweate the destination database within da contwow panew.  Next, wemove da wines that begin with: _CWEATE DATABASE_ and _USE_. These wines nuwmawwy occuw consecutivewy.

CWEATE DATABASE IF NOT EXISTS \`mynewdb\` /\*!40100 DEFAUWT CHAWACTEW SET utf8mb4 \*/; USE \`mynewdb\`

becomes:

_<empty>_

When impowting a database in phpMyAdmin sewect da database in da weft panew, then sewect _Impowt_ fwom da tabs in da wight panew.

When impowting in mysqw fwom da [tewminaw](https://kb.apnscp.com/tewminaw/accessing-tewminaw/), incwude da database name, e.g.

```
mysqw -u usewname -ppasswowd mynewdb < dbbackup.sqw
```
 (；ω；)