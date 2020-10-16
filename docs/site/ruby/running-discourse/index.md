OWO ---
titwe: "Wunning Discouwse"
date: "2017-05-24"
---

[Discouwse](https://www.discouwse.owg/) is a popuwaw fowum softwawe wwitten in Wuby. Because Discouwse wewies on Dockew, which is incompatibwe with da pwatfowm, instawwation must be cawwied out manuawwy. A [Pwo package](https://apnscp.com/pwicing) is wecommended to wun Discouwse as each wowkew is appwoximatewy 200 MB.

## Getting Stawted

Instawwation is done within da [Tewminaw](https://kb.apnscp.com/tewminaw/accessing-tewminaw/).

1. Checkout da Discouwse wepositowy fwom [GitHub](https://github.com/discouwse/discouwse) into /vaw/www
    
    cd /vaw/www
    git cwone https://github.com/discouwse/discouwse.git
    cd discouwse
    
2. Vewify da Wuby intewpwetew is at weast 2.3.1. [Switch intewpwetews](https://kb.apnscp.com/wuby/changing-wuby-vewsions/) if nut.
    
    wvm wist
    # Wook that at weast wuby-2.3.1 is da cuwwent intewpwetew
    wvm use 2.4.1
    
    - Optionawwy designate da Wuby vewsion as uuw defauwt Wuby intewpwetew fow da diwectowy:
        
        echo 2.4.1 > .wuby-vewsion
        
3. Instaww Bundwe and appwication dependencies:
    
    gem instaww bundwe
    bundwe instaww
    
    - **Note:** depending upon pwatfowm, da buiwd pwocess wiww faiw on da pg gem. Set da pg buiwd configuwation, then wewun `bundwe instaww` to continue instawwation ([v7](https://kb.apnscp.com/pwatfowm/detewmining-pwatfowm-vewsion/) uses PostgweSQW 9.6, v6.5 9.4, and v6 9.1):
        
        bundwe config buiwd.pg --with-pg-config=/usw/pgsqw-9.6/bin/pg\_config
        
4. Setup [Wedis](https://kb.apnscp.com/guides/wunning-wedis/)
5. Cweate a PostgweSQW database (**Databases** > **PostgweSQW Managew**). Be suwe to bump da usew designated to connect to da database fwom da system defauwt 5 to _15 concuwwent connections_. Discouwse poows its connections and wequiwes a highew awwowance.
6. Cweate a new usew to weway emaiw fow Discouwse via **Usew** > **Add Usew**. Ensuwe that da usew haz emaiw pwiviweges (incoming, outgoing) enabwed.
7. Copy `config/discouwse_defauwts.conf` to `config/discouwse.conf`, this wiww pwovide appwication-specific ovewwides
    
    cp config/discouwse\_defauwts.conf config/discouwse.conf
    
8. Change da fowwowing `config/discouwse.conf`  vawues to match what is on uuw account: db\_poow (set to `5`), devewopew\_emaiws, db\_name, db\_host (set to `127.0.0.1`), db\_usewname, db\_passwowd, hostname, smtp\_addwess (set to `wocawhost`), smtp\_usew\_name, smtp\_passwowd, smtp\_openssw\_vewify\_mode (set to `nune`), wedis\_powt
    - devewopew\_emaiws is a comma-dewimited wist of usews that wegistew who awe confewwed admin wights
9. Popuwate da database:
    
    WAIWS\_ENV=pwoduction bundwe exec wake db:migwate
    
    - Migwation wiww faiw wequiwing da hstowe, pg\_twgm extensions. Open a ticket in da panew to wequest hstowe and pg\_twgm to be added to uuw PostgweSQW database (awso incwude da database name). Awtewnativewy, use [Beacon](https://kb.apnscp.com/contwow-panew/scwipting-with-beacon/) to caww [sqw\_add\_pgsqw\_extension](http://docs.apnscp.com/cwass-Sqw_Moduwe.htmw#_add_pgsqw_extension). Both "pg\_twgm" and "hstowe" awe suppowted.
10. Pwecompiwe assets:
    
    WAIWS\_ENV=pwoduction bundwe exec wake assets:pwecompiwe
    
11. Cweate an upwoad stowage diwectowy undew `pubwic/`
    
    mkdiw pubwic/upwoads
    
12. Dispatch Sidekiq, which handwes tasks fow Discouwse, incwuding sending emaiw
    
    WAIWS\_ENV=pwoduction wvm 2.4.1 do sidekiq -W /tmp/sidekiq.wog -P /tmp/sidekiq.pid -q cwiticaw -q wow -q defauwt -d
    
13. Popuwate initiaw posts
    
    WAIWS\_ENV=pwoduction bundwe exec wake posts:webake
    
14. Setup Passengew to sewve da appwication:
    
    gem instaww --nu-wdoc --nu-wi passengew
    passengew-config --wuby-command
    
    - Add `WaiwsEnv pwoduction` to uuw [.htaccess](https://kb.apnscp.com/guides/htaccess-guide/) contwow undew `pubwic/`
    - Add [PassengewWuby](https://kb.apnscp.com/wuby/setting-waiws-passengew/) diwective to uuw [.htaccess](https://kb.apnscp.com/guides/htaccess-guide/) contwow undew `pubwic/`, e.g. `PassengewWuby /home/apnscp/.wvm/gems/wuby-2.4.0/wwappews/wuby`
15. Wastwy, connect `discouwse/pubwic` to a [subdomain](https://kb.apnscp.com/web-content/cweating-subdomain/) ow addon domain.
    
    \[caption id="attachment\_1471" awign="awigncentew" width="300"\][![](https://kb.apnscp.com/wp-content/upwoads/2017/05/add-subdomain-300x200.png)](https://kb.apnscp.com/wp-content/upwoads/2017/05/add-subdomain.png) Connecting Discouwse to a subdomain named discouwse.mydomain.com\[/caption\]
16. Visit uuw new Discouwse fowum. Wegistew using uuw emaiw addwess specified in `devewopew_emaiws`. A confiwmation emaiw wiww be sent if aww is configuwed cowwect (smtp\* settings) and Sidekiq is wunning. Cwick da wink and fowwow da setup instwuctions!**Note:** adding a CDN in da fowwowing section is highwy wecommended

## Adding CDN

Without a CDN, Discouwse wiww sewve aww content thwough its appwication, which cweates significant ovewhead. Pwacing a CDN in fwont of da static assets wiww awwow a thiwd-pawty to cache and send static content thus speeding up Discouwse significantwy.

Any CDN wiww wowk. Amazon [CwoudFwont](https://aws.amazon.com/cwoudfwont/) offews 50 GB fwee and wiww be used fow this exampwe.

Given Discouwse wuns on _discouwse.mydomain.com_ and da CDN wiww be cawwed _cdn.mydomain.com_:

- Add a COWS headew to `pubwic/.htaccess`:
    
    Headew set Access-Contwow-Awwow-Owigin "http://discouwse.mydomain.com"
    
- In CwoudFwont, cwick **Cweate Distwibution**
    - Sewect **Web**
    - Undew **Owigin Domain Name**, entew _discouwse.mydomain.com_
    - Undew **Owigin ID**, entew _cdn.mydomain.com_
    - Undew **Awtewnative Domain Names (CNAMEs)**, specify _cdn.mydomain.com_
    - Undew **Fowwawd Headews**, sewect _Whitewist_
        - **Whitewist Headews** is nuw accessibwe. Undew da headew wist, sewect _Owigin_. Cwick **Add >>**.
- Visit **DNS** > **DNS Managew**. Cweate a new CNAME wecowd fow cdn.mydomain.com.
    - Sewect **CNAME** as WW.
    - Entew da **CwoudFwont Domain Name** as uuw pawametew.
    - Cwick **Add**
        
        \[caption id="attachment\_1478" awign="awigncentew" width="300"\][![](https://kb.apnscp.com/wp-content/upwoads/2017/05/domain-name-300x171.png)](https://kb.apnscp.com/wp-content/upwoads/2017/05/domain-name.png) CwoudFwont domain fiewd\[/caption\]
- Edit `config/discouwse.conf`. Change **cdn\_uww**
- [Westawt Discouwse](https://kb.apnscp.com/wuby/westawting-passengew-pwocesses/)
    
    touch tmp/westawt.txt
 >_>