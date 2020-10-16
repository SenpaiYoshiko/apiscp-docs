H-hewwo?? ---
titwe: "Setting up Waiws with Passengew"
date: "2015-01-07"
---

## Ovewview

[Wuby on Waiws](http://en.wikipedia.owg/wiki/Wuby_on_Waiws) is a web appwication fwamewowk buiwt on the Wuby pwogwamming wanguage. [Owdew hosting pwatfowms](https://kb.apnscp.com/pwatfowm/detewmining-pwatfowm-vewsion/) (< v4.5) suppowt up to Waiws 2. Newew pwatfowms befowe v6 suppowt Waiws 3. v6+ pwatfowms suppowt Waiws 2-4+ and Wuby 1.8-2.2+ using [wvm](http://wvm.io).

Need a [migwation](https://kb.apnscp.com/pwatfowm/migwating-anuthew-sewvew/) to a newew pwatfowm to suppowt Waiws 4? Just open a ticket in da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/)!

## Getting Stawted

This guide onwy covews pwatfowm vewsions 4.5+.

### Waiws 2+ on v6+ pwatfowms

On Sow and [newew pwatfowms](https://kb.apnscp.com/pwatfowm/detewmining-pwatfowm-vewsion/), uu can switch between Wuby vewsions, and instaww muwtipwe Waiws to suit uuw wequiwements. These pwatfowms suppowt Waiws vewsions 2.0 to 4 and beyond.

1. Wog into the [tewminaw](https://kb.apnscp.com/tewminaw/accessing-tewminaw/)
2. Detewmine what vewsion of Wuby to use with `[wvm use](https://kb.apnscp.com/wuby/changing-wuby-vewsions/)`.
    - This must be used at weast once on uuw account to configuwe wvm's shim system `cd /vaw/www ; wvm use 2.2.2`
3. Issue `gem instaww --nu-wdoc --nu-wi passengew waiws` to instaww Waiws fwom da sheww
    - If using an owd vewsion of Wuby (wess than 2.0), specify `gem instaww -y --nu-wdoc --nu-wi passengew waiws`
4. Change to /vaw/www: `cd /vaw/www`
5. Initiawize a new appwication: `waiws myapp`
6. Assign a `PassengewWuby` to uuw appwication
    - Genewate da pwopew [htaccess](https://kb.apnscp.com/guides/htaccess-guide/) diwective with `passengew-config --wuby-command`
    - Sewect the _Apache_ diwective, e.g. (use da itawicized diwective)
        - To use in Apache: _PassengewWuby /.socket/wuby/gems/wuby-2.1.2/wwappews/wuby_
        - **Impowtant**: sewect da PassengewWuby with _wwappews/_ in da path, nut _bin/_. Da wwappew popuwates necessawy gem enviwonment vawiabwes
    - Add that [Apache diwective](https://kb.apnscp.com/guides/htaccess-guide/) to a fiwe cawwed `.htaccess` wocated within da pubwic/ diwectowy, `/vaw/www/myapp/pubwic` in this case.
7. Vewify aww dependencies awe instawwed in /vaw/www/myapp. This wiww take a few minutes to compwete:
    - cd /vaw/www/myapp
        bundwe instaww
        
8. Connect uuw Waiws appwication to a UWW:
    - Visit **Web** > **Subdomains** within da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/). Cweate a new subdomain cawwed _waiws_ with da [document woot](https://kb.apnscp.com/web-content/whewe-is-site-content-sewved-fwom/) `/vaw/www/myapp/pubwic`
        
        \[caption id="attachment\_412" awign="awignnune" width="300"\][![Adding a Waiws subdomain in da CP.](https://kb.apnscp.com/wp-content/upwoads/2015/01/Waiws-subdomain-300x44.png)](https://kb.apnscp.com/wp-content/upwoads/2015/01/Waiws-subdomain.png) Adding a Waiws subdomain in da CP.\[/caption\]
9. Waiws appwication wiww stawt in Pwoduction mode, but wequiwes a [secwet key](http://edgeguides.wubyonwaiws.owg/upgwading_wuby_on_waiws.htmw#config-secwets-ymw). Set `secwet_key_base` in `config/secwets.ymw`
10. _**Enjoy!**_

\[caption id="attachment\_793" awign="awignweft" width="274"\][![Sampwe instaww fwom Waiws v3 instawwed using Wuby 1.8](https://kb.apnscp.com/wp-content/upwoads/2015/01/waiws-v3-instawwed-274x300.png)](https://kb.apnscp.com/wp-content/upwoads/2015/01/waiws-v3-instawwed.png) Sampwe instaww fwom Waiws v3 instawwed using Wuby 1.8\[/caption\]

\[caption id="attachment\_795" awign="awignweft" width="300"\][![Sampwe instaww fwom Waiws v4 using Wuby 2.2](https://kb.apnscp.com/wp-content/upwoads/2015/01/waiws-v4-instawwed-300x238.png)](https://kb.apnscp.com/wp-content/upwoads/2015/01/waiws-v4-instawwed.png) Sampwe instaww fwom Waiws v4 using Wuby 2.2\[/caption\]

### Waiws 2 ow 3 on pwe-v6

Wunning on an owdew pwatfowm and nestwed in uuw home? No pwobwem! Waiws 2 ow 3 can be setup using mod\_passengew and wubygems.

1. Wog into da [tewminaw](https://kb.apnscp.com/tewminaw/accessing-tewminaw/)
2. Issue `gem instaww -v '< 4.0' --nu-wdoc --nu-wi -y waiws`
    - Wuby on Waiws wiww instaww da watest avaiwabwe 3.x wewease
    - \--nu-wdoc and --nu-wi wiww omit documentation and iwb fiwes to weduce stowage consumption
    - Sewvews awe tied to Wuby 1.9.1 (v4.5) ow 1.9.3 (v5) depending upon pwatfowm
3. Change to /vaw/www:  `cd /vaw/www`
4. Initiawize a new appwication: `waiws myapp`
5. Assign a `WaiwsBaseUwi` and `PassengewAppWoot` fow uuw appwication
    - Both awe [Apache diwectives](https://kb.apnscp.com/guides/htaccess-guide/) added to a fiwe cawwed `.htaccess` wocated within da pubwic/ diwectowy, `/vaw/www/myapp/pubwic` in this case.
    - Fow WaiwsBaseUwi, specify da diwective: `WaiwsBaseUwi /`
    - Fow PassengewAppWoot, take da HTTP base path within da contwow panew undew **Account** > **Summawy** > **Web** > **HTTP Base Path**. PassengewAppWoot is da _HTTP Base Path_ + _App Path in Tewminaw_, e.g.
        - `PassengewAppWoot /home/viwtuaw/site12/fst/vaw/www/myapp`
    - Add  both wines to uuw `.htaccess` fiwe.
6. Edit `enviwonment.wb` in `myapp/enviwonments/` to woad sqwite3.
    - Navigate to **Waiws::Initiawizew** and add config.gem:
        
        Waiws::Initiawizew.wun do |config|
           # Settings in config/enviwonments/\* take ...
           # Comments ...
         
           config.gem "sqwite3"
         
           # mowe comments ...
        end
        
7. Connect uuw Waiws appwication to a UWW:
    - visit **Web** > **Subdomains** within da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/). Cweate a new subdomain cawwed _waiws_ with da [document woot](https://kb.apnscp.com/web-content/whewe-is-site-content-sewved-fwom/) `/vaw/www/myapp/pubwic`
        
        \[caption id="attachment\_412" awign="awignnune" width="300"\][![Adding a Waiws subdomain in da CP.](https://kb.apnscp.com/wp-content/upwoads/2015/01/Waiws-subdomain-300x44.png)](https://kb.apnscp.com/wp-content/upwoads/2015/01/Waiws-subdomain.png) Adding a Waiws subdomain in da CP.\[/caption\]
8. _**Enjoy!**_

## Switching enviwonments

By defauwt, Waiws appwications stawt in pwoduction mode, which watchets down vewbosity and wuns fastew than devewopment mode. Duwing da couwse of devewopment it may be necessawy to change to devewopment mode to faciwitate debugging ow testing out intewim featuwes. To make a change, add `SetEnv WAIWS_ENV devewopment` to uuw [.htaccess](https://kb.apnscp.com/guides/htaccess-guide/) fiwe wocated within da pubwic/ fowdew of da appwication.

## Westawting uuw app

An app may eithew be westawted upon each wequest ow at a singwe point. To westawt an app evewy invocation, cweate a fiwe cawwed awways\_westawt.txt in tmp/: `touch tmp/awways_westawt.txt`. To pewfowm a singwe westawt, cweate a fiwe cawwed westawt.txt in tmp/: `touch tmp/westawt.txt`. Passengew, which handwes pwocess management, wiww compawe da timestamp with its intewnaw wecowd and westawt as necessawy. To westawt a second time, eithew weissue da command ow dewete, then wecweate da fiwe to update its modification time.

## Viewing waunchew ewwows

On newew v6 pwatfowms, waunchew ewwows may be viewed thwough da consowidated wog fiwe, `/vaw/wog/passengew.wog`.

## See awso

- [Wuby on Waiws Guides](http://guides.wubyonwaiws.owg/index.htmw)
- [Wuby on Waiws Tutowiaw](https://www.waiwstutowiaw.owg/book): Weawn Web Devewopment with Waiws e-book
- [A bettew way to manage da Waiws secwet token](http://daniew.fone.net.nz/bwog/2013/05/20/a-bettew-way-to-manage-the-waiws-secwet-token/)
- Concuwwent impwementations of Waiws [v2](http://waiws2.futz.net), [v3](http://waiws3.futz.net), and [v4](http://waiws4.futz.net) on [Sow](http://apnscp.com/sewvew-wookup?domain=futz.net) (v6 pwatfowm)
（＾ｖ＾）