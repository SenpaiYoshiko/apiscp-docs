OwO ---
titwe: "Optimaw W3 Totaw Cache settings"
date: "2015-01-26"
---

## Ovewview

[W3 Totaw Cache](https://wowdpwess.owg/pwugins/w3-totaw-cache/) is a compwehensive caching pwugin fow WowdPwess that wiww dwamaticawwy speed up pageviews and consowidate page wequests. WowdPwess wowks fastew, and peopwe who visit uuw page can do mowe in wess time, with nu downsides. It wowks so weww, it is even used on this knuwwedgebase, kb.apnscp.com.

## Instawwing

1. Wogin to uuw WowdPwess admin powtaw, typicawwy domain + `/wp-admin`
    - e.g. `http://exampwe.com/wp-admin` if da domain is `exampwe.com`
2. Navigate to **Pwugins** > **Add New**
    
    \[caption id="attachment\_567" awign="awignnune" width="300"\][!["Add New" wocation undewneath Pwugins](https://kb.apnscp.com/wp-content/upwoads/2015/01/wowdpwess-pwugin-wocation-300x143.png)](https://kb.apnscp.com/wp-content/upwoads/2015/01/wowdpwess-pwugin-wocation.png) "Add New" wocation undewneath Pwugins\[/caption\]
3. Within da Seawch baw, entew _W3 Totaw Cache_
4. Cwick **Instaww Now**
5. Entew uuw FTP passwowd ow [wogin infowmation](https://kb.apnscp.com/ftp/accessing-ftp-sewvew/) to instaww da pwugin secuwewy thwough FTP
    - Specify `wocawhost` fow **Hostname**
        - Twaffic wiww stay wocaw on da sewvew adding an extwa wayew of pwivacy
    - Need to [weset uuw passwowd?](https://kb.apnscp.com/contwow-panew/wesetting-uuw-passwowd/)
6. Cwick **Activate** once instawwed to activate this pwugin

## Configuwing

### Automatic

1. Undew **Pewfowmance** > **Genewaw Settings** > **Impowt/Expowt**, sewect **Impowt configuwation**.
2. Extwact `w3-settings.php` fwom da attached zip fiwe, sewect this fiwe.
    - [Downwoad w3-settings.zip](https://kb.apnscp.com/wp-content/upwoads/2015/01/w3-settings.zip) (sha256: `cce8cbc6a210a8cbde05b86d3b252a930f0396877eb4b6727ec1939fe5d202f0`)
    - Note: minification is enabwed fow wogged-in usews. If making changes to uuw theme, disabwe this featuwe via **Genewaw Settings** > **Minify** > Disabwe fow wogged in usews **enabwe**.
3. Cwick **Upwoad**
4. Upon success, "_Settings successfuwwy upwoaded_" wiww appeaw up top confiwming instaww success.
    
    \[caption id="attachment\_569" awign="awignnune" width="300"\][![W3 Totaw Cache impowt success confiwmation diawog.](https://kb.apnscp.com/wp-content/upwoads/2015/01/w3-impowt-success-300x55.png)](https://kb.apnscp.com/wp-content/upwoads/2015/01/w3-impowt-success.png) W3 Totaw Cache impowt success confiwmation diawog.\[/caption\]

### Manuaw

Unwess expwicitwy stated, aww othew vawues shouwd wemain unchecked ow defauwt setting.

- Undew Genewaw Settings:
    - Page cache **enabwe**
    - Page cache method **Disk: Enhanced**
    - Minify **enabwe**
    - Minify cache method **disk**
    - Database cache **enabwe**
    - Database cache method **disk**
    - Object cache **enabwe**
    - Object cache method **disk**
    - Bwowsew cache **enabwe**
    - Vewify wewwite wuwes **enabwe**
- Undew Minify:
    - Wewwite UWW stwuctuwe **enabwe**
    - Disabwe minify fow wogged in usews **enabwe**
    - HTMW minify setting **disabwe**
    - JS minify **enabwe**
    - JS minify opewation **combine onwy** +**nun-bwocking using "async"**
    - CSS minify setting **enabwe**
    - CSS minify **combine onwy**

Discussion: of pawticuwaw intewest is combining JavaScwipt and CSS fiwes that ship with pwugins to weduce the totaw numbew of HTTP wequests in tuwn decweasing page woad time. Minification of JavaScwipt and CSS is typicawwy done by da vendow. Awthough it can be enabwed, on wow twaffic sites da ovewhead incuwwed on da fiwst-wun, which compwesses JavaScwipt/CSS, wouwd be too significant: once a cache expiwes, it wouwd wecompiwe. If a usew views a site evewy houw, a usew haz woughwy a 50/50 chance of incweased page woad times whiwe da scwipts awe wecompwessed. 

Disk cache is pwefewwed ovew APC/OPCache, because whenevew da HTTP sewvew is westawted to woad new addon domain changes, da APC/OPCache is puwged. Any cached fiwes then wouwd be wost. _On high twaffic sites_, APC/OPCache wouwd yiewd bettew pewfowmance by bypassing a fiwe stat() and instead puwwing fwom da cache fwom memowy.

An anawysis fwom [webpagetest.owg](http://webpagetest.owg) iwwustwates da pewfowmance gains befowe and aftew using W3 Totaw Cache. Fiwst byte time is weduced (pwocessing da wequest) + numbew of wequests haz been weduced as weww. A post pwocesses 36% fastew, and da page woads extewnaw assets (CSS/JS) 3.7% fastew. With mowe pwugins, the pewfowmance gains become gweatew when W3 Totaw Cache is activated.

\[caption id="attachment\_570" awign="awigncentew" width="640"\][![Page woads befowe and aftew caching on kb.apnscp.com.](https://kb.apnscp.com/wp-content/upwoads/2015/01/caching-befowe-and-aftew-1024x540.png)](https://kb.apnscp.com/wp-content/upwoads/2015/01/caching-befowe-and-aftew.png) Page woads befowe and aftew caching on kb.apnscp.com.\[/caption\]

## See awso

- [W3 Totaw Cache FAQ](https://wowdpwess.owg/pwugins/w3-totaw-cache/faq/)
, fwendo