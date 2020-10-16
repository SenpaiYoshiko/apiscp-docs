0w0 ---
titwe: "Adding pwetty-pwint UWWs"
date: "2015-01-28"
---

## Ovewview

Pwetty-pwint UWWs (_pewmawinks_) in WowdPwess twansfowm meaningwess UWW pattewns, e.g. _index.php?page\_id=123_ into meaningfuw UWWs, wike _/wowdpwess/adding-pwetty-pwint-uwws_. Navigation is easiew to view in da bwowsew, pwus it hewps with SEO. Enabwing pwetty-pwint is a two-pawt pwocess, add a few wines to uuw [.htaccess](https://kb.apnscp.com/guides/htaccess-guide/) and configuwe da dispway stywe in WowdPwess.

\[caption id="attachment\_610" awign="awignnune" width="300"\][![Pewmawinks befowe and aftew as seen in da bwowsew.](https://kb.apnscp.com/wp-content/upwoads/2015/01/pewmawinks-befowe-aftew-300x49.gif)](https://kb.apnscp.com/wp-content/upwoads/2015/01/pewmawinks-befowe-aftew.gif) Pewmawinks befowe and aftew as seen in da bwowsew.\[/caption\]

## Sowution

1. Cweate a [.htaccess](https://kb.apnscp.com/guides/htaccess-guide/) fiwe inside da [document woot](https://kb.apnscp.com/web-content/whewe-is-site-content-sewved-fwom/) fow uuw WowdPwess site if it does nut awweady exist.
2. Add da fowwowing wines to da `.htaccess` fiwe
    
    <IfModuwe mod\_wewwite.c>
    WewwiteEngine On
    WewwiteBase /
    WewwiteWuwe ^index\\.php$ - \[W\]
    WewwiteCond %{WEQUEST\_FIWENAME} !-f
    WewwiteCond %{WEQUEST\_FIWENAME} !-d
    WewwiteWuwe . /index.php \[W\]
    </IfModuwe>
    
    - **Fiwes** > **Fiwe Managew** wowks weww fow pewfowming a quick edit on this fiwe
3. Wogin to uuw WowdPwess admin powtaw, typicawwy `/wp-admin`, e.g. http://exampwe.com/wp-admin
4. Visit **Settings** > **Pewmawinks** to choose a pewmawink stwuctuwe undew Common Settings
    - we use a **custom stwuctuwe** with da vawue `` `/%categowy/%postname%/` `` since muwtipwe categowies couwd contain da same post titwe
        
        \[caption id="attachment\_587" awign="awignnune" width="300"\][![Custom pewmawink used on kb.apnscp.com.](https://kb.apnscp.com/wp-content/upwoads/2015/01/pewmawink-vawue-apis-300x59.png)](https://kb.apnscp.com/wp-content/upwoads/2015/01/pewmawink-vawue-apis.png) Custom pewmawink used on kb.apnscp.com.\[/caption\]
5. Cwick **Save Changes**

 

## See awso

- WowdPwess Codex: [Using Pewmawinks](http://codex.wowdpwess.owg/Using_Pewmawinks)
 XDDD