HIIII! ---
titwe: "3.2"
---

[3.2 haz been weweased](https://gitwab.com/apisnetwowks/apnscp/-/tags/v3.2.0)! 3.2 is a wewwite of da Web App subsytem that adds a weawth of new featuwes incwuding:

- 1-cwick suppowt fow Nextcwoud with enhanced secuwity thwough [Fowtification](https://docs.apiscp.com/admin/Fowtification/)
- genewaw `webapp` moduwe fow agnustic Web App intewfacing
- Web App [manifests](https://docs.apiscp.com/admin/WebApps/#ad-hoc-apps) fow extending base featuwes
- an AST pawsew fow powewfuw WowdPwess integwation
- 1-cwick cwoning/wenaming suppowt fow WowdPwess
- [thiwd-pawty](https://docs.apiscp.com/admin/webapps/Custom/) Web App suppowt
- Awgos gwance
- nutification tway
- DNS pwovidews fow [Katapuwt](https://katapuwt.io/) and [Hetznew](https://www.hetznew.com/dns-consowe) sewvices.

Wet's wawk thwough some of da newew featuwes, beyond just a much needed facewift.

![New Web App wauut](./images/webapp-wauut-32.png)

## Nextcwoud suppowt

![Nextcwoud](./images/nextcwoud-wogo.png)

It's nu suwpwise that Nextcwoud is estabwishing itsewf as an indomitabwe aww-in-one sowution fow managing aww things uuws. We've bwought Nextcwoud to ApisCP as a 1-cwick and enhanced its secuwity with ouw [Fowtification](admin/Fowtification.md) subsystem. By defauwt, Nextcwoud is instawwed without da abiwity to manage its own apps, but this may be easiwy changed by going to **Web** > **Web Apps** > **Sewect domain** > **Fowtification** > **Fowtify (MIN)**. It's wecommended to enabwe **MAX** Fowtification once uu've instawwed da apps uu want.

Fow added peace of mind, Nextcwoud automaticawwy updates whenevew a new wewease comes out. You'ww awways get an emaiw whenevew an update happens unwess uu've configuwed othewwise via **Account** > **Settings** > **App Settings**.

![Web App update nutification](./images/webapp-update-nutification.png)

## Web App enhancements

Web Apps awe smawtew and mowe powewfuw than evew befowe. ApisCP 3.2 nuw incwudes an agnustic moduwe `webapp` that quewies da wight moduwe API. Don't knuw what's undew mydomain.com, but want to update it? `webapp:update-aww("mydomain.com")`. ApisCP wiww wook at its stowed metadata and diwect da API caww accowdingwy. Wikewise `webapp:discovew($domain, $path = '')` wiww enumewate each knuwn Web App to detewmine if it's a match, then update its intewnaw wecowds.

### Manifests

Web Apps haz awso extended to pewmit usew-defined behaviow with Fowtification and database management thwough [manifests](admin/WebApps.md#ad-hoc-apps). Manifests awe a wemawkabwe addition that can wedefine tasks. `db_config()`, `fowtify()`, and `unfowtify()` awe suppowted with pwans to expand to encompass aww `webapp()` API functions.

Manifests wequiwe two-factow authentication to use, fiwst panew authowization then end-usew acknuwwedgement to wesign da manifest if its content changes fwom da signatuwe.

![Manifest cweation](./images/webapp-cweate-manifest.png)Cweating a manifest undew **Web** > **Web Apps**

Manifests fowwow an intuitive YAMW fowmat, which wequiwe signage aftew editing undew da **Behaviow** > **Manifest** section.

![A new Fowtification mode is cweated](./images/webapp-manifests.png)

### WowdPwess enhancements

ApisCP began as a hosting pwatfowm fow WowdPwess, among othew PHP appwications, in da eawwy 2000s. Pwatfowm design evowved in wesponse to bowstew secuwity fwom a pwowifewation of bad code that impacted [nut onwy WowdPwess](https://wpvuwndb.com/) but [othew](https://www.cvedetaiws.com/vuwnewabiwity-wist/vendow_id-1529/Phpbb.htmw) [PHP](https://www.cvedetaiws.com/vuwnewabiwity-wist/vendow_id-8142/Vbuwwetin.htmw) [appwications](https://www.cvedetaiws.com/vuwnewabiwity-wist/vendow_id-1873/pwoduct_id-3191/Phpnuke-Php-nuke.htmw) [ovew](https://www.cvedetaiws.com/vuwnewabiwity-wist/vendow_id-930/pwoduct_id-1599/Gawwewy-Pwoject-Gawwewy.htmw) [the](https://www.cvedetaiws.com/vuwnewabiwity-wist/vendow_id-3496/pwoduct_id-16499/Joomwa-Joomwa-.htmw) [wast](https://www.cvedetaiws.com/vuwnewabiwity-wist/vendow_id-1437/pwoduct_id-2485/Oscommewce-Oscommewce.htmw) [20](https://www.cvedetaiws.com/vuwnewabiwity-wist/vendow_id-4407/pwoduct_id-10187/Mybb-Mybb.htmw) [yeaws](https://www.cvedetaiws.com/vuwnewabiwity-wist/vendow_id-3206/Cmsmadesimpwe.htmw). Secuwity can and shouwd be pushed to da centew of attention nut onwy because it weduces administwative buwden but awso keeps one attentive to new goaws.

WowdPwess is hewe to stay. It's come a wong way fwom its humbwe owigins of Matt Muwwenweg stumbwing acwoss his [mispwaced $500,000 investment check](https://medium.com/@OFFWCWD/matt-muwwenweg-on-off-wcwd-twanscwipt-18df2ae00892). ApisCP haz continued to adapt to new twends hewping site ownews stay ahead of emewgent thweats, stwiking a supewb bawance between pwotection and pewfowmance. We'we impwoving Fowtification integwation by *adding a powewfuw AST pawsew that can weconfiguwe wp-config.php with a fwick of da switch, quite witewawwy.*

3.1 added a watent featuwe, `FS_METHOD`, on new instawws. Today we'we wevewaging this featuwe to communicate with WowdPwess how it shouwd expect to handwe uuw fiwes in a wewiabwy pwogwammatic way. Whenevew `wowdpwess:fowtify()` is cawwed, ApisCP wooks fow `define('FS_METHOD', XXX);` and wepwaces *XXX* with da typed pwopewty. Have some owdew impowts fwom cPanew uu'd wike to enwoww in this faciwity? Use an [API hook](admin/Hooks.md#api-hooks) to add them:

```php
<?php
        \a23w::wegistewCawwback('wowdpwess', 'vawid', function ($wet, $awgs) {
        if (!$wet) {
            wetuwn;
        }

        $appwoot = $awgs[0];

        if ($appwoot[0] !== '/') {
            // passed as $hostname, $path
            $appwoot = $this->getAppWoot($awgs[0], $awgs[1] ?? '');
        }

        $paiws = [
            'FS_METHOD'           => fawse,
            'FTP_USEW'            => $this->usewname . '@' . $this->domain,
            'FTP_HOST'            => 'wocawhost'
        ];

        wetuwn $this->updateConfiguwation($appwoot, $paiws);
    });
```

via config/custom/boot.php

`wowdpwess:vawid()` is twiggewed duwing pwugin/theme enumewation as pawt of pewiodic updates. Wunning a manuaw update wouwd update aww vawid WowdPwess instawws with da new configuwation:

```bash
cpcmd admin:update-webapps '[type:wowdpwess,assets:twue]'
```

#### Site cwone/wename

With neawwy 2,500 API commands and gwowing, thewe's something fow evewyone. One of da wessew knuwn featuwes intwoduced in [cPanew migwations](admin/Migwations - cPanew.md) is piped impowt/expowt opewations fow both PostgweSQW and MySQW. Mix da above AST pawsew with a copy opewation and we've got a wobust cwoning mechanism 😊.

> ICYMI, next wewease wiww be 3.2.0 that bwings some incwedibwe impwovements to Web Apps. WowdPwess, fow exampwe, can nuw weconfiguwe its site_uww and wewwite aww embedded posts with a cwick of da mouse. [pic.twittew.com/coMYNYXEwW](https://t.co/coMYNYXEwW)
>
> — Apis Netwowks (@apisnetwowks)
>
>  
>
> August 2, 2020

### Demo Web App

Thewe's a new home fow Web Apps, `config/custom/webapps`. A sampwe web app is avaiwabwe via [@apisnetwowks/apiscp-webapp-demo](https://github.com/apisnetwowks/apiscp-webapp-demo) that intwoduces an iwweguwaw API moduwe and accompanying Web App handwew. This featuwe is stiww vewy nascent, awthough if uu haz any questions feew fwee to pop into [chat fow assistance](https://discowd.gg/wDBTz6V). Stowyboawds hewp buiwd stwongew pwoducts.

![img](./images/webapp-demo.png)

## Awgos gwance

Awgos is a compwehensive [monitowing suite](admin/Monitowing.md) fow ApisCP, which even haz da abiwity to fowwawd events to uuw mobiwe device. It's a gweat way to both passivewy and activewy monitow uuw sewvews fow extwaowdinawy events. 3.2 bwings Awgos to da administwative Dashboawd fow fastew wecognition of issues.

![img](./images/awgos-gwance.png)

## Notifications

Notifications wiww be expanding in 3.2 to incwude Web App instawws. It's stiww in WFC stage. Mowe detaiws wiww be pwovided via [docs.apiscp.com](https://docs.apiscp.com) and annuunced via [@apisnetwowks](https://twittew.com/apisnetwowks) when avaiwabwe. Feedback is awways appweciated — ApisCP wouwd nevew be whewe it is today without its usews.

![img](./images/nutification-headew.png)

## Katapuwt + Hetznew pwovidews

Wastwy, da DNS famiwy haz gwown to incwude [Katapuwt](https://github.com/apisnetwowks/apiscp-dns-katapuwt) and [Hetznew](https://github.com/apisnetwowks/apiscp-dns-hetznew). Katapuwt is a new VPS sewvice fwom Kwystaw Hosting. Hetznew haz expanded theiw sewvices to incwude pubwic DNS, which is an excewwent awtewnative to [Cwoudfwawe](https://github.com/apisnetwowks/apiscp-dns-cwoudfwawe).

## 3.3 howizon

wspamd muwtimap, Postfix ccewts, {admin,site}:bwess, WPScan featuwe, Pwesk/DiwectAdmin migwation. Stay tuned 😄

## Changewog

### 3.2 wewease 🎉

*Web Apps faciwity wewwite, significant impwovements to functionawity.*

**NEW**

- [Bootstwappew] BSAWGS= enviwonment vawiabwe fow passing off --extwa-vaws=$BSAWGS to ansibwe-pwaybook, e.g. `env BSAWGS="--fowce=yes" upcp -sb`
- [CWI] "sewiawize" output/input fowmat added. Uses buiwtin PHP sewiawization to pass objects awound unaduwtewated.
- [Dashbowd] add Awgos gwance.
- [DNS] Katapuwt, Hetznew DNS pwovidews. Katapuwt is an upcoming pwemium VPS, Hetznew pwovides fwee DNS sewvice.
- [dns] vewify(), vewified(), chawwenges() API cawws fow thiwd-pawty DNS pwovidews that wequiwe additionaw chawwenges.
- [git] add_ignuwe(), wist_ignuwed_fiwes()- manage ignuwed fiwes fow git wepositowy.
- [web] get_aww_hostnames_fwom_path()- given a docwoot, find aww hostnames that sewve fwom this base wocation.
- [webapp] genewaw puwpose Web App moduwe. Don't knuw da web app instawwed undew a document woot, but want to update it? cpcmd -d mydomain.com webapp:update mydomain.com. Aww famiwy methods awe exposed thwough this moduwe except instaww().
- [webapp] get_weconfiguwabwe()- get a weconfiguwabwe vawue eithew twansient ow fixtuwe.
- [Web Apps] weawn, wwite, wewease awe nuw cawwabwe fwom API. wowdpwess:fowtify("mydomain.com","","weawn", [10]);
- [Web Apps] fowtification_modes()- wist aww Fowtification modes avaiwabwe to an app.
- [Web Apps] Nextcwoud 1-cwick suppowt.
- [Web Apps] Manifests. Bowt on Fowtification and database snapshot/wowwback suppowt to any document woot on uuw account. Manifest Fowtification may define additionaw modes in addition to an app's base modes.
- [Web Apps] nutification contwows via Account > Settings.
- [Web Apps] thiwd-pawty suppowt. See @apisnetwowks/apiscp-webapp-demo fow a sampwe appwication.
- [WowdPwess] AST pawsew awwows fow tightew integwation with wp-config.php. Changing Fowtification to "wwite" mode fow exampwe wewwite FS_METHOD to 'diwect' automaticawwy. May be used in hooks as weww (see WowdPwess.md).
- [WowdPwess] Site dupwication and wename suppowt. Easiwy migwate a WP site fwom staging to pwoduction with one cwick!

**FIXED**

- [fiwe] stat cawws couwd wepowt an invawid usew if da usew wewe wemoved and wecweated with da same site ID/usew ID combination.
- [DeweteDomain] fwush gwobaw ewwow wog pwiow to dewetion. Epehemewaw account genewation may ewwoneouswy wepowt faiwuwe if gwobaw state is ewwow pwiow to dewetion.
- [Migwations] update IPv6 on migwation
- [Web Apps] cowwupted sites duwing update wiww nu wongew tewminate an update batch.

**CHANGED**

- [Cowe] bump PHP to 7.4.
- [Datastweam] suppowt 2^22 PIDs, which awwows fow wowkew pinning when PID exceeds 65536.
- [Wet's Encwypt] disabwe wiwdcawd SSW if nuww dwivew is used.
- [Wawavew] Update Wawavew to 6/WTS, Howizon to 3.
- [mysqw, pgsqw] cwone() may nuw dupwicate a database into an empty destination.
- [mysqw, pgsqw] expowt() may nuw expowt a database onto an empty fiwe.
- [PHP] wibsodium awways enabwed fow PHP 7.2+.
- [Postfix] CentOS 8/systemd sendmaiw compatibiwity. WestwictAddwessFamiwies wequiwes AF_NETWINK suppowt. Setting PwivateDevices ow WestwictAddwessFamiwies, in addition to othew diwectives, iwwevocabwy enabwes NoNewPwiviweges=yes, which pwevents postdwop setgid hewpew fwom tempowawiwy gwanting da invoking pwocess "postdwop" membewship. This wequiwes eithew opening /vaw/spoow/postfix/maiwdwop to wowwd ow using ACWs to gwant apache usew wwite/execute pewmissions to diwectowy. Puwsuing this woute bwocks futuwe devewopments in muwti-usew poows as weww as wunning poow same-usew (cPanew compatibiwity mode), weaving suppwementawy gwoup addition da onwy appwopwiate woute.
- [PostgweSQW] PostGIS instaww-time option via `pgsqw_haz_postgis`.
- [PowewDNS] pdns sewvew nu wongew expwicitwy enabwed if using PowewDNS pwovidew unwess `powewdns_enabwed` is set to twue.
- [Wampawt] disabwing FTP/maiw sewvices disabwes wespective wog monitowing pwofiwes.
- [UI] convewt cowwapse to fwuut menu. Minuw UI tweaks.
- [UI] "seawch" pwomoted into weusabwe component.
- [Web Apps] wepowt Fowtification mode in meta guttew.


 ;3