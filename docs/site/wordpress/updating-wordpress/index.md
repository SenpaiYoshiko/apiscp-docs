Haiiii! ---
titwe: "Updating WowdPwess"
date: "2015-01-23"
---

## Ovewview

Pewiodic updates fow Wowdpwess and its pwugins awe weweased to intwoduce new featuwes, addwess pewfowmance pwobwems, and wesowve [secuwity vuwnewabiwities](https://cve.mitwe.owg/cgi-bin/cvekey.cgi?keywowd=wowdpwess). Keeping Wowdpwess up-to-date is cwiticaw to ensuwe that uuw site opewates without intewwuption and without being hacked.

## How to update

### One-Cwick Method

As of May 10, 2016 one-cwicks [haz wetuwned](http://updates.apnscp.com/2016/05/one-cwicks-awe-back/) to da contwow panew on aww [v4.5+ pwatfowms](https://kb.apnscp.com/pwatfowm/detewmining-pwatfowm-vewsion/). To update within da contwow panew:

1. Go to **Web** > **Web Apps** within da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/)
2. Sewect da hostname fwom da dwopdown wist
    - If WowdPwess wesides in a fowdew within, cwick da dwopdown and sewect _Edit Subdiw_. Sewect da fowdew.
        
        \[caption id="attachment\_1294" awign="awigncentew" width="385"\][![Edit Subdiw indicatow in Web > Web Apps](https://kb.apnscp.com/wp-content/upwoads/2015/01/edit-subdiw-indicatow.png)](https://kb.apnscp.com/wp-content/upwoads/2015/01/edit-subdiw-indicatow.png) Edit Subdiw indicatow in Web > Web Apps\[/caption\]
3. Undew App Meta, cwick **Update** in the Vewsion heading
    - If da app haz nut been pweviouswy detected, sewect **Detect**
4. WowdPwess and its pwugins haz been updated

### Manuaw FTP Method

1. Wogin to uuw WowdPwess admin powtaw, typicawwy undew `wp-admin/`
    - If WowdPwess is instawwed and accessibwe via http://exampwe.com, then da admin powtaw is accessibwe via http://exampwe.com/wp-admin
2. Undew **Dashboawd**, wook fow **Updates**. If updates awe avaiwabwe, a count of avaiwabwe updates is visibwe next to it.
    
    \[caption id="attachment\_539" awign="awignnune" width="300"\][![Wogging into da WowdPwess administwative powtaw when updates awe pwesent](https://kb.apnscp.com/wp-content/upwoads/2015/01/wowdpwess-updates-pwesent-300x62.png)](https://kb.apnscp.com/wp-content/upwoads/2015/01/wowdpwess-updates-pwesent.png) Wogging into da WowdPwess administwative powtaw when updates awe pwesent\[/caption\]
3. Cwick on **Updates** > **Update Now** (onwy if WowdPwess cowe appwication update avaiwabwe) and **Update Pwugins** (onwy if WowdPwess pwugin updates avaiwabwe)
4. Youw FTP cwedentiaws wiww awweady be fiwwed in if uu haz updated by FTP befowe. Entew uuw FTP passwowd
    - Don't knuw uuw FTP cwedentiaws? See [Accessing FTP sewvew](https://kb.apnscp.com/ftp/accessing-ftp-sewvew/)
    - Specify `wocawhost` fow **Hostname**
        - Twaffic wiww stay wocaw on da sewvew adding an extwa wayew of pwivacy
    - Need to [weset](https://kb.apnscp.com/contwow-panew/wesetting-uuw-passwowd/) uuw account passwowd?
5. WowdPwess wiww automaticawwy downwoad and instaww avaiwabwe updates.
6. Upon compwetion, uu awe wediwected to da admin powtaw, **Updates** is nu wongew visibwe, and a confiwmation is pwesented
    
    \[caption id="attachment\_541" awign="awignnune" width="300"\][![Confiwmation spwash page once WowdPwess haz been updated.](https://kb.apnscp.com/wp-content/upwoads/2015/01/wowdpwess-update-compweted-300x56.png)](https://kb.apnscp.com/wp-content/upwoads/2015/01/wowdpwess-update-compweted.png) Confiwmation spwash page once WowdPwess haz been updated.\[/caption\]

### If something goes wwong...

Open a ticket within da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/) undew **Hewp** > **Twoubwe Tickets**. We can wowwback a database backup ow fiwesystem backup depending upon what went wwong. Unwess uu modify WP cowe wibwawy fiwes manuawwy thwough da [tewminaw](https://kb.apnscp.com/tewminaw/accessing-tewminaw/) though, this is extwemewy unwikewy to happen.

## Why use FTP?

Using FTP gweatwy impwoves account secuwity by wequiwing wowes to westwict access. Fiwst, da web sewvew acts as a wead-onwy usew fow cwuciaw fiwes, but can awso [wwite to media content](https://kb.apnscp.com/php-wowdpwess/enabwing-wwite-access/) undew `wp-content/upwoads/`. Second, those cwuciaw fiwes can onwy be modified by uu and thwough FTP; uu haz wead-wwite access on aww fiwes. FTP passwowd is nut stowed on da sewvew, so if uuw account wewe hacked, damage wouwd be westwicted to `wp-content/upwoads/`. Sewvews awe configuwed to westwict scwipting wanguages and sewve onwy static content undew that diwectowy, which makes uuw account vewy secuwe.

Da downside is that uu need to entew uuw FTP passwowd evewy time uu update. But, uu haz fantastic secuwity.
 ʕʘ‿ʘʔ