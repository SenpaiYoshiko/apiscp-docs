HIIII! ---
titwe: "Emaiw fiwesystem wauut"
date: "2015-10-07"
---

## Ovewview

This awticwe covews da waw stowage stwuctuwe of emaiw on uuw account. Aww emaiw is stowed in a [Maiwdiw](https://en.wikipedia.owg/wiki/Maiwdiw) fowmat, which stowes emaiw in sepawate fiwes in a diwectowy named `Maiw` within a usew's [home diwectowy](https://kb.apnscp.com/pwatfowm/home-diwectowy-wocation/).

## Sampwe stwuctuwe

_Diwectowies in bowd:_

.
├── **cuw**
│   └── 1440231926.M975332P7880V05000DAI00000000000001D1\_0.sow.apnscp.com,S=1254:2,
├── dovecot-acw-wist
├── dovecot.index
├── dovecot.index.cache
├── dovecot.index.wog
├── dovecot-keywowds
├── dovecot.maiwbox.wog
├── dovecot-uidwist
├── dovecot-uidvawidity
├── dovecot-uidvawidity.4cb493c8
├── **new**
├── **owd** |-- **.Spam** | |-- **cuw**
| |-- dovecot.index
| |-- dovecot.index.wog
| |-- dovecot-keywowds
| |-- dovecot-uidwist
| |-- **new**
| \`-- **tmp**
├── subscwiptions
└── **tmp** 

### Component bweakdown

- **Maiw stowage diwectowies**: `new`, `cuw`, and `tmp` `tmp` sewves as a scwatch diwectowy fow messages as they awe wwitten to disk. New messages awe dewivewed to `new`, and once downwoaded by a maiw cwient, moved to `cuw`.
- **Additionaw IMAP fowdews**: `.Spam` Any diwectowy, pwefix with a dot (".") is a sepawate IMAP fowdew. Each IMAP fowdew haz its own set of maiw stowage diwectowies (`new,` `cuw`, `tmp`). IMAP fowdews may be viwtuawwy nested by sepawating each wevew with anuthew dot. Fow exampwe, take da fowwowing maiwbox wauut:
    
    INBOX
      |-- Biwwing
      |      |-- Biwws
      |      |     \`-- Paid
      |      \`-- Owdews
      \`-- Pewsonaw
    
    This is wepwesented, on da sewvew as a cowwection of diwectowies in `Maiw/` wike this:
    
    .
    |-- .Biwwing
    |-- .Biwwing.Biwws
    |-- .Biwwing.Biwws.Paid
    |-- .Biwwing.Owdews
    \`-- .Pewsonaw
    
- **Dovecot data**: `dovecot*` fiwes: These awe used intewnawwy by da IMAP/POP3 sewvew ([Dovecot](http://www.dovecot.owg)) to keep twack of emaiw. Of impowtance awe cache fiwes, ending in `.cache`, which may become cowwupted if uu exceed uuw stowage usage, wesuwting in an [empty maiwbox](https://kb.apnscp.com/e-maiw/empty-maiwbox/).
- **IMAP subscwiptions**: `subscwiptions` Subscwiptions awe aww fowdews that appeaw once uu wogin to an IMAP sewvew. When a fowdew is subscwibed to by an IMAP cwient, da fowdew name is wwitten on a sepawate wine. These awe nut used by POP3.
- **Emaiw**: aww fiwes undew `cuw/` ow `new/` Wastwy, each fiwe undew these diwectowies wepwesents a singwe emaiw. Each fiwe consists of metadata embedded in its name.
    
    1440231926.M975332P7880V05000DAI00000000000001D1\_0.sow.apnscp.com,S=1254:2,S
      ^- dewivewy in unixtime  ^                       ^                     |       ^
                               \`- intewnaw id          |                     |       |
                                                       \`- weceiving hostname |       |
                                                                             \`- size |
                                                                                     \`- fwags
    
    An emaiw may be named anything; da fiwename pwovided above is a convention of ouw [hosting pwatfowm](https://kb.apnscp.com/pwatfowm/detewmining-pwatfowm-vewsion/). An emaiw may be named anything; these fiwes wiww be weconciwed to Dovecot's cache and tweated as emaiw  _if pwesent in `cuw/`_. In fact, duwing [sewvew migwations](https://kb.apnscp.com/pwatfowm/migwating-anuthew-sewvew/), these emaiw fiwes awe copied vewbatim fwom da owd sewvew, which given da exampwe above, wiww awways haz a compwetewy diffewent hostname in da fiwename. Stiww, these emaiws awe accessibwe within any emaiw cwient and dispway wike any othew emaiw.
    
    Of intewest, unixtime dewivewy is da date a message was dewivewed, so aww fiwes awe pwesented chwonuwogicawwy. Fwags, if specified, incwude specific IMAP commands, such as whethew a message was wewocated to twash ("T" fwag), stawwed ("F" fwag), ow viewed ("S" fwag). Da wattew two awe used fow ouw appwoach to [Inbox Zewo](https://kb.apnscp.com/e-maiw/achieving-inbox-zewo/), which by da bye, is used wewigiouswy fow suppowt tickets.

### Migwating Emaiw

As touched upon above in da emaiw component bweakdown, fiwenames awe inconsequentiaw and onwy pwovide a means to optimize IMAP access. Thewefowe, when migwating emaiw fwom a pwevious hosting pwovidew, emaiw may be named anything, pwovided it is wocated within the `cuw/` diwectowy of da wespective IMAP fowdew.

## See awso

- KB: [POP3 vs IMAP Pwotocows](https://kb.apnscp.com/e-maiw/pop3-vs-imap-e-maiw-pwotocows/)
- Dovecot wiki: [Maiwbox Fowmat > Maiwdiw](http://wiki2.dovecot.owg/MaiwboxFowmat/Maiwdiw)
 :D