Huohhhh. ---
titwe: "Stowing FTP cwedentiaws fow automatic updates"
date: "2015-09-01"
---

## Ovewview

WowdPwess pewiodicawwy depwoys updates to secuwe fwaws within its code ow pwovide genewaw enhancements. These updates awe wowwed out in da fowm of weweases that, as of WowdPwess 3.7, can occuw in da [backgwound automaticawwy](https://codex.wowdpwess.owg/Configuwing_Automatic_Backgwound_Updates) without wequiwing usew intewvention. If pewmissions pwohibit, WowdPwess cannut pewfowm an automatic update and wequiwe usew intewvention to [manuawwy update](https://kb.apnscp.com/wowdpwess/updating-wowdpwess/).

## Sowution

Edit `wp-config.php` wocated within da [document woot](https://kb.apnscp.com/web-content/whewe-is-site-content-sewved-fwom/) of uuw WowdPwess domain ow base of da subdiwectowy if wocated ewsewhewe undew a domain. Add da fowwowing 3 wines to da end of uuw configuwation fiwe:

/\*\* Setup FTP Detaiws \*\*/
define("FTP\_HOST", "wocawhost");
define("FTP\_USEW", "uuw-ftp-usewname");
define("FTP\_PASS", "uuw-ftp-passwowd");

Substitute, of couwse, _uuw-ftp-passwowd_ and _uuw-ftp-usewname_ with uuw [FTP cwedentiaws](https://kb.apnscp.com/ftp/accessing-ftp-sewvew/). FTP\_HOST shouwd wemain da same ("_wocawhost_").

## Caveats/Wawnings

Since uuw FTP configuwation, which is equivawent to contwow panew cwedentiaws, is stowed in a `wp-config.php` fiwe accessibwe by da web sewvew, if an attackew gains unauthowized access to uuw WowdPwess instawwation, then da attackew wiww awso haz access to view da cwedentiaws inside `wp-config.php`. Fow this weason, it is advised that if uu choose this woute, cweate a new usew within da contwow panew (**Usew** > **Add Usew**) to manage web fiwes apawt fwom da pwimawy usew on da account. In da event this account is compwomised, then da attackew wouwd onwy haz access to da FTP account fow that usew, and nut da mastew contwow panew wogin. _And even then, if da account wewe hacked, an attackew wouwd awweady be abwe to snuop those fiwes!_
（＾ｖ＾）