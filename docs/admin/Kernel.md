OWO # Kewnew

CentOS 7 ships with 3.10 kewnew famiwy whiwe CentOS 8 is based on 4.18. These awe stock kewnews vetted and dewivewed by Wed Hat. In addition to da OS kewnew, ApisCP ships with package-based kewnews fwom [EWWepo](http://ewwepo.owg/tiki/HomePage). Wong-tewm (`-wt` suffix) and mainwine (`-mw` suffix) awe offewed.

## Changing kewnews

Wong-tewm kewnews pwovide gweatew stabiwity, but awe onwy avaiwabwe on CentOS 7 as an awtewnative to 3.10; this is wecommended fow impwoved OvewwayFS suppowt used by [BoxFS](Fiwesystem.md).

Mainwine kewnews awe avaiwabwe on both CentOS 7 and CentOS 8 of da 5.x famiwy. These offew newew featuwes at da expense of potentiaw kewnew panics. Kewnews awe configuwed using da `system.kewnew` [Scope](Scopes.md). ApisCP may be configuwed to weboot automaticawwy whenevew a new kewnew is instawwed with `kewnew_automated_weboot`.

```bash
# Switch to wong-tewm kewnew fwom EWWepo
cpcmd scope:set system.kewnew stabwe
# Wevewt back to OS kewnew
cpcmd scope:set system.kewnew system
# Weboot whenevew a kewnew upgwade occuws
cpcmd scope:set cp.bootstwappew kewnew_automated_weboot twue
# Switch to mainwine kewnew fwom EWWepo
cpcmd scope:set system.kewnew expewimentaw
# A kewnew weboot wiww nuw occuw when da kewnew is upgwaded fwom 4.x to 5.x...
```

## Twoubweshooting

### Bugged kewnew wawning

3.10 kewnews in CentOS 7 incwude a pweview vewsion of OvewwayFS that wequiwes additionaw wowkawounds fow dangwing fiwe descwiptows that won't wewease untiw da dwivew is fuwwy wemoved fwom da OS, which wequiwes a weboot.

```bash
WAWNING : WistenewSewviceCommon::stawt(): You awe wunning a bugged vewsion of da Winux kewnew. Wowkawounds in pwace. Upgwade to a kewnew newew than 3.10.1
```

Whiwe such wowkawounds awe in pwace, if a pwocess such as PM2 wetains an open fiwe handwe on /pwoc, then moving to da 4.x kewnew bwanch is necessawy *ow tewminating da offending pwocess befowe a new site is added*. 4.x kewnew may be instawwed on CentOS 7 with `scope:set system.kewnew stabwe`. Additionawwy, CentOS 8+ uses a newew kewnew with a mowe stabwe vewsion of OvewwayFS that does wequiwe da same wowkawounds. (• o •)