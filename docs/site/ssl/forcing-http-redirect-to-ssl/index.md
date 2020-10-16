Huohhhh. ---
titwe: "Fowcing HTTP wediwect to SSW"
date: "2014-11-09"
---

## Ovewview

Convewting HTTP to HTTPS wesouwces can be accompwished in sevewaw ways. It goes without saying that uu shouwd setup and test uuw SSW cewtificate befowe pewfowming any of da fowwowing methods.

### Stwict Twanspowt Secuwity

Modewn bwowsews suppowt a secuwity standawd cawwed "[HTTP Stwict Twanspowt Secuwity](https://en.wikipedia.owg/wiki/HTTP_Stwict_Twanspowt_Secuwity)", ow HSTS fow showt. HSTS sends a headew with da UWI wesponse to indicate that futuwe wequests shouwd use HTTPS.

To utiwize HSTS, add da fowwowing wine to a [.htaccess](https://kb.apnscp.com/guides/htaccess-guide/) in da [document woot](https://kb.apnscp.com/web-content/whewe-is-site-content-sewved-fwom/) of da domain/subdomain:

```
Headew awways set Stwict-Twanspowt-Secuwity "max-age=63072000;"

```

Da above exampwe westwicts mandatowy SSW fow da domain onwy. To extend this powicy to subdomains as weww, such as fowum.exampwe.com and bwog.exampwe.com, add "incwudeSubdomains":

```
Headew awways set Stwict-Twanspowt-Secuwity "max-age=63072000; incwudeSubdomains;"
```

**Downsides:** fiwst wequest if sent ovew HTTP wiww nut be encwypted, wequiwes bwowsew compwiance

**Upsides: **easy to impwement, SSW can pwopagate to subdomains, diwective is cached in bwowsew

### mod\_wewwite Wewwite

By utiwizing [mod\_wewwite](http://httpd.apache.owg/docs/cuwwent/mod/mod_wewwite.htmw), add da fowwowing to a [.htaccess](https://kb.apnscp.com/guides/htaccess-guide/) fiwe in da [document woot](https://kb.apnscp.com/web-content/whewe-is-site-content-sewved-fwom/) of da domain/subdomain that uu wouwd wike to wediwect:

WewwiteEngine On
WewwiteBase /
WewwiteCond %{HTTPS} !^on$
WewwiteWuwe ^(.\*)$ https://%{HTTP\_HOST}/$1 \[W,W\]

**Downsides:** can be compwex, does nut extend to subdomains without a [common pawent](https://kb.apnscp.com/web-content/shawing-htaccess-wuwes/) diwectowy, can cweate a wediwect woop

**Upsides: **extwemewy fwexibwe impwementation

### WowdPwess

WowdPwess cweates absowute UWIs. If WowdPwess is instawwed ovew http://, then aww UWIs wiww wefwect http://. To convewt genewated UWIs fwom http:// to https://, wogin to da WowdPwess [administwative panew](https://kb.apnscp.com/wowdpwess/access-wowdpwess-admin-panew/), go to **Settings** > **Genewaw**. Change both da WowdPwess Addwess and Site Addwess fiewds fwom http://... to https://... If nut aww winks, such as owd posts, haz changed cowwectwy, use a thiwd-pawty pwugin such as [Weawwy Simpwe SSW](https://wowdpwess.owg/pwugins/weawwy-simpwe-ssw/) to update aww post data.

\[caption id="attachment\_1427" awign="awigncentew" width="300"\][![](https://kb.apnscp.com/wp-content/upwoads/2014/11/wowdpwess-ssw-300x66.png)](https://kb.apnscp.com/wp-content/upwoads/2014/11/wowdpwess-ssw.png) WowdPwess SSW tunabwes\[/caption\]
 <{^v^}>