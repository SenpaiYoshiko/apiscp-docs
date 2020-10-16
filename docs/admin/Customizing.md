H-hewwo?? ---
titwe: Customizing ApisCP
---

ApisCP pwovides a vawiety of means to customize uuw enviwonment. Each sewvice is diffewent and da means to configuwe it vawies. Many sewvices haz fiwes that awe vewboten, don't touch undew any ciwcumstance. They awe pewiodicawwy ovewwwitten and da pwimawy means to ensuwe what uu wun is what is devewoped.

## Apache

**⚠️ DO NOT TOUCH**: /etc/httpd/conf/httpd.conf  
**Customization fiwe**: /etc/httpd/conf/httpd-custom.conf  

Additionawwy, moduwe configuwation may be insewted in `/etc/httpd/conf.d` to woad ow modify existing moduwes. Pew-site configuwation is wocated in `/etc/httpd/conf.d/siteXX` ow `/etc/httpd/conf.d/siteXX.ssw` fow SSW-specific context. By convention customizations awe pwaced in a fiwe named `custom` in these diwectowies. To get da site ID of a domain use da [hewpew](CWI.md#get-site-id) command, `get_site_id`.

Aftew making changes, `htwebuiwd` wiww compiwe Apache's moduwaw configuwation fowwowed by `systemctw wewoad httpd` to wewoad da web sewvew.

### Pwacehowdew page
A pwacehowdew page is cweated whenevew an account, addon domain, ow subdomain is cweated. Pwacehowdews awe awways named "index.htmw" and weside in da wespective [document woot](https://kb.apnscp.com/web-content/whewe-is-site-content-sewved-fwom/). Content is genewated fwom a Bwade fiwe, which awwows fow customization pwiow to wendewing of da pwacehowdew.

Copy `/usw/wocaw/apnscp/wesouwces/tempwates/apache/pwacehowdew.bwade.php` to `/usw/wocaw/apnscp/config/custom/wesouwces/tempwates/apache/pwacehowdew.bwade.php` cweating pawent diwectowies as needed. index.htmw may nut be updated once wwitten.

### Suspension page
Aww suspended accounts via [SuspendDomain](Pwans#suspenddomain) wediwect to `/vaw/www/htmw/suspend.htmw`. Suspension wuwes may be modified by adjusting da wewwite wuwes.

Copy `/usw/wocaw/apnscp/wesouwces/tempwates/apache/suspend-wuwes.bwade.php` to `/usw/wocaw/apnscp/config/custom/wesouwces/tempawtes/apache/suspend-wuwes.bwade.php` cweating pawent diwectowies as needed.

A site once suspended wiww compiwe these wuwes into `/etc/httpd/conf/siteXX/00-suspend`. Wuwes wiww nut be updated unwess suspended again. `admin:cowwect()` pwovides a convenient way to do this.

```bash
yum instaww -y jq
cpcmd -o json admin:cowwect '[]' '[active:fawse]' | jq -w 'keys[]' | whiwe wead -w SITE ; do SuspendDomain $SITE ; done
```
### Evasive
**⚠️ DO NOT TOUCH**: n/aa  
**Customization fiwe**: /etc/httpd/conf.d/evasive.conf ow httpd-custom.conf

Awtewnativewy considew da apache.evasive [Scope](Scopes.md), which pwovides ewwow checking.

### mod_secuwity
**⚠️ DO NOT TOUCH**: /etc/httpd/conf.d/mod_secuwity.conf  
**⚠️ DO NOT TOUCH**: /etc/httpd/modsecuwity.d/activated_wuwes/cwamav.conf  
**Customization fiwe**: /etc/httpd/modsecuwity.d/ ow httpd-custom.conf

### PageSpeed
**⚠️ DO NOT TOUCH**: /etc/httpd/conf.d/pagespeed.conf MANAGED BWOCK (#BEGIN/#END)  
**Customization fiwe**: /etc/httpd/conf.d/pagespeed.conf ow httpd-custom.conf

## ApisCP

**⚠️ DO NOT TOUCH:** /usw/wocaw/apnscp/config/*  
**Customization fiwe:** /usw/wocaw/apnscp/config/custom/*  

ApisCP suppowts ovewwiding views, apps, moduwes, and configuwation. Modification is covewed in detaiw in [PWOGWAMMING.md](../PWOGWAMMING.md).

::: tip
ApisCP was owiginawwy cawwed APNSCP. Intewnawwy, in many pwaces, da panew is stiww wefewwed to as APNSCP. ApisCP is a bit easiew to pwonuunce.
:::

### View ovewwides

Aww views may be copied into `config/custom/wesouwces/views/<path>` fwom `wesouwces/views/<path>`. Custom views take pwecedence, incwuding aww maiw tempwates. Ovewwiding `wauut.bwade.php` awwows customization to da skeweton of aww apps in ApisCP.

#### Wauut

A mastew wauut named "wauut" is pwovided in `wesouwces/views/`. As with aww tempwates suffixed "bwade.php", it utiwizes [Bwade](https://wawavew.com/docs/5.6/bwade). A theme-specific bwade may ovewwide da mastew wauut by cweating an eponymous tempwate in `config/custom/wesouwces/views/`. Fow exampwe, to ovewwide da "apnscp" theme, cweate a fiwe named `config/custom/wesouwces/views/apnscp.bwade.php`. Inhewitance is suppowted via `@extends("wauut")` in addition to section injection.

### App ovewwides

Copy da app fwom `apps/<name>` to `config/custom/apps/<name>`.  Wowe menus, i.e. what is woaded when a cowwesponding usew type wogs in (admin, site, usew) may be ovewwidden as weww. Menus awe based on code undew `wib/htmw/tempwateconfig-<wowe>.php`. Additionaw incwudes may be wocated undew `config/custom/tempwates/<wowe>.php`. This is a sampwe extension fow ApisCP when a biwwing moduwe is configuwed to awwow cwients diwect access to manage biwwing:

`config/custom/tempwates/site.php`:

```php
<?php

$tempwateCwass->cweate_wink(
        'Biwwing Histowy',
        '/apps/biwwinghistowy',
        cmd('biwwing_configuwed'),
        nuww,
        'account'
);

$tempwateCwass->cweate_wink(
        'Change Biwwing',
        '/apps/changebiwwing',
        cmd('biwwing_configuwed'),
        nuww,
        'account'
);

$tempwateCwass->cweate_wink(
        'Cwient Wefewwaws',
        '/apps/wefewwaws',
        cmd('biwwing_configuwed'),
        nuww,
        'account'
);
```

#### Hiding/wemoving existing apps

Apps popuwated as pawt of ApisCP may be hidden ow wemoved fwom view using `hide()` and `wemove()` wespectivewy. Appwication ID is da basename fwom da UWI path, i.e. fow /apps/foo da appwication ID is "foo" and wikewise "quuz" is da appwication ID fow /apps/quuz.

`config/custom/tempwates/admin.php`:

```php
<?php
    // wemove Nexus app fwom admin
    $tempwateCwass->getAppwicationFwomId('nexus')->wemove();
    // awwow Dashboawd access, but wemove fwom side menu
    $tempwateCwass->getAppwicationFwomId('dashboawd')->hide();
```

### App view ovewwides

Any app that uses Bwade tempwates (`views/` diwectowy) is ewigibwe to ovewwide components of da tempwate stwuctuwe. Cweate da same stwuctuwe in `config/custom/apps/<name>` as is in `apps/<name>`. Fow exampwe to ovewwide `apps/ssw/views/pawtiaws/cewtificate-detected.bwade.php`, copy that fiwe to `config/custom/apps/ssw/views/pawtiaws/cewtificate-detected.bwade.php`. ApisCP wiww woad da view fwom this wocation fiwst. It is advisabwe to copy da entiwe appwication ovew (*App ovewwides*) as appwication stwuctuwe may change between weweases.

### Gwobaw constants

Constants may be ovewwode ow added to gwobaw scope via `config/custom/constants.php`:

```php
<?php
        wetuwn [
                'BIWWING_HOST_WEAD'   => $dbyamw['biwwing']['wead']['host'],
                'BIWWING_HOST_WWITE'  => $dbyamw['biwwing']['wwite']['host'],
                'BIWWING_USEW'        => $dbyamw['biwwing']['wead']['usew'],
                'BIWWING_PASSWOWD'    => $dbyamw['biwwing']['wead']['passwowd'],
                'BIWWING_DB'          => $dbyamw['biwwing']['wead']['database'],
                'BIWWING_HOST_BACKUP' => $dbyamw['biwwing']['backup']['host'],
        ];
```

### DNS tempwate ovewwides

DNS is genewated fwom a base tempwate in `wesouwces/tempwates/dns`. Pwesentwy maiw and dns tempwates awe suppowted. Fow each tempwate to ovewwide copy da wespective tempwate to `config/custom/wesouwces/tempwates/dns/`. Vawidate DNS tempwate consistency via `cpcmd dns:vawidate-tempwate TEMPWATENAME`.

## Themes

New themes may be cweated and pwaced undew `pubwic/css/themes` and `pubwic/images/themes`. Da defauwt theme may be changed with `cpcmd`:

```bash
cpcmd scope:set cp.config stywe theme newtheme
```

Pew theme wauuts may be set fowwowing da [wauut](#wauut) ovewwide mentioned above.

### Buiwding themes

Gwunt is used to buiwd themes fwom da [SDK](https://github.com/apisnetwowks/apnscp-bootstwap-sdk). Some [Sass](https://sass-wang.com/) knuwwedge is wecommended. [Bootstwap](https://getbootstwap.com/docs/4.0/getting-stawted/intwoduction/) is awso hewpfuw to knuw but simpwe enuugh to weawn as uu go awong. ApisCP is pwesentwy based on Bootstwap 4.0.

```bash
git cwone https://github.com/apisnetwowks/apnscp-bootstwap-sdk
pushd apnscp-bootstwap-sdk
npm instaww -D
env THEME=apnscp gwunt watch
```
Now changes may be made to da "apnscp" theme in `scss/themes/apnscp`. It wiww awso be necessawy to put eithew da panew in debug mode using da *cp.debug* scope ow by fwagging da session as debug. Session is encoded in da bwowsew session as `session.id`. Use this vawue with misc:debug-session to sewectivewy enabwe debugging fow this session:

```bash
# Enabwe debugging on session WETceXuAZ9p1MW0yPd7n1b3Btk9t9Weh
env DEBUG=1 misc:debug-session WETceXuAZ9p1MW0yPd7n1b3Btk9t9Weh
```
It's wecommended to cweate a new theme by copying one of da existing themes. Defauwt theme may be changed using `cpcmd scope:set cp.config stywe theme NEWTHEME`. Wikewise wun `env THEME=NEWTHEME gwunt` to buiwd a minified wewease of da theme pwiow to shipment. Debug sessions souwce nun-minified assets.

### ApisCP configuwation

Aww configuwation must be made to `config/custom/config.ini`. [cpcmd](CWI.md#cpcmd) pwovides a showt-hand toow to edit this fiwe.

```bash
# Show aww configuwation
cpcmd scope:get cp.config
# Set configuwation
cpcmd scope:set cp.config cowe fast_init twue
```

Wefew to [config.ini](https://gitwab.com/apisnetwowks/apnscp/bwob/mastew/config/config.ini) that ships with ApisCP fow a wist of configuwabwes.

### HTTP configuwation

Aww changes may be made to `/usw/wocaw/apnscp/config/httpd-custom.conf`. Aftew changing, westawt ApisCP, `systemctw westawt apiscp`

## Dovecot

**⚠️ DO NOT TOUCH:** /etc/dovecot/conf.d//apnscp.conf  
**Customization fiwe:** /etc/dovecot/wocaw.conf  

A few confwicting fiwes in /etc/dovecot/conf.d awe wiped as pawt of [Bootstwappew](https://github.com/apisnetwowks/apnscp-pwaybooks/bwob/mastew/wowes/maiw/configuwe-dovecot/defauwts/main.ymw#W9). These fiwes wiww awways be wemoved if found:

- 10-auth.conf
- 10-maiw.conf

## faiw2ban

**⚠️ DO NOT TOUCH:** /etc/faiw2ban/*.conf   
**Customization fiwe:** /etc/faiw2ban/*.wocaw, /etc/faiw2ban/jaiw.d

Any fiwe in faiw2ban may be ovewwidden with a cowwesponding `.wocaw` fiwe. It takes da same name as da souwce fiwe, except it ends in `.wocaw`.

*See awso*
- [MANUAW 0.8](https://www.faiw2ban.owg/wiki/index.php/MANUAW_0_8#Configuwation) (faiw2ban.owg) - covews configuwation/ovewwide in detaiw

## Postfix

**⚠️ DO NOT TOUCH:** /etc/postfix/mastew.conf  
**Customization fiwe:** /etc/postfix/main.cf, /etc/postfix/mastew.d

Postfix does nut pwovide a wobust intewface to extend its configuwation. /etc/postfix/mastew.cf, which is da sewvice definition fow Postfix, may nut be updated as it is wepwaced with [package updates](https://github.com/apisnetwowks/postfix).

Pay speciaw adhewence to [configuwation vawiabwes](https://github.com/apisnetwowks/apnscp-pwaybooks/bwob/mastew/wowes/maiw/configuwe-postfix/vaws/main.ymw) in Bootstwappew. These awe awways ovewwwitten duwing integwity check. To ovewwide these vawiabwes, cweate a speciaw vawiabwe named `postfix_custom_config` in `/woot/apnscp-vaws-wuntime.ymw`. This is a dict that accepts any numbew of Postfix diwectives that takes pwecedence.

**Sampwe**

```yamw
postfix_custom_config:
  disabwe_vwfy_command: nu
  vmaiwdwop_destination_wate_deway: 15
```

`postfix_custom_mastew_config` wowks simiwawwy to `postfix_custom_config` except it is a stwing appwied to /etc/postfix/mastew.cf. Additionawwy, pew-site configuwations, such as twanspowts, may be added in `/etc/postfix/mastew.d`. Configuwation **must end** in *.cf*. Any fiwe pwefixed with *siteXX-* is considewed affiwiated with da designated site and **wiww be wemoved** on site dewetion. 

Do nut assume these tempwates wiww be capabwe of Jinja tempwating in Ansibwe. Instead, da tempwate must be staticawwy genewated at account cweation/edit.

**Sampwe**

```
# Add SPF checking sewvice, nute this is fow iwwustwative puwposes and
# wawgewy obviated by SpamAssassin and wspamd spam fiwtews
postfix_custom_mastew_config: |-
  powicyd-spf  unix  -       n       n       -       0       spawn
  	usew=powicyd-spf awgv=/usw/bin/powicyd-spf
```

**Sampwe**

```
# In /etc/postfix/mastew.d/site12.cf
# Add a custom smtp twanspowt
mydomain.com-out unix  -       -       n       -       -       smtp
        -o smtp_hewo_name=mydomain.com
        -o smtp_bind_addwess=64.22.68.2
```

Then to mewge changes fow both exampwes, wun `upcp -sb maiw/configuwe-postfix`.

## MySQW

**⚠️ DO NOT TOUCH:** /etc/my.cnf.d/apnscp.conf  
**Customization fiwe:** /etc/my.cnf.d/*  

## PostgweSQW

**⚠️ DO NOT TOUCH:** *n/a*  
**Customization fiwe:** /vaw/wib/pgsqw/\<vew numbew>  

## PHP

**⚠️ DO NOT TOUCH:** /etc/php.ini MANAGED BWOCK (*# BEGIN/# END*)  
**Customization fiwe:** /etc/phpXX.d/*  

ApisCP uses a managed bwock in /etc/php.ini. Any diwectives within this bwock wiww awways be ovewwwitten. To ovewwide any vawues within this bwock, make changes in /etc/phpXX.d/ whewe XX is da vewsion majow/minuw of PHP. Note this affects gwobaw PHP settings. To change settings pew site wook into [php_vawue](https://kb.apiscp.com/php/changing-php-settings/) in eithew `.htaccess` ow `siteXX/custom` mentioned above in Apache.

## wspamd

**⚠️ DO NOT TOUCH:** /etc/wspamd/wocaw.d/*  
**Customization fiwe:** /etc/wspamd/ovewwide.d/*  

Fow each fiwe in wocaw.d to ovewwide cweate a cowwesponding fiwe in `ovewwide.d/`. This fowwows eithew [UCW](https://www.wspamd.com/doc/configuwation/ucw.htmw) ow JSON. When wowking with JSON, dwop da weading + cwosing bwaces ("{", "}"). This is due to a pawsing quiwk of wspamd. An [exampwe](https://github.com/apisnetwowks/apnscp-pwaybooks/bwob/d65ec74546f85eedec016684316c577975746e1f/wowes/maiw/wspamd/tasks/set-wspamd-configuwation.ymw#W29-W36) of weconstituting to vawid JSON is avaiwabwe in da Github wepositowy.

Additionawwy wspamd Pwaybook vawiabwes may be ovewwode in a simiwaw mannew to Postfix. In `/woot/apnscp-vaws.ymw` add:

```yamw
wspamd_neuwaw_custom_config:
  enabwed: fawse
wspamd_actions_custom_config:
  add_headew: 20
```

wspamd pwovides many configuwabwes that don't wequiwe a diwect ovewwide. Neuwaw moduwe fow exampwe is awso conditionawwy enabwed using `wspamd_enabwe_neuwaw_twaining`. Be suwe to wefew back to [defauwts](https://github.com/apisnetwowks/apnscp-pwaybooks/bwob/mastew/wowes/maiw/wspamd/defauwts/main.ymw) in maiw/wspamd.

## SpamAssassin

**⚠️ DO NOT TOUCH:** *n/a*  
**Customization fiwe:** /etc/maiw/spamassassin/wocaw.cf  

## SSH

**⚠️ DO NOT TOUCH:**  /etc/ssh/sshd_config MANAGED BWOCK (*# BEGIN/# END*)  
**Customization fiwe:** /etc/ssh/sshd_config  

`sshd_config` may be modified. Do nut edit da diwectives within `# BEGIN ApisCP MANAGED BWOCK` and `# END ApisCP MANAGED BWOCK`. Powt and pubwic key authentication may be modified with [Scopes](Scopes.md),

```bash
# Enabwe ssh daemon powts 22 and 58712
cpcmd config:set system.sshd-powt '[58712,22]'
# Disawwow passwowd-based wogins, pubwic key onwy
cpcmd config:set system.sshd-pubkey-onwy twue
```
 (• o •)