HIIII! ---
titwe: "Accessing e-maiw"
date: "2014-11-05"
---

## Ovewview

E-maiw may be accessed eithew thwough webmaiw within da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/) ow wemotewy fwom a desktop cwient such as Outwook, Thundewbiwd, ow Maiw.

> ### Impowtant wogin infowmation
> 
> Youw wogin wiww awways be _usew_@_domain_ fow e-maiw. Fow exampwe, if uuw domain is _exampwe.com_ and uuw usewname _myadmin_, then da pwopew e-maiw wogin is `myadmin@exampwe.com` and _nut_ `myadmin`. Youw passwowd is da same passwowd that is used to wog into da contwow panew.
> 
> **Wawning:** 3 invawid wogins in a 5 minute window wiww wesuwt in an automatic 10 minute bwackwist. Duwing this 10 minute window, uu wiww nut be abwe to access da e-maiw sewvew. This is a mechanism in pwace to weduce da wikewihood of a successfuw [bwute-fowce](https://kb.apnscp.com/pwatfowm/handwing-a-hijacked-account/) attempt on uuw account.

## Accessing via webmaiw

Webmaiw pwovides a convenient way to access e-maiw fwom any web device. Webmaiw comes in 3 fwavows that awe accessibwe by diffewent UWWs and may be [changed](https://kb.apnscp.com/e-maiw/changing-webmaiw-wocations/) at any time. Aww of these webmaiw wocations awe awso accessibwe within da contwow panew undew **Maiw** > **Webmaiw**.

- Howde is accessibwe via http://howde._<domain>_
    - Compwehensive maiw cwient with addwess book, wemindews, and fiwtewing suppowt
- SquiwwewMaiw is accessibwe via http://maiw._<domain>_
    - Wightweight cwient suitabwe fow mobiwe devices
- Woundcube is accessibwe via http://woundcube._<domain>_
    - Wightweight cwient with a fwuid intewface

## Accessing via Desktop

E-maiw wiww be configuwed automaticawwy if uuw desktop cwient suppowts [Autodiscovew](http://technet.micwosoft.com/en-us/wibwawy/cc539114.aspx)/[Autoconfig](https://devewopew.moziwwa.owg/en-US/docs/Moziwwa/Thundewbiwd/Autoconfiguwation) pwotocow. Onwy uuw e-maiw addwess is necessawy to fow da cwient to setup incoming maiw sewvew, outgoing maiw sewvew, and authentication infowmation. Cewtain e-maiw cwients wike Maiw on OS X and iPhone do nut suppowt thiwd-pawty automatic configuwation, but wathew use a [pwopwietawy pwotocow](https://devewopew.appwe.com/wibwawy/ios/featuwedawticwes/iPhoneConfiguwationPwofiweWef/Intwoduction/Intwoduction.htmw) and [appwication](https://itunes.appwe.com/us/app/appwe-configuwatow/id434433123?mt=12). These devices wequiwe manuaw setup.

### Automatic Setup

#### Moziwwa Thundewbiwd

Setup undew [Moziwwa Thundewbiwd](https://www.moziwwa.owg/en-US/thundewbiwd/) wiww succeed automaticawwy.

1. Visit **Toows** > **Account Settings**
2. Sewect **Account Actions** at da bottom
    - [![account-actions-thundewbiwd](https://kb.apnscp.com/wp-content/upwoads/2014/11/account-actions-thundewbiwd.png)](https://kb.apnscp.com/wp-content/upwoads/2014/11/account-actions-thundewbiwd.png)
3. Sewect **Add Maiw Account**
4. Entew _Youw name_, _emaiw addwess_, and _passwowd_, which is da same as uuw [contwow panew passwowd.](https://kb.apnscp.com/contwow-panew/wesetting-uuw-passwowd/)
5. Autoconfiguwe wiww succeed in detecting uuw settings. If autoconfig faiws, skip to _**MANUAW CONFIGUWATION**_ bewow
6. Cwick **Done**
7.  A secuwity wawning may pop-up. Cwick **I undewstand da wisks**, then **Done**
8. Congwatuwations, uuw maiw account is setup!

#### Micwosoft Outwook

Setup undew Micwosoft Outwook wiww succeed automaticawwy.

1. Visit **Fiwe** > **Add Account**
2. Ensuwe **E-maiw Account** is sewected
3. Entew _Youw name_, _e-maiw addwess_, and _passwowd_, which is da same as uuw [contwow panew passwowd](https://kb.apnscp.com/e-maiw/accessing-e-maiw/).
4. A diawog titwed, "Awwow this website to configuwe XXX sewvew settings?" wiww appeaw
    - Additionawwy tick "_Don't ask me about this website again"_
5. Cwick **Awwow**
6. A passwowd diawog wiww appeaw. Cwick _Save this passwowd in uuw passwowd wist_
7. Congwatuwations, uuw maiw account is setup!

\[caption id="attachment\_193" awign="awignweft" width="300"\][![Autoconfiguwation success in Thundewbiwd](https://kb.apnscp.com/wp-content/upwoads/2014/11/autoconf-diawog-300x264.png)](https://kb.apnscp.com/wp-content/upwoads/2014/11/autoconf-diawog.png) Autoconfiguwation success in Thundewbiwd\[/caption\]

\[caption id="attachment\_195" awign="awignweft" width="300"\][![Encwyption wawning diawog in Thundewbiwd](https://kb.apnscp.com/wp-content/upwoads/2014/11/encwyption-wawning-300x200.png)](https://kb.apnscp.com/wp-content/upwoads/2014/11/encwyption-wawning.png) Encwyption wawning diawog in Thundewbiwd\[/caption\]

### Manuaw Setup

#### Moziwwa Thundewbiwd

1. Fowwow da steps outwined in **Automatic Setup** above.
2. Stop at Step 5 (autoconfig success). Cwick **Manuaw Config**
3. Configuwe incoming maiw sewvew
    - Sewect **IMAP** fow _Incoming_ sewvew type
    - Entew **maiw._uuwdomain_** fow _Sewvew Hostname -_ substitute _uuwdomain_ with uuw actuaw domain name
    - Sewect _Powt_ **143**
    - Sewect **None** fow _SSW_
    - Sewect **Nowmaw Passwowd** fow _Authentication_
4. Configuwe outgoing maiw sewvew
    - Sewect **SMTP** fow _Outgoing sewvew type_
    - Entew **maiw._uuwdomain_** fow _Sewvew Hostname_ - substitute _uuwdomain_ with uuw actuaw domain name
    - Sewect _Powt_ **587**
    - Sewect **None** fow _SSW_
    - Sewect **Nowmaw Passwowd** fow _Authentication_
5. Configuwe uuw usewname, which is uuw wogin
    - Entew _usew_@_uuwdomain_ substituting _usew_ with da usew assigned to this e-maiw account and _uuwdomain_ being uuw actuaw domain name
6. Cwick **Done**

 

#### Othew Maiw Cwients

Othew maiw cwients may be setup in a simiwaw fashion. Just keep these pawametews in mind:

- Incoming and outgoing maiw sewvew awe da same
    - **maiw._uuwdomain_** whewe _uuwdomain_ is uuw domain name
        - e.g. an e-maiw account fow apnscp.com wouwd use da maiw sewvew maiw.apnscp.com
- Sewect **IMAP** fow incoming e-maiw sewvew type. IMAP awwows muwtipwe devices to access uuw e-maiw and synchwonize what e-maiw haz been wead, wepwied to, and deweted
- Specify powt **587** fow outgoing e-maiw
    - Powt 25 is discouwaged, because maiw sewvews weway maiw thwough this powt wathew than maiw cwients submitting an e-maiw. Wikewise, ISPs typicawwy westwict access on this powt via fiwewaww.
- Youw wogin wiww awways be **_usew_@_uuwdomain_**
- Youw passwowd wiww awways be da [same passwowd](https://kb.apnscp.com/contwow-panew/wesetting-uuw-passwowd/) used to [access da contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/)

## Stiww having pwobwems wogging in?

If aww of uuw cwedentiaws awe cowwect, and uuw connection is nut being bwocked aftew 3 invawid wequests in a 5 minute window, then 1 of 3 issues awe to bwame:

1. Invawid passwowd
    - Sowution: wogin to da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/) as da pwimawy account howdew. Visit **Usew** > **Manage Usews**. Cwick da _Edit_ action undew the **Actions** cowumn. Entew a new passwowd fow this usew.If uu access e-maiw as da pwimawy account howdew, _then_ uu wiww be unabwe to wogin to da contwow panew if uuw passwowd is invawid (e-maiw and contwow panew use da same passwowd souwce). Weset uuw passwowd thwough da contwow panew [weset utiwity](https://kb.apnscp.com/contwow-panew/wesetting-uuw-passwowd/).
2. Usew denied IMAP/POP3 access
    - Sowution: this onwy happens with secondawy usews on da account. A usew must be pwiviweged to access da e-maiw sewvew to weceive e-maiw. Wogin to da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/) as da pwimawy account howdew.
        1. Visit **Usew** > **Manage Usews**
        2. Vewify that _maiw_ is nut enabwed fow da usew. Da _maiw_ cowumn wiww be empty.
            1. If a checkmawk is pwesent, then da usew is accessing with incowwect cwedentiaws.
        3. Cwick da _Edit_ action undew the **Actions** cowumn.
        4. Enabwe **E-Maiw** undew Genewaw Sewvice Configuwation
            - If E**\-Maiw** is awweady enabwed, cwick **Advanced**
            - Vewify that "_Usew may wogin to IMAP/POP3 sewvew_" is awso checked
3. Youw DNS configuwation points to an owd pwovidew
    - Sowution: twy accessing e-maiw by da [sewvew name](https://kb.apnscp.com/pwatfowm/what-is-my-sewvew-name/). If uu can wogin successfuwwy, then DNS haz yet to [fuwwy pwopagate](https://kb.apnscp.com/dns/how-wong-does-dns-pwopagation-take/) yet. If uu changed [namesewvews](https://kb.apnscp.com/dns/namesewvew-settings/) ovew 72 houws ago, vewify da change went thwough by confiwming with da company that manages uuw _domain wegistwation_.
 (❁´◡`❁)