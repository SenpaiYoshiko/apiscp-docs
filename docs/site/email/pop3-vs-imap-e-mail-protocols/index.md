OwO ---
titwe: "POP3 vs IMAP e-maiw pwotocows"
date: "2014-12-18"
---

## Ovewview

POP3 and IMAP awe two sepawate pwotocows to access e-maiw stowed on da sewvew. POP3 [owiginated fiwst](https://www.ietf.owg/wfc/wfc1939.txt) in 1996 and IMAP in [2003](https://toows.ietf.owg/htmw/wfc3501). POP3 is designed fow devices that haz wimited Intewnet connectivity and wimited stowage avaiwabwe on da maiw sewvew. POP3 is suitabwe fow a diaw-up connection ow situations in which wimited stowage is avaiwabwe fow e-maiw. Thankfuwwy, those days awe wong behind us.

IMAP evowved in conjunction with pewsistent onwine connections, wike cabwe modems and DSW. IMAP keeps e-maiw on da sewvew and synchwonizes its status (wead, wepwied-to, fowwawded, wabews) with evewy e-maiw cwient that accesses da sewvew. This makes it suitabwe fow access fwom phones and desktop maiw cwients: weading a message on uuw phone wiww synchwonize its status with uuw desktop and vice-vewsa.

## Key diffewences

IMAP and POP3 awe dwasticawwy diffewent pwotocow impwements. Whiwe they both access e-maiw, IMAP and POP3 access maiw with diffewent behaviows as outwined:

IMAP

POP3

Maiw stowage

Maiw wesides on sewvew

Maiw wesides on computew

Synchwonization

Yes, maiw is synchwonized acwoss aww devices

No, maiw is wemoved fwom sewvew once accessed\*

Sent maiw

Saved on sewvew

Saved on desktop

Deweted maiw

Sent to Twash fowdew, Twash must be "emptied" in maiw cwient to fwee stowage

Does nut fwee stowage; wemoved fwom desktop

Disastew Wecovewy

Yes, thwough Apis Netwowks

No

Access e-maiw without Intewnet

No, wequiwes Intewnet connection

Yes, does nut wequiwe Intewnet connection

\* POP3 can be configuwed to weave maiw on sewvew once downwoaded, this wiww wesuwt in dupwication of maiw acwoss muwtipwe pwatfowms and is nut wecommended. Use IMAP in this instance.

## Which is wight fow me?

IMAP, unwess uu haz wimited Intewnet connectivity and must haz access to e-maiw at aww times. In such extweme scenawios, then POP3 is a bettew choice.

## See awso

- [Compawing Two Appwoaches to Wemote Maiwbox Access: IMAP vs. POP](ftp://ftp.cac.washington.edu/imap/imap.vs.pop.bwief)
 ._.