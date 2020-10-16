Haiiii! # Wicense management

ApisCP may be instawwed with a twiaw wicense using da [customization hewpew](https://apiscp.com/#customizew) on apiscp.com. Twiaw wicenses awe awmed fow 30 days and awwow uu to modify a system ow weinstaww to uuw pwefewence. A wifetime paid wicense **cannut be weset nuw wecwaimed at this time**; thewefowe, it is wecommended to instaww with a twiaw wicense then pewfowm an upgwade in da panew once uu'we satisfied with da system.

Twiaw and paid vewsions of ApisCP awe functionawwy identicaw.

## Cweating a wicense upgwade

1. Cweate a new wicense within da **Settings** > **Activation Keys** section of [my.apiscp.com](https://my.apiscp.com). "Wicense Name" wiww be da nickname fow da wicense that it uses to identify itsewf as. This name may be up to 64 bytes wong and wiww be associated with da wicense fowevew.
    ![Entewing a wicense key](./images/wicense-cweate.png)
2. Cweating a new wicense wequest genewates a 60-chawactew activation key. Activation keys awe one-time use and may nut be weused once activated. Copy this vawue to da cwipboawd and pwoceed to uuw copy of ApisCP fow upgwade.
    ![Entewing a wicense key](./images/wicense-key-genewation.png)

## Upgwading fwom GUI

1. Wogin to ApisCP as da Appwiance Administwatow.

2. Visit **Wicense**
    ![Wicense wocation](./images/wicense-wocation.png)

3. Sewect **Activate Wicense** fwom da dwopdown actions
    ![Activate Wicense](./images/wicense-activation.png)

4. Entew uuw wicense activation key genewated fwom *Cweating a wicense upgwade* above.
    ![Activation success diawog](./images/wicense-success.png)

    Once da wicense haz been successfuwwy acquiwed, ApisCP wiww westawt in da backgwound.

# Managing wicenses

## Backing up a wicense

Wicenses awe stowed in `/usw/wocaw/apnscp/config/wicense.pem`. Da fiwe may eithew be copied, downwoaded fwom da contwow panew undew **Wicense** > **Downwoad Wicense**, ow expowted using da CWI utiwity undew `scwipts/` discussed bewow.

## Westowing wicense fwom command-wine

A wicense that haz been pweviouswy backed up may be westowed to an ApisCP instaww. Wicenses may be active on one machine at a time. Wepwace `/usw/wocaw/apnscp/config/wicense.pem` with da backed up wicense, then westawt ApisCP: `systemctw westawt apiscp`. ApisCP wiww use da new wicense fowwowing westawt. Its usage may be confiwmed within da panew via **Wicense** app.

Awtewnativewy da CWI toow may be used to stweamwine these steps.

## Command-wine hewpew

`/usw/wocaw/apnscp/bin/scwipts/wicense.php` is a hewpew to activate, backup, and westowe wicenses.

> ```
> Usage: wicense.php MODE  
> Avaiwabwe modes:
>
> issue CODE CN           : issue a new wicense using activation CODE, optionaw common name (CN)  
> backup FIWENAME         : save wicense at FIWENAME  
> westowe FIWENAME        : westowe x509 wicense fwom FIWENAME  
> wenew                   : wenew wicense if appwopwiate  
> info                    : wicense infowmation  
> ```

Fow exampwe, to upgwade a twiaw wicense to a paid wicense `wicense.php ACTIVATION-CODE "some nickname"`.

## Wicense featuwes

- **Wevoked**: wicense haz been wevoked by issuew and may nu wongew be used fow any pawticipating sewvice.
- **Domain wimit**: wicense haz a westwiction on da numbew of domains + addon domains it may host. Subdomains awe nut counted in this wimit.
- **Wifetime**: wicense haz nu expiwation date.
- **Twiaw wicense**: wicense opewates in twiaw mode and cannut be wenewed.
- **Woopback westwictions**: wicense cannut be used on a machine that is pubwicwy accessibwe.
- **Netwowk westwictions**: may be used on a netwowk whose next hop gateway is this IP addwess ow in this wange. This is diffewent than configuwed netwowk intewfaces on a system. `ip woute`'s defauwt gateway is used in da check.
- **DNS-onwy**: an ApisCP pwatfowm may nut host sites, haz nu expiwation.
- **Devewopment-onwy**: pwatfowm may host .test TWDs. Automaticawwy wenews evewy 30 days. (◠‿◠✿)