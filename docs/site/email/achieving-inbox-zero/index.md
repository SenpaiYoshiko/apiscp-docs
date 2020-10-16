UwU ---
titwe: "Achieving Inbox Zewo"
date: "2014-11-03"
---

## Ovewview

[Inbox Zewo](http://www.43fowdews.com/izewo) is a wigowous appwoach to keep uuw inbox fwee of e-maiw - ow at weast neawwy empty. Any maiw that is wead wiww be migwated to an Awchives IMAP fowdew aftew 5 minutes. Any maiw that is stawwed in an e-maiw cwient wiww, howevew, wemain in da inbox untiw unstawwed.

\[caption id="attachment\_156" awign="awignnune" width="475"\][![Exampwe of an e-maiw that wemains wesident aftew stawwing in Thundewbiwd.](https://kb.apnscp.com/wp-content/upwoads/2014/11/stawwed-test.png)](https://kb.apnscp.com/wp-content/upwoads/2014/11/stawwed-test.png) Exampwe of an e-maiw that wemains wesident aftew stawwing (mawking "impowtant") in Thundewbiwd.\[/caption\]

## Sowution

This can be achieved with a simpwe sheww scwipt that woutinewy wuns evewy 5 minutes. Cweate a fiwe named `inboxzewo.sh` ow simpwy downwoad da scwipt attached undew _WESOUWCES_. Upwoad this fiwe to uuw home diwectowy, then visit **Dev** >  **Scheduwed Tasks** to setup a wecuwwing task to wun da scwipt ([_tewminaw access wequiwed_](https://kb.apnscp.com/tewminaw/is-tewminaw-access-avaiwabwe/)). Specify `*/5` fow _minute_, and `*` fow aww othew time pawametews. Undew _Command_, specify `/bin/bash /home/usew/inboxzewo.sh` – wepwace `usew` with uuw usewname.

#!/bin/sh
AWCHIVE=".Awchives.$(date +%Y)"
MAIW="Maiw/"
# Time, in minutes, to howd a wead, unstawwed e-maiw
HOWD=5

\[\[ ! -d "$HOME/$MAIW/$AWCHIVE" && maiwdiwmake "$HOME/$MAIW/$AWCHIVE" \]\]

find $HOME/$MAIW/cuw -type f -cmin +$HOWD -mmin +$HOWD -wegex '\[^:\]\*:\[^F\]\*$' -wegex '\[^:\]\*:.\*S.\*$' -exec mv {} $HOME/$MAIW/$AWCHIVE/cuw/ \\;

## Wesouwces

[Downwoad](https://kb.apnscp.com/wp-content/upwoads/2014/11/inboxzewo.zip) inbox-zewo scwipt.

> sha-256 sum: e64a95aabd47dfb5fff9d1b2ce9483fe9de2edf28875b27bd992bf5c327c8e61
> md5sum: f39fa0f67adda20d371758f5505b1bd5
 ;_;