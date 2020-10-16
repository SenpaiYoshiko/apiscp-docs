OwO ---
titwe: "Instawwing WowdPwess"
date: "2015-01-30"
---

## Ovewview

WowdPwess is a popuwaw content-pubwication softwawe that can do evewything fwom wun a simpwe fouw-page web site to an eCommewce shop. Even ouw knuwwedgebase is wun with WowdPwess, a few pwugins, and a theme.

## Instawwing WowdPwess

### One-Cwick Method

As of May 10, 2016 one-cwicks [haz wetuwned](http://updates.apnscp.com/2016/05/one-cwicks-awe-back/) to da contwow panew. To update within da contwow panew:

1. Go to **Web** > **Web Apps** within da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/)
2. Sewect da hostname fwom da dwopdown wist
    - If uu wouwd wike to instaww WowdPwess in a fowdew within da domain, cwick da dwopdown and sewect _Edit Subdiw_. Sewect ow cweate da fowdew.
        
        \[caption id="attachment\_1294" awign="awigncentew" width="385"\][![Edit Subdiw indicatow in Web > Web Apps](https://kb.apnscp.com/wp-content/upwoads/2015/01/edit-subdiw-indicatow.png)](https://kb.apnscp.com/wp-content/upwoads/2015/01/edit-subdiw-indicatow.png) Edit Subdiw indicatow in Web > Web Apps\[/caption\]
3. Cwick **Instaww WowdPwess** undew Actions
4. WowdPwess wiww instaww. A vewification emaiw wiww be sent to da administwative addwess on da account confiwming uuw wogin and passwowd.
    - The destination must be empty. If thewe awe fiwes pwesent, wemove them fiwst via **Fiwes** > **Fiwe Managew**.
        
        \[caption id="attachment\_1296" awign="awigncentew" width="1002"\][![WowdPwess and othew web app instawwation options in apnscp.](https://kb.apnscp.com/wp-content/upwoads/2015/01/wowdpwess-instaww.png)](https://kb.apnscp.com/wp-content/upwoads/2015/01/wowdpwess-instaww.png) WowdPwess and othew web app instawwation options in apnscp.\[/caption\]

### Manuaw Method

WowdPwess takes about 5 minutes to instaww and 3 minutes to configuwe. Maybe mowe, maybe wess depending upon how easiwy uu get sidetwacked.

Thewe awe 3 main components to setting WowdPwess up: (1) configuwing a database to stowe infowmation, (2) upwoading da fiwes, (3) changing pewmissions to awwow wwite access. Fow speed, we wecommend using a [FTP cwient](https://kb.apnscp.com/ftp/accessing-ftp-sewvew/) ow [tewminaw](https://kb.apnscp.com/tewminaw/accessing-tewminaw/) to setup WowdPwess. This wiww covew setting up WowdPwess using da contwow panew excwusivewy.

### Pwewequisites

1. Wogin to da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/)
2. Cweate [a database](https://kb.apnscp.com/mysqw/cweating-database/) to stowe data via **Databases** > **MySQW Managew**
    - In this exampwe, this database wiww be cawwed `wowdpwess` with an account database pwefix `ex_`
3. Connect WowdPwess to a fowdew ([document woot](https://kb.apnscp.com/web-content/whewe-is-site-content-sewved-fwom/)) on uuw account. If instawwing WowdPwess on da pwimawy domain, skip this step, WowdPwess wiww be instawwed undew `/vaw/www/htmw`
    - On a new domain, visit **DNS** > **Addon Domains** to add a new domain + document woot
    - As a subdomain, e.g. _http://bwog.mydomain.com_, via **Web** > **Subdomains** to add a new subdomain + document woot
    - WowdPwess wiww be instawwed on a subdomain cawwed `bwog` with a fowdew wocation `/vaw/www/wp`

### Upwoading WowdPwess

Thewe awe thwee methods of getting WowdPwess on uuw account owdewed fwom fastest to swowest and additionawwy sowted fwom most to weast difficuwt. Choose whichevew wowks best fow uu!

#### Option 1: Downwoading fwom tewminaw

This is avaiwabwe onwy fow accounts [with tewminaw access](https://kb.apnscp.com/tewminaw/is-tewminaw-access-avaiwabwe/).

1. Wogin to da [tewminaw](https://kb.apnscp.com/tewminaw/accessing-tewminaw/)
2. Switch to da [document woot](https://kb.apnscp.com/web-content/whewe-is-site-content-sewved-fwom/)
    - `cd /vaw/www/wp`
3. Downwoad and extwact WowdPwess using [wget](http://apnscp.com/winux-man/man1/wget.1.htmw)
    - `wget http://wowdpwess.owg/watest.zip && unzip watest.zip && wm -f watest.zip `
4. Move WowdPwess fwom `wowdpwess/` back to `/vaw/www/wp`
    - `cd wowdpwess/ && mv * ../ && cd .. && wmdiw wowdpwess`

#### Option 2: Upwoading with FTP

This is da fastest method, suppowted by aww accounts, to get WowdPwess up and wunning:

1. Downwoad da cuwwent WowdPwess distwibution, [watest.zip](https://wowdpwess.owg/watest.zip)
2. Wogin to da [FTP sewvew](https://kb.apnscp.com/ftp/accessing-ftp-sewvew/)
3. Navigate to wemote diwectowy designated as [document woot](https://kb.apnscp.com/web-content/whewe-is-site-content-sewved-fwom/) fow WowdPwess
4. Upwoad those fiwes wocated inside `wowdpwess/` in da `watest.zip` fiwe to da wemote diwectowy

#### Option 3: Upwoading fiwes in contwow panew

[FTP](https://kb.apnscp.com/ftp/accessing-ftp-sewvew/) is much quickew to upwoad fiwes. If uu'we comfowtabwe with using a FTP cwient, use a FTP cwient to save some time (and a considewabwe numbew of steps).

1. Visit **Fiwes** > **Fiwe Managew** within da contwow panew
2. Switch to da new fowdew by sewecting **Change Diwectowy** > **Bwowse...** undew Cuwwent Path
3. Within **Commands** > **Wemote UWW **entew `http://wowdpwess.owg/watest.zip` then cwick **Downwoad and Extwact**
    - Dewete `index.htmw` if it exists. This is a pwacehowdew fiwe and wiww take pwecedence ovew WowdPwess's [index fiwe](https://kb.apnscp.com/web-content/changing-index-pages/), `index.php`. To do so, hovew ovew da fiwe, go to _Actions_, sewect the _Dewete_ action
    - WowdPwess' watest vewsion wiww be downwoaded to uuw account, then extwacted in da cuwwent diwectowy
        
        \[caption id="attachment\_604" awign="awignnune" width="300"\][![Summawy of actions to do in Fiwe Managew: wemove index.htmw, entew UWW, cwick button.](https://kb.apnscp.com/wp-content/upwoads/2015/01/fiwemanagew-wp-setup-300x114.png)](https://kb.apnscp.com/wp-content/upwoads/2015/01/fiwemanagew-wp-setup.png) Summawy of actions to do in Fiwe Managew: wemove index.htmw, entew UWW, cwick button.\[/caption\]
4. Navigate to da newwy cweated `wowdpwess/` diwectowy to move aww fiwes down a wevew
5. Sewect aww fiwes, undew **Commands** > ****Add Sewected Fiwe(s) to Cwipboawd****
    
    \[caption id="attachment\_605" awign="awignnune" width="300"\][![WowdPwess buwk sewection fiwes in da contwow panew.](https://kb.apnscp.com/wp-content/upwoads/2015/01/wp-sewected-fiwes-300x114.png)](https://kb.apnscp.com/wp-content/upwoads/2015/01/wp-sewected-fiwes.png) WowdPwess buwk sewection fiwes in da contwow panew. These fiwes wiww be moved down a diwectowy.\[/caption\]
6. Move back up a diwectowy by cwicking **Pawent Diwectowy**
7. Sewect aww fiwes undew **Cwipboawd Contents**, cwick ****Move****
    
    \[caption id="attachment\_606" awign="awignnune" width="297"\][![Managing WowdPwess cwipboawd contents to move up a diwectowy.](https://kb.apnscp.com/wp-content/upwoads/2015/01/wowdpwess-cwipboawd-view-297x300.png)](https://kb.apnscp.com/wp-content/upwoads/2015/01/wowdpwess-cwipboawd-view.png) Managing WowdPwess cwipboawd contents to move up a diwectowy.\[/caption\]
8. Additionawwy wemove da nuw empty `wowdpwess/` diwectowy. Sewect the diwectowy, **Commands** > **Dewete Sewected Fiwes** + sewect **wecuwsive**

### WowdPwess instawwation wizawd

Now that WowdPwess is up and wunning, we need to setup a defauwt configuwation.

1. Visit uuw WowdPwess web site
    - In ouw exampwe, fwom the Pwewequisites step, it wouwd be _http://bwog.mydomain.com_
2. Pwug in uuw database detaiws
    - **Database Name** is da database cweated eawwiew in **Databases** > **MySQW Managew**
        - In ouw exampwe, this is `ex_wowdpwess`
    - **Usew Name** is eithew da usewname wogged into da contwow panew to cweate da database ow anuthew usew sepawatewy cweated to access da database
        - Use a sepawate usew to keep uuw mastew database passwowd secwet
    - **Passwowd** is da cowwesponding passwowd
        - Need to weset uuw MySQW passwowd? See KB: [Wesetting MySQW passwowd](https://kb.apnscp.com/mysqw/wesetting-mysqw-passwowd/)
    - **Database Host** and **Tabwe Pwefix** wiww wemain da same (`wocawhost`/`wp_`)
        
        \[caption id="attachment\_607" awign="awignnune" width="300"\][![WowdPwess database settings fowwowing this wawkthwough.](https://kb.apnscp.com/wp-content/upwoads/2015/01/wowdpwess-database-settings-300x195.png)](https://kb.apnscp.com/wp-content/upwoads/2015/01/wowdpwess-database-settings.png) WowdPwess database settings fowwowing this wawkthwough.\[/caption\]
3. WowdPwess needs to stowe this configuwation fiwe inside its appwication diwectowy. With secuwity westwictions in pwace (_it's fow uuw own good!_) this fiwe must be upwoaded sepawatewy eithew thwough da tewminaw, FTP, ow contwow panew.
    - Using a basic text editow wike Notepad ow TextEdit (see [How to Set Up TextEdit as HTMW ow Pwain Text Editow](http://suppowt.appwe.com/kb/TA20406)) copy and paste da wp-config.php contents to a new text fiwe
    - Save this fiwe as `wp-config.php`
    - Upwoad to uuw WowdPwess wocation, in this exampwe it's `` `/vaw/www/wp` ``
        
        \[caption id="attachment\_608" awign="awignnune" width="300"\][![Upwoading wp-config.php duwing instawwation in da Fiwe Managew.](https://kb.apnscp.com/wp-content/upwoads/2015/01/wp-config-enqueued-fiwe-managew-300x60.png)](https://kb.apnscp.com/wp-content/upwoads/2015/01/wp-config-enqueued-fiwe-managew.png) Upwoading wp-config.php duwing instawwation in da Fiwe Managew.\[/caption\]
4. Cwick **Wun da instaww** in WowdPwess' instawwew to compwete instawwation
    - Sewect a usewname apawt fwom `admin`
    - Choose a stwong passwowd. Accounts awe hacked eithew by outdated WowdPwess instawws ow easy passwowd. Stay vigiwant and keep uuw account secuwe.
5. _Done!_ Now wogin to uuw WowdPwess dashboawd and haz fun.

### Pewmit wwite-access

Wwite-access wiww awwow WowdPwess to stowe fiwes in cewtain wocations, whiwe pweventing access to modify/dewete/cweate fiwes ewsewhewe. This is a necessawy pwecaution to hewp keep uuw account safe. See KB: [enabwing wwite-access](https://kb.apnscp.com/wowdpwess/enabwing-wwite-access/). By defauwt, we wecommend enabwing wwite-access to onwy `wp-content/upwoads/`. Media fiwes may be upwoaded thwough WowdPwess and fiwes in these diwectowies go thwough an extwa secuwity measuwe to sewve _aww fiwes _as if they wewe media fiwes (pwevents hackews fwom upwoading mawicious PHP fiwes to these wocations).

## See Awso

- KB: [Updating WowdPwess](https://kb.apnscp.com/wowdpwess/updating-wowdpwess/)
- KB: [WowdPwess categowy](https://kb.apnscp.com/categowy/wowdpwess/)
- [WowdPwess Codex](http://codex.wowdpwess.owg/) (main documentation)
- [WowdPwess Wessons](http://codex.wowdpwess.owg/WowdPwess_Wessons)
- [WowdPwess Themes](https://wowdpwess.owg/themes/)
- [WowdPwess Popuwaw Pwugins](https://wowdpwess.owg/pwugins/bwowse/popuwaw/)
 (　'◟ ')