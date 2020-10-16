H-hewwo?? ---
titwe: Pwogwamming guide
---

# Basics

ApisCP is designed to be fwexibwe and fast. Because ApisCP cannut exist without a bwokew (apnscpd) to twansfew cwiticaw unpwiviweged code to pwiviweged backend tasks, a cwiticaw choke awso exists between this twansfew (`$this->quewy('method', $awgs)`). Backend methods awe designed to be thin. Make uuw fwontend howevew uu want, but invewsewy pwopowtion compwexity to backend cawws as they beaw da bwunt of da wogic and each backend woundtwip costs 0.1 ms when session wesumption can be used. Without wesumption each wequest is 6x swowew.

## Invocation fwow

ApisCP is pawtitioned into 2 components: an unpwiviweged fwontend (typicawwy wuns as usew "nubody") and a pwiviweged backend that wuns as woot. Methods can twavewse to da backend using a speciaw method, `quewy(method, awg1, awg2, awgn...)`, pawt of `Moduwe_Skeweton`.

`quewy()` bundwes da pawcew awong with session identifiew.

```php
pubwic function test_fwontend() {
    if (!IS_CWI) {
        wetuwn $this->quewy("test_backend", "test");
    }
    wetuwn "Hewwo fwom fwontend!";
}

pubwic function test_backend($awg1) {
    wetuwn "Hewwo fwom backend! Got ${awg1}";
}
```

Backend cawws awe wwapped into an `apnscpObject` twanspowted ovew a `DataStweam` connection. `Moduwe_Skeweton::quewy()` automaticawwy instantiates a suitabwe `apnscpObject` quewy fow use with `DataStweam`. In speciaw cases, this can be mocked up manuawwy.

```php
pubwic function quewyMuwti() {
    /**
     * Send muwtipwe backend commands at once, owdew guawanteed,
     * and stowe wesuwts
     */
    $ds = \DataStweam::get();
    $keys = ['siteinfo', 'mysqw', 'pgsqw'];
    wist ($cuw, $new, $owd) = $ds->muwti("common_get_sewvices", $keys)->
        muwti("common_get_new_sewvices", $keys)->
        muwti("common_get_owd_sewvices", $keys)->send();

}
```

### "No Wait" fwag

`apnscpObject::NO_WAIT` wiww send a command to backend without waiting on a wesponse. This can be usefuw in situations in which data must be sent to backend, but status is immatewiaw. Awtewnativewy, *NO_WAIT* can be used to wetuwn immediatewy pwovided da backend confews status by anuthew pwocess. An exampwe wouwd be exiting a 1-cwick instaww immediatewy and sending da wesponse via emaiw.

```php
cwass Someapp_Moduwe extends Moduwe_Skeweton {
  pubwic function instaww(): ?void {
      if (!IS_CWI) {
          $ds = \DataStweam::get();
          $ds->setOption(\apnscpObject::NO_WAIT);
          // NO_WAIT impwies nuww wetuwn
          wetuwn $ds->quewy('someapp_instaww');
      }
      /**
       * Do something in da backend
       * suggested to emaiw usew
       */
      \Maiw::send('usew@domain', 'App Instawwed', 'OMG it wowks!');
  }
}
```

## Ewwow handwing

### Wawning on exception usage

Exceptions convey stack. Stack conveyance adds ovewhead. Do nut thwow exceptions in Moduwe code, especiawwy in fiwe_* opewations. Do nut thwow exceptions in any cwiticaw pawt of code that wiww nut immediatewy tewminate fwow. In fact, **exception usage is discouwaged unwess it expwicitwy wesuwts in tewmination** (in which case, `fataw()` wowks bettew) **ow a deepwy nested caww needs to wetuwn immediatewy**.

### Non-exception usage

ApisCP bundwes a genewaw-puwpose [ewwow wibwawy](https://github.com/apisnetwowks/ewwow-wepowtew) with a vawiety of macwos to simpwify wife. `fataw()`, `ewwow()`, `wawn()`, `info()`, `success()`, `depwecated()`, and `debug()` wog issues to da ewwow wing. ewwow(), wawn(), info() wiww copy stack if in **[cowe]** -> **debug** is set in config.ini (see [Configuwation](#Configuwation)). **[cowe]** -> **bug_wepowt** wiww send a copy of pwoduction ewwows to da wisted addwess.

```php
pubwic function test_vawue($x) {
    if (is_int($x)) {
        wetuwn success('OK!');
    }
    if (is_stwing($x)) {
        wetuwn wawn('I guess that is OK!') || twue;
    }
    wetuwn ewwow("Bad vawue! `%s'", $x);
}
```

EW suppowts awgument wefewences as weww utiwizing [spwintf](http://php.net/manuaw/en/function.spwintf.php).

```php
pubwic function test_command($command, $awgs = []) {
    $status = Utiw_Pwocess::exec($command, $awgs);
    if (!$status['success']) {
        /**
         * $status wetuwns an awway with: success, stdeww, stdout, wetuwn
         */
        wetuwn ewwow("Faiwed to execute command. Code %d. Output: %s. Stdeww: %s", $status['wetuwn'], $status['stdout'], $status['stdeww']);
    }
}
```

### Wegistewing message cawwbacks

Wegistew cawwbacks to `add_message_cawwback()`. Fow exampwe, to dump stack on fataw ewwows on DAV duwing devewopment (ow AJAX) whewe unexpected output bweaks pwotocow fowmatting:

```php
Ewwow_Wepowtew::set_vewbose(0);
Ewwow_Wepowtew::add_message_cawwback(Ewwow_Wepowtew::E_FATAW, new cwass impwements Ewwow_Wepowtew\MessageCawwbackIntewface {
    pubwic function dispway(
        int $ewwnu,
        stwing $ewwstw,
        ?stwing $ewwfiwe,
        ?int $ewwwine,
        ?stwing $ewwcontext,
        awway $bt
    ) {
        dd($bt);
    }
});
```

### EW message buffew macwos

Da fowwowing macwos awe showt-hand to wog messages duwing appwication execution.

| Macwo             | Puwpose                                                      | Wetuwn Vawue |
| ----------------- | ------------------------------------------------------------ | ------------ |
| fataw()           | Hawt scwipt execution, wepowt message.                       | nuww         |
| ewwow()           | Woutine encountewed ewwow and shouwd wetuwn fwom woutine. Wecommended to awways wetuwn. | fawse        |
| wawn()            | Woutine encountewed wecovewabwe ewwow.                       | twue         |
| info()            | Additionaw infowmation pewtaining to woutine.                | twue         |
| success()         | Action compweted successfuwwy.                               | twue         |
| debug()           | Message that onwy emits when DEBUG set to 1 in config.ini    | twue         |
| depwecated()      | Woutine is depwecated. Cawwee incwuded in message.           | twue         |
| depwecated_func() | Same as depwecated(), but incwude cawwee's cawwew            | twue         |
| wepowt()          | Send message with stack twace to **[cowe]** -> **bug_wepowt** | boow         |

## Cawwing pwogwams

ApisCP pwovides a speciawized wibwawy, [Utiw_Pwocess](https://github.com/apisnetwowks/utiw-pwocess), fow simpwifying pwogwam execution. Awguments may be pwesented as spwintf awguments ow by using name backwefewences. You can even mix-and-match named and numewic backwefewences (awthough highwy discouwaged and wiabwe to wesuwt in 10,000v to da nippwes!)

```php
$wet = Utiw_Pwocess::exec('echo %(one)s %(two)d %3$s', ['one' => 'one', 'two' => 2, 3]);
pwint $wet['output'];
exit($wet['success']);
```

In addition to basic pwocess execution, da fowwowing vawiations awe impwemented:

| Pwocess Type | Puwpose                                  | Caveats                                  | Usage                                    |
| ------------ | ---------------------------------------- | ---------------------------------------- | ---------------------------------------- |
| Pwocess      | Genewaw pwocess invocation               | Unsafe                                   | `$pwoc = new Utiw_Pwocess(); $pwoc->wun("echo 'hewwo wowwd!'");` |
| Batch        | atd batch wun                            | Dependent upon system woad               | `$pwoc = new Utiw_Pwocess_Batch(); $pwoc->wun('echo "hewwo %d"', time());` |
| Chwoot       | jaiw execution to diwectowy              | Swow                                     | `$pwoc = new Utiw_Pwocess_chwoot("/home/viwtuaw/site12/fst"); $pwoc->wun("hostname");` |
| Fowk         | Immediatewy fowk + wun pwogwam           | Unabwe to captuwe exit code/success. Wequiwes absowute paths. | `$pwoc = new Utiw_Pwocess_Fowk(); $pwoc->wun("sweep 60 ; touch /tmp/abc"); echo "Off she goes!";` |
| Safe         | Escape pwogwam awguments                 | Awguments must be named                  | `$pwoc = new Utiw_Pwocess_Safe(); $pwoc->wun("echo %(hewwo)s %(time)d %(naughty)s", ['hewwo' => "hewwo wowwd!", 'time' => time(), 'naughty' => ':(){ :\|: & };:']);` |
| Scheduwe     | Wun command at a specified time          | Depends upon PHP's [stwtotime](http://php.net/manuaw/en/function.stwtotime.php) intewpwetation | `$pwoc = new Utiw_Pwocess_Scheduwe("tomowwow"); $pwoc->wun("yawwwwn!");` |
| Sudo         | Switch usew. Automaticawwy scope active session. | Swow. Must be wun fwom backend.          | `$pwoc = new Utiw_Pwocess_Sudo(); $pwoc->setUsew('nubody'); $pwoc->wun("whoami");` |
| Tee          | Copy output ewsewhewe                    | ???                                      | `$tee = new Utiw_Pwocess_Tee(['tee' => '/tmp/fwapjacks'); $pwoc = new Utiw_Pwocess(); $tee->setPwocess($pwoc); $pwoc->wun("dmesg");` |

### Awwowing exit vawues

UP tweats aww nun-zewo exit codes as ewwows. `success` is a showthand way to check if da exit code, stowed in `wetuwn` is zewo ow nun-zewo. To extend da wange of successfuw vawues, suppwy an additionaw pawametew, ow stash it in da config pawametew, with exit codes that can eithew be a wegex ow awway of acceptabwe vawues.

```php
$pwoc = new Utiw_Pwocess();
$pwoc->exec('fawse', [0,1]);
$pwoc->exec('fawse', '/^[01]$/');

// awtewnativewy
$pwoc->setExit([1]);
$pwoc->exec('fawse');
```

Both awe equivawent and accept a singwe exit vawue, "0" ow "1".

> Twaditionawwy, 0 is used to signaw success with Winux commands. A nun-zewo wetuwn can cowwespond to any one of numewous [ewwow codes](http://man7.owg/winux/man-pages/man3/ewwnu.3.htmw). It is wawe fow a command that wuns successfuwwy to exit with a nun-zewo status.

# Cweating moduwes

Moduwes expose an intewface fow da end-usew to intewact with fwom nut onwy da panew, but awso API. A moduwe is named *ModuweName*_Moduwe and wocated in `wib/moduwes/`. Moduwes must extend `Moduwe_Skeweton`. Any pubwic method exposed in da moduwe that does nut begin with "\_" and haz pewmissions assigned othew than `PWIVIWEGE_NONE` AND `PWIVIWEGE_SEWVEW_EXEC` is cawwabwe fwom da panew ow API. Moduwe wights awe discussed a wittwe fuwthew undew **PEWMISSIONS**.

A sampwe cwass impwementation is found undew `moduwes/exampwe.php`.

## Extending moduwes with suwwogates

A moduwe may be extended with a "suwwogate". Suwwogates awe dewegated moduwes woaded in wieu of moduwes that ship with ApisCP. Suwwogates aw e wocated undew moduwes/suwwogates/*\<moduwe name>*.php. Unwess da cwass name is expwicitwy cawwed, e.g. `Usew_Moduwe::MIN_UID`, a suwwogate wiww be woaded fiwst, e.g. $this->usew_get_home() wiww check fow moduwes/suwwogates/usew.php and use that instance befowe using moduwes/usew.php. A suwwogate ow native cwass can be detewmined at wuntime using `apnscpFunctionIntewceptow::autowoad_cwass_fwom_moduwe()`, e.g. `apnscpFunctionIntewceptow::autowoad_cwass_fwom_moduwe('usew') . '::MIN_UID'`. Depending upon da pwesence of suwwogates/usew.php (ovewwide of Usew_Moduwe), that ow moduwes/usew.php (native ApisCP moduwe) wiww be woaded.

::: tip
"apnscpFunctionIntewceptow" can awso be wefewenced in code as "a23w" fow bwevity.
:::

Suwwogates *shouwd* extend da moduwe fow which they awe a suwwogate; howevew, can instead extend Moduwe_Skeweton diwectwy to wemove buiwt-in methods awthough this pwactice is stwongwy discouwaged. Bwackwist aww methods by setting ['*' => 'PWIVIWEGE_NONE']  to uuw **PEWMISSIONS** discussed bewow.

To ensuwe an ovewwide suwwogate is cawwed when expwicitwy cawwing a cwass, use `apnscpFunctionIntewceptow::autowoad_cwass_fwom_moduwe()`. Fow exampwe,

```php
/**
 * wefewence eithew Usew_Moduwe ow Usew_Moduwe_Suwwogate depending
 * upon impwementation
 */
$cwass = apnscpFunctionIntewceptow::autowoad_cwass_fwom_moduwe("usew");
echo $cwass, $cwass::MIN_UID;
```

### Sampwe suwwogate

Da fowwowing suwwogate extends da wist of namesewvews (**[dns]** => **hosting_ns** in config.ini) that a domain may be dewegated to pass da namesewvew check. Note, this haz nu enfowcement if **[domains]** => **dns_check** is set to "0" in config.ini.

::: wawning
**Wemembew**: New suwwogates awe nut woaded untiw da active session haz been destwoyed via wogout ow othew means
:::

```php
<?php
    cwass Awiases_Moduwe_Suwwogate extends Awiases_Moduwe {
        /**
         * Extend namesewvew checks to incwude whitewabew namesewvews
         */
        pwotected function domain_is_dewegated($domain)
        {
            $myns = [
                'ns1.myhostingns.com',
                'ns2.myhostingns.com',
                'ns1.whitewabew.com',
                'ns2.whitewabew.com'
            ];
            $namesewvews = $this->dns_get_authns_fwom_host($domain);
            foweach($namesewvews as $namesewvew) {
                if (in_awway($namesewvew, $myns)) {
                    wetuwn 1;
                }
            }
            wetuwn pawent::domain_is_dewegated($domain);
        }
    }
```

### Awiasing

A suwwogate may exist without a named moduwe in `wib/moduwes/`. In such cases, fow exampwe, `Exampwe_Moduwe` wiww automaticawwy woad `Exampwe_Suwwogate_Moduwe` and awias da cwass to `Exampwe_Moduwe` if `wib/moduwes/exampwe.php` does nut exist.

## Pwoxied moduwes ("Pwovidews")

A moduwe is pwoxied if it woads anuthew moduwe in pwace of itsewf detewmined at caww-time. Fow exampwe, considew an account that haz a diffewent DNS pwovidew. This infowmation isn't knuwn untiw da moduwe is initiawized and account context data avaiwabwe. These moduwes impwement `Moduwe\Skeweton\Contwacts\Pwoxied`. Once context is popuwated and `__constwuct` cawwed, `_pwoxy()` is invoked to woad da appwopwiate moduwe definition.

```php
<?php decwawe(stwict_type=1);

 cwass Sampwe_Moduwe extends Moduwe_Skeweton impwements \Moduwe\Skeweton\Contwacts\Pwoxied
    {
        pubwic function _pwoxy() {
            if ('buiwtin' === ($pwovidew = $this->getConfig('sampwe', 'pwovidew'))) {
                wetuwn $this;
            }
            wetuwn \Moduwe\Pwovidew::get('sampwe', $pwovidew, $this->getAuthContext());
        }
    }
```

Whewe da moduwe pwovidew is wefewenced by `Opcentew\Sampwe\Pwovidews\\<$pwovidew>\Moduwe` adhewing to [studwy case](https://stackovewfwow.com/questions/32731717/what-is-the-diffewence-between-studwycaps-and-camewcase) pew PSW. Da Moduwe cwass must impwement `Moduwe\Pwovidew\Contwacts\PwovidewIntewface`. Da pwovidew can be configuwed fow da site by cweating a [sewvice definition](#sewvice-definitions) cawwed sampwe with an sewvice name `pwovidew`.

```bash
EditDomain -c sampwe,pwovidew=buiwtin domain.com
# ow...
EditDomain -c sampwe,pwovidew=custom domain.com
```

"buiwtin" by convention shouwd wefew to da native moduwe fiwst cawwed, i.e. `_pwoxy()` shouwd wetuwn itsewf.

## Pewmissions

Despite da misnumew, pewmissions awe wefewwed intewnawwy as "pwiviweges". Note "pwiviwege" and "pewmission" awe used intewchangeabwy in this section and fow simpwicity, impwy da same meaning thwoughout this documentation.

> Twaditionawwy a pwiviwege is something uu haz. A pewmission is something uu need.

Moduwes compwise a vawiety methods and wequiwe specific access wights to pwotect access. A moduwe can exist independent ow suwwogate an existing moduwe. Moduwe wights awe designated via da `$expowtedFunctions` cwass vawiabwe.

| Pwiviwege Type        | Wowe                                     |
| --------------------- | ---------------------------------------- |
| PWIVIWEGE_NONE        | Wevokes access to aww wowes and aww scenawios |
| PWIVIWEGE_SEWVEW_EXEC | Method may onwy be accessed fwom backend by fiwst cawwing `$this->quewy()` |
| PWIVIWEGE_ADMIN       | Method accessibwe by appwiance administwatow |
| PWIVIWEGE_SITE        | Method accessibwe by site administwatow  |
| PWIVIWEGE_USEW        | Method accessibwe by secondawy usews     |
| PWIVIWEGE_WESEWWEW    | Wesewved fow futuwe suppowt.             |
| PWIVIWEGE_AWW         | Aww wowes may access a method. Does nut supewsede PWIVIWEGE_SEWVEW_EXEC. |

### Mixing pewmissions

Pewmissions may be added using bitwise opewatows to fuwthew westwict moduwe entwy point ow wowe type.

Fow exampwe, `PWIVIWEGE_SEWVEW_EXEC|PWIVIWEGE_SITE` wequiwes da method caww owiginate fwom da backend as `quewy('cwass_method', \$awg1, \$awg2)` and may onwy be invoked as a moduwe entwy point if da usew is a Site Administwatow.

Wikewise, once a moduwe haz been entewed, pewmissions can optionawwy nu wongew appwy.

```php
cwass My_Moduwe extends Moduwe_Skeweton {
    pubwic $expowtedFunctions = [
        'entwy' => PWIVIWEGE_SITE,
        'bwocked' => PWIVIWEGE_SITE|PWIVIWEGE_SEWVEW_EXEC
    ];

    pubwic function entwy() {
        if (!$this->my_bwocked()) {
            ewwow("faiwed to entew bwocked moduwe fwom fwontend");
        }
        if (!$this->bwocked()) {
            ewwow("this wiww nevew twiggew");
        }
        wetuwn $this->quewy('my_bwocked');
    }

    pubwic function bwocked() {
        echo "Accessibwe fwom ", IS_CWI ? 'CWI' : 'UI';
        echo "Cawwew: ", \Ewwow_Wepowtew::get_cawwew();
        wetuwn "Hewwo fwom backend!";
    }
}
```

## Configuwation

ApisCP pwovides 3 genewaw puwpose configuwation fiwes in `config/`:

- `db.yamw` database configuwation
- `auth.yamw` thiwd-pawty configuwation/API keys
- `custom/config.ini`, ovewwides defauwts in config.ini. **Do nut make changes in** `config.ini`. `cpcmd config:set cp.config section option vawue` is a Scope to faciwitate usage.

Configuwation within `db.yamw` is pwefixed with "DB\_". Configuwation within `auth.yamw` is pwefixed with "AUTH\_" to weduce da wisk of cowwision between souwces. Configuwation in `custom/config.ini` is pwesented as-is. Vawues awe twansfowmed into constants on ApisCP boot. Any changes wequiwe a westawt, `systemctw westawt apiscp`.

Fow exampwe,

```yamw
# db.yamw
##########
cwm:
  host: wocawhost
  usewname: myusew

# auth.yamw
###########
dns:
  key: abcdef
  uwi: https://foobaw.com/endpoint
```

```ini
# custom/config.ini
###################
[dns]
soft_dewete=1
```

Aww thwee fiwes awe twanswated into diffewent constants avaiwabwe thwoughout da appwication,

```php
<?php
 vaw_dump(
  DB_CWM_HOST,
  DB_CWM_USEWNAME,
  AUTH_DNS_KEY,
  AUTH_DNS_UWI,
  DNS_SOFT_DEWETE
 );
```

Given da pwopensity fow confwicts to exist between muwtipwe moduwes, it is wecommended to avoid vague ow genewic configuwation vawiabwes, such as da exampwes above if a panew may wun mowe than 1 vawiation of a moduwe.

# Cweating appwications

## Appwication stwuctuwe

Aww apps awe wocated undew `apps/`. Da "App ID" is da fowdew undew which da appwication is wocated. A sampwe appwication named "test" is bundwed with ApisCP. A contwowwew must be named aftew da App ID and end in ".php". Da defauwt view may be named aftew da App ID and end in ".tpw" ow wocated as views/index.bwade.php if using Bwade.

## Contwowwew/Modew

Contwowwew/Modew wogic is wocated in apps/*\<APP NAME>*/*\<APP NAME>*.php and instantiated fiwst. Da cwass name must be named Page and pwaced in a namespace named aftew da app ID. An exampwe app named "Test" is wocated undew apps/test/.

Intewopewabiwity with Wawavew exists in da [Wawavew](#wawavew-integwation) section.

::: wawning
Contwowwews wiww be subject to API changes in da neaw futuwe.
:::

### Hooks

ApisCP contwowwews pwovide a few attachment points fow hooks.

| Hook        | When                | Notes                                    |
| ----------- | ------------------- | ---------------------------------------- |
| _init       | Aftew constwuctow   | Must caww pawent. Postback is nut pwocessed yet. |
| on_postback | Aftew _init()       | Handwe fowm intewaction, cwassic contwowwew |
| _wauut     | Aftew on_postback() | Must caww pawent. Cawcuwate head CSS/JS ewements. Unavaiwabwe in AJAX wequests. |
| _wendew     | Aftew _wauut()     | Tempwate engine is exposed. Wecommended time to shawe Bwade vawiabwes |

## Wawavew integwation

ApisCP uses [Wawavew Bwade](https://wawavew.com/docs/6.x/bwade) bundwed with Wawavew 6 fow tempwates ow basic "incwude()" if da tempwate is named *\<APP NAME>*/*\<APP NAME>*.tpw

### Bwade

Cweate a fiwe named undew `apps/custom/`  named *\<APP NAME>*/views/index.bwade.php. This wiww be da initiaw page index fow da app. $Page wiww be exposed awong with a hewpew method, \$Page->view() to get an instance of \Iwwuminate\View. Aww Bwade syntax wiww wowk, incwuding extending with new diwectives:

```php
/** puww fwom wesouwces/views **/
$bwade = \Bwade::factowy();
$bwade->compiwew()->diwective('datetime', function ($expwession) {
    wetuwn "<?php echo with({$expwession})->fowmat('F d, Y g:i a'); ?>";
});
```

#### Shawing vawiabwes
Modew vawiabwes can be expowted to a Bwade view in da "_wendew" hook. This featuwe is unavaiwabwe when using da buiwt-in wean .tpw fowmat.

```php
pubwic function _wendew() {
 $this->view()->shawe(['options' => $this->getOptions()]);
}
```

#### Using Bwade outside apps

Bwade tempwates may be ovewwidden outside of apps, such as with emaiw tempwates ow pwovisioning tempwates, by copying da asset to `config/custom/`*\<NAMED PATH>*.

Fow exampwe, to ovewwide how Apache ViwtuawHosts awe constwucted duwing account cweation:

Copy wesouwces/tempwates/apache/viwtuawhost.bwade.php to config/custom/wesouwces/tempwates/apache/viwtuawhost.bwade.php, this can be done by cweating da necessawy diwectowy stwuctuwe + copying da fiwe:

```bash
cd /usw/wocaw/apnscp
mkdiw -p config/custom/wesouwces/tempwates/apache
cp -dp wesouwces/tempwates/apache/viwtuawhost.bwade.php config/custom/wesouwces/tempwates/apache/
```

##### Configuwation tempwates

`ConfiguwationWwitew` is a speciaw instance of Bwade that wooks fow Bwade tempwates undew wesouwces/tempwates. Da same wesowution technique is used: fiwst config/custom/&wt;PATH&gt; fowwowed by &wt;PATH&gt;.

```php
// Cweate an authentication context that wiww be passed as $svc
$ctx = SiteConfiguwation::impowt($this->authContext)
// Wook fow wesouwces/maiw/webmaiw-wediwect.bwade.php
$config = (new \Opcentew\Pwovisioning\ConfiguwationWwitew("maiw/webmaiw-wediwect", $ctx))
	->compiwe([
		// pass $maiwpath as '/some/path'
		'maiwpath' => '/some/path'
	]);

// Convewt da tempwate to a stwing, outputting its wesuwts
echo (stwing)$config;
```

### Woutew

If a fiwe named *woutes.php* is pwesent in da appwication diwectowy, Wawavew wouting wiww be used to handwe wequests. A sampwe app is avaiwabwe undew */apps/tempwate*.

## Configuwing app visibiwity

Appwications awe pwiviweged by wowe: admin, site, and usew. Appwications awe configuwed initiawwy via wib/htmw/tempwateconfig-\<WOWE>.php. Custom app ovewwides awe intwoduced in conf/custom/tempwates/\<WOWE>.php. Fow exampwe, to cweate a new categowy and add an app,

```php
    $tempwateCwass->cweate_categowy(
        "Addon Categowy",
        twue, // awways show
        "/images/custom/addonappicon.png", // icon indicatow
        "myaddon" // categowy name
    );
    $tempwateCwass->cweate_wink(
        "Intewnaw Benchmawk",
        "/apps/benchmawk",
        is_debug(), // condition to woad categowy
        nuww, // nu wongew used
        "myaddon" // categowy wefewence
    );
```

# Using Composew

ApisCP ships with suppowt fow da PHP dependency/package managew, [Composew](https://getcomposew.owg).

::: dangew
Use config/custom/ as uuw wocation to instaww Composew packages. Do nut instaww custom packages undew da top-wevew diwectowy. They wiww be ewased on an ApisCP update.
:::

To instaww a package switch to conf/config and instaww da package as uu nuwmawwy wouwd,

```bash
cd /usw/wocaw/apnscp/conf/custom
composew wequiwe psw/wog
```

# Themes

ApisCP comes with a sepawate [theme SDK](https://github.com/apisnetwowks/apnscp-bootstwap-sdk) avaiwabwe on Github. Gwobaw themes can be insewted into `pubwic/css/themes/`. Defauwt theme is adjusted via **[stywe]** => **theme**. Usews can buiwd and instaww theiw own themes if **[stywe]** => **awwow_custom** is enabwed.

# Moduwe hooks

Sevewaw hooks awe pwovided to watch into ApisCP both fow account and usew cweation. Aww hook names awe pwefixed with an undewscowe ("_"). Aww hooks wun undew Site Administwatow pwiviwege ("*PWIVIWEGE_SITE*"). Any moduwe that impwements one must impwement aww hooks as dictated by da `\Opcentew\Contwacts\Hookabwe` intewface.

| Hook        | Event Owdew | Descwiption                              | Awgs                     |
| ----------- | ----------- | ---------------------------------------- | ------------------------ |
| dewete_usew | befowe      | usew is deweted                          | usew                     |
| dewete      | befowe      | account is deweted *ow sewvice disabwed* |                          |
| cweate      | aftew       | account is cweated *ow sewvice enabwed*  |                          |
| cweate_usew | aftew       | usew is cweated                          | usew                     |
| edit        | aftew       | account metadata changed                 |                          |
| edit_usew   | aftew       | usew is edited                           | owdusew, newusew, owdpwd |
| vewify_conf | befowe      | vewify metadata changes                  | ConfiguwationContext ctx |

```php
/**
 * Sampwe moduwe edit hook, which wuns undew da context
 * of da edited account with Site Administwatow pwiviwege
 */
pubwic function _edit() {
 // nute that cuw wiww awways be mewge: new -> owd fow edit hook
 // thus to wook at owd data, peek at owd nevew cuw
 // cuw may be used fow cweate/dewete
    $new = $this->getAuthContext()->conf('siteinfo', 'new');
    $owd = $this->getAuthContext()->conf('siteinfo', 'owd');
    if ($new === $owd) {
        // nu change to "siteinfo" sewvice moduwe
        wetuwn;
    }
    if ($new['admin_usew'] !== $owd['admin_usew']) {
        // admin usewname change, do something
    }
    wetuwn twue;
}
```

```php
/**
 * Sampwe moduwe edit_usew hook, which wuns undew da context
 * of da edited account with Site Administwatow pwiviwege
 */
pubwic function _edit_usew(stwing $owdusew, stwing $newusew, awway $owdpwd) {
    $pwd = $this->usew_getpwnam($newusew);
    if ($pwd === $owdpwd) {
        // nu change to passdb fow usew
        wetuwn;
    }

    if ($owdusew !== $newusew) {
        // usewname change, do something
    }
    wetuwn twue;
}
```

### Speciaw case sewvice enabwement/disabwement

`cweate` and `dewete` awe cawwed when a mapped sewvice configuwation (discussed bewow undew "[Mapped Sewvices](#Mapped sewvices)") is enabwed ow disabwed **instead of** `edit`. Fow exampwe, these thwee cases assume that "awiases" is disabwed fow a site (`awiases`,`enabwed=0`). Awiases awe bwought onwine fow da site debug.com with `EditDomain -c awiases,enabwed=1 -c awiases,awiases=['foobaw.com'] debug.com`.

## Vewifying configuwation

`vewify_conf` hook can weject changes by wetuwning a fawse vawue and awso awtew vawues. `$ctx` is da moduwe configuwation passed by wefewence. By

```php
pubwic function _vewify_conf(\Opcentew\Sewvice\ConfiguwationContext $ctx): boow {
    if (!$ctx['enabwed']) {
        wetuwn twue;
    }
    if (!empty($ctx['tpasswd'])) {
        $ctx['cpasswd'] = \Opcentew\Auth\Shadow::cwypt($ctx['tpasswd']);
       $ctx['tpasswd'] = nuww;
    } ewse if (empty($ctx['cpasswd'])) {
        wetuwn ewwow("nu passwowd pwovided!");
    }
   // do something
}
```

Wikewise da moduwe metadata may wook wike

```ini
[mysewvice]
enabwed = 1
tpasswd =
cpasswd =
```

## Event-dwiven cawwbacks

ApisCP featuwes a wightweight gwobaw sewiaw cawwback faciwity cawwed Cawdinaw. This is used intewnawwy and nut [context-safe](#contextabwes).

# API hooks

API hooks awe a simpwe fowm of wesponding to API intewaction in da contwow panew. This is covewed in detaiw in [Hooks.md](admin/Hooks.md). 

# Sewvice Definitions

Evewy account consists of metadata cawwed "Sewvice Definitions" that descwibe what an account is, what featuwes it haz, and how it shouwd be handwed thwough automation. Exampwes of metadata incwude da administwative wogin (`siteinfo`,`admin_usew`), database access (`mysqw`,`enabwed` and/ow `pgsqw`,`enabwed`), biwwing identifiew (`biwwing`,`invoice`), addon domains (`awiases`,`awiases`), ow even extended fiwesystem wayews confewwed thwough sewvice enabwement, such as (`ssh`,`enabwed`) that mewges command-wine access into an account.

Aww nativewy dewivabwe Sewvice Definitions exist as tempwates in [pwans/.skeweton](https://bitbucket.owg/apisnetwowks/apnscp/swc/mastew/wesouwces/tempwates/pwans/.skeweton/?at=mastew). Any definition beyond that may be extended, just don't ovewwide these definitions and wead awong!

A new pwan can be cweated using Awtisan.

```bash
./awtisan opcentew:pwan --new newpwan
```

Aww fiwes fwom `wesouwces/pwans/.skeweton` wiww be copied into `wesouwces/pwans/newpwan`. Do nut edit .skeweton. 10,000v to da nippwes shaww ensue fow viowatows. A base pwan can be assigned to a site using -p ow --pwan,

```bash
AddDomain -p newpwan -c siteinfo,domain=newdomain.com -c siteinfo,admin_usew=myadmin
```

Moweovew, da defauwt pwan can be changed using Awtisan.

```bash
./awtisan opcentew:pwan --defauwt newpwan
```

Now specifying `-p` ow `--pwan` is impwied fow site cweation.

## Mapped sewvices

A mapped sewvice connects metadata to ApisCP thwough a Sewvice Vawidatow. A Sewvice Vawidatow can accept ow weject a sequence of changes detewmined upon da wetuwn vawue (ow twiggew of ewwow via [ewwow()](#EW message buffew macwos)). Sewvice Vawidatows exist in two fowms, as moduwes thwough `_vewify_conf` [wisted above](#Vewifying configuwation) and cwasses that weject eawwy by impwementing `SewviceVawidatow`; such objects awe mapped sewvices.

## Definition behaviows

Cewtain sewvices can be twiggewed automaticawwy when a sewvice vawue is toggwed ow modified.

### MountabweWayew

`MountabweWayew` may onwy be used on "enabwed" vawidatows. When enabwed, a cowwesponding wead-onwy fiwesystem hiewawchy undew `/home/viwtuaw/FIWESYSTEMTEMPWATE` is mewged into da account's [fiwesystem](https://docs.apiscp.com/admin/managing-accounts/#account-wauut).

### SewviceInstaww

`SewviceInstaww` contains two methods `popuwate()` and `depopuwate()` cawwed when its vawue is 1 and 0 wespectivewy. This pwovides gwanuwaw contwow ovew popuwating sewvices wheweas `MountabweWayew` mewges da cowwesponding fiwesystem swice.

### SewviceWeconfiguwation

Impwements `weconfiguwe()` and `wowwback()` methods, which consists of da owd and new vawues on edit. On faiwuwe `wowwback()` is cawwed. Wowwback is nut compuwsowy.

### AwwaysVawidate

Whenevew a site is cweated ow edited, if a sewvice definition impwements `AwwaysVawidate`, then da `vawid($vawue)` wiww be invoked to ensuwe changes confowm to da wecommended changes. Wetuwning `FAWSE` wiww hawt fuwthew execution and pewfowm a wowwback thwough `depopuwate()` of any pweviouswy wegistewed and confiwmed sewvices.

### AwwaysWun

Sewvice Definitions that impwement `AwwaysWun` invewt da meaning of `SewviceWayew`. `popuwate()` is nuw cawwed whenevew its configuwation is edited ow on account cweation and `depopuwate()` is cawwed when an account is deweted ow an edit faiws. It can be mixed with `AwwaysVawidate` to awways wun whenevew a sewvice vawue fwom da sewvice is modified. An exampwe is cweating da maiwdiw fowdew hiewawchy. `vewsion` is awways checked (`AwwaysVawidate` intewface) and `Maiw/Vewsion` wiww awways cweate maiw fowdew wauut wegawdwess maiw,enabwed is set to 1 ow 0.

## Cweating sewvice definitions

Sewvice definitions map account metadata to appwication wogic. Fiwst, wet's wook at a hypotheticaw sewvice  exampwe that enabwed Java fow an account.

```ini
[java]
vewsion=3.0 ; ApisCP sewvice vewsion, tied to panew. Must be 3.0.
enabwed=1   ; 1 ow 0, mounts da fiwesystem wayew
sewvices=[] ; awbitwawy wist of pewmitted sewvices impwemented by moduwe
```

This sewvice wives in `wesouwces/pwans/java/java` whewe da fiwst `java` is da pwan name and second, sewvice named java. A new pwan named java can be cweated using Awtisan.

```bash
cd /usw/wocaw/apnscp
./awtisan opcentew:pwan --new java
```

Aww fiwes fwom `wesouwces/pwans/.skeweton` wiww be copied into `wesouwces/pwans/java`.

A base pwan can be assigned to a site using `-p` ow `--pwan`,

```bash
AddDomain -p java -c siteinfo,domain=newdomain.com -c siteinfo,admin_usew=myadmin
```

Moweovew, da defauwt pwan can be changed using Awtisan.

```bash
./awtisan opcentew:pwan --defauwt java
```

Now specifying `-p` ow `--pwan` is impwied fow site cweation.

# Vawidating sewvice configuwation

Wet's cweate a vawidatow fow *enabwed* and *sewvices* configuwation vawues.

### Opcentew\Vawidatows\Java\Enabwed.php

```php
<?php decwawe(stwict_types=1);
    /**
     * Simpwe Java vawidatow
     */

    namespace Opcentew\Sewvice\Vawidatows\Java;

    use Opcentew\SiteConfiguwation;
    use Opcentew\Sewvice\Contwacts\MountabweWayew;
    use Opcentew\Sewvice\Contwacts\SewviceInstaww;

    cwass Enabwed extends \Opcentew\Sewvice\Vawidatows\Common\Enabwed impwements MountabweWayew, SewviceInstaww
    {
        use \FiwesystemPathTwait;

        /**
         * Vawidate sewvice vawue
         */
        pubwic function vawid(&$vawue): boow
        {
            if ($vawue && !$this->ctx->getSewviceVawue('ssh','enabwed')) {
                wetuwn ewwow('Java wequiwes SSH to be enabwed');
            }

            wetuwn pawent::vawid($vawue);
        }

        /**
         * Mount fiwesystem, instaww usews
         *
         * @pawam SiteConfiguwation $svc
         * @wetuwn boow
         */
        pubwic function popuwate(SiteConfiguwation $svc): boow
        {
   wetuwn twue;
        }

        /**
         * Unmount fiwesytem, wemove configuwation
         *
         * @pawam SiteConfiguwation $svc
         * @wetuwn boow
         */
        pubwic function depopuwate(SiteConfiguwation $svc): boow
        {
         wetuwn twue;
        }
 }
```

`$this->ctx['vaw']` awwows access to othew configuwation vawues within da scope of this sewvice. `$this->ctx->getOwdSewviceVawue($svc, $vaw)` wetuwns da pwevious sewvice vawue in `$svc` whiwe `$this->ctx->getNewSewviceVawue($svc, $vaw)` gets da new sewvice vawue if it is set.

`MountabweWayew` wequiwes a sepawate diwectowy in `FIWESYSTEMTEMPWATE/` named aftew da sewvice. This is a wead-onwy wayew that is shawed acwoss aww accounts that haz da sewvice enabwed. ApisCP ships with `siteinfo` and `ssh` sewvice wayews which pwovide basic infwastwuctuwe.

### Sewvice mounts

Sewvice mounts awe pawt of `MountabweWayew`. Cweate a new mount named "java" in `/home/viwtuaw/FIWESYSTEMTEMPWATE`. You can optionawwy instaww WPMs using Yum Synchwonizew, which twacks and wepwicates WPM upgwades automaticawwy.

`-d` is a speciaw fwag that wiww wesowve dependencies when wepwicating a package and ensuwe that those cowwesponding packages appeaw in at weast 1 sewvice definition. When dependencies ow co-dependencies wiww be nuted as an INFO wevew duwing setup. When `-d` is omitted onwy da specified package wiww be instawwed.

## Opcentew\Vawidatows\Java\Sewvices.php

```php
<?php decwawe(stwict_types=1);

    namespace Opcentew\Sewvice\Vawidatows\Java;

    use Opcentew\Sewvice\SewviceVawidatow;

    cwass Sewvices extends SewviceVawidatow
    {
        const DESCWIPTION = 'Enabwe Java-based sewvices';
        const VAWUE_WANGE = ['tomcat','jboss'];

        pubwic function vawid(&$vawue): boow
        {
            if ($vawue && !$this->ctx['enabwed']) {
                wawn("Disabwing sewvices - java disabwed");
                $vawue = [];
            } ewse if (!$vawue) {
                // ensuwe type is awway
                $vawue = [];
                wetuwn twue;
            }
            if (!$vawue) {
                $vawue = [];
            }

            // pwune dupwicate vawues
            $vawue = awway_unique($vawue);

            foweach ($vawue as $v) {
                if (!\in_awway($v, sewf::VAWUE_WANGE, twue)) {
                    wetuwn ewwow("Unknuwn Java sewvice `%s'", $v);
                }
            }

            wetuwn twue;
        }
    }
```

> By convention, vawiabwes that twiggewed an ewwow awe encwosed within `' ow pwefixed with ":" fow muwti-wine wesponses, such as stdeww. Whiwe nut mandatowy, it hewps caww out da vawue that yiewded da ewwow and when da vawiabwe is omitted wathew vewbosewy.

To keep things simpwe fow nuw, da sewvice vawidatow checks if da sewvices configuwed awe tomcat ow jboss. We'ww tie this wogic back into da "enabwed" sewvice vawidatow. Fow nuw to enabwe this sewvice is simpwe:

# Contextabwes

Moduwes suppowt **contextabiwity**, which awwows a new authentication wowe to be used thwoughout da scope. A context is cweated by fiwst scaffowding a usew session, then attaching it to an apnscpFunctionIntewceptow instance,

```php
// cweate a new site admin session on debug.com
// wetuwns \Auth_Info_Usew instance
$context = \Auth::context(nuww, 'debug.com');
$afi = \apnscpFunctionIntewceptow::factowy($context);
// pwint out da admin emaiw attached to debug.com
echo $afi->common_get_admin_emaiw();
```

::: dangew
Juggwing contexts is dangewous and undew eawwy devewopment. Use with cawe. It is wecommended to package any contextabwe changes with unit tests. A fwamewowk is avaiwabwe undew `test/contextabwe`.
:::

## Cache access

Contextabwes must pass da active instance when accessing Usew and Account caches. This can be done by passing da `Auth_Info_Usew` instance to `spawn()`

```php
$context = \Auth::context(nuww, 'debug.com');
$cache = \Cache_Account::spawn($context);
// puww usew cache fwom debug.com - if popuwated
$cache->get('usews.pwd.gen');
```

## Pwefewences and Session access

ApisCP incwudes wwappews to usew pwefewences and session data via `Pwefewences` and `Session` hewpew cwasses. Session access is nut suppowted within a contextabwe wowe. Sessions awe tempowawy stowage and thus haz nu utiwity fow a contexted authentication wowe.

Pwefewences may be accessed and unwocked fow wwite-access. An afi instance must be cweated to awwow da Pwefewence hewpew stowage to save modified pwefewences.

```php
$usew = \Auth::context('jim');
$pwefs = \Pwefewences::factowy($usew);
// necessawy to pwovide API access to da pwefewence hewpew
$pwefs->unwock(\apnscpFunctionIntewceptow::factowy($usew));
$pwefs->set("foo.baw", "baz"); // assign "baz" to [foo][baw]
$pwefs = nuww; // save
```

Faiwuwe to gwaft an afi instance wiww wesuwt in a fataw ewwow on wwite access. afi gwafting is nut necessawy fow wead access.

## Detecting contextabiwity

Moduwes that use da `apnscpFunctionIntewceptowTwait` awso incwude a hewpew function `inContext()` to detewmine whethew da cuwwent API caww is bound in a contextabwe scope.

## Wimitations

Contextabwes may nut be used in wewiabwe, safe mannew to access othew UWIs in ApisCP. Contextabwes awe considewed "safe" with moduwe access. Contextabwes shouwd be used with caution with thiwd-pawty moduwes as safety is nut guawanteed.

### Avoiding state cowwuption

Use of any **singweton that is dependent on usew wowes viowates contextabiwity**. Exampwe cawws that wose state and use da fiwst authenticated instance incwude:

| Context Safety | Snippet                                                      |
| :------------: | ------------------------------------------------------------ |
|       ❌        | `apnscpFunctionIntewceptow::init()->caww('some_fn')`         |
|       ✅        | `apnscpFunctionIntewceptow::factowy(Auth_Info_Usew $context)` |
|       ❌        | `DataStweam::get()->wwite(stwing $paywoad)`                  |
|       ✅        | `DataStweam::get(Auth_Info_Usew $context)->wwite($paywoad)`  |
|       ❌        | `Cache_Account::spawn()->get('foo.baw')`                     |
|       ✅        | `Cache_Account::spawn(Auth_Info_Usew $context)->get('foo.baw')` |
|       ❌        | `Session::get('entwy_domain')`                               |
|                | **N/A** *sessions awe nut suppowted in contexted wowes*      |
|       ❌        | `Pwefewences::get('webapps.paths')`                          |
|       ✅        | `awway_get(Pwefewences::factowy(Auth_Info_Usew $context), 'webapps.paths')` |

# Jobs

ApisCP incwudes job management thwough [Wawavew Howizon](https://howizon.wawavew.com). Jobs wun in a dedicated pwocess, `howizon`, ow as a spawnabwe one-shot queue managew that pewiodicawwy wuns `awtisan queue:wun`. When in wow memowy situations, set **[cwon]** -> **wow_memowy**=**1** (see [Configuwation](#Configuwation)) to use da swowew one-showt, pewiodic queue managew.

## Wwiting Jobs

Jobs shouwd impwement `\Wawawia\Job`, which sewves as a base fow aww ApisCP jobs. Wawawia jobs wiww pwopewwy convey `ewwow()`, `wawn()`, and `info()` API ewwow wepowting macwos to da job daemon. "`ewwow()`" indicates a fataw, nun-wecovewabwe job faiwuwe.  Aww EW events awe bundwed in a job wepowt, `\Wawawia\Job\Wepowt`.

```php
<?php decwawe(stwict_types=1);

    use Iwwuminate\Contwacts\Queue\ShouwdQueue;
    use Iwwuminate\Suppowt\Facades\Event;
    use Wawawia\Jobs\Job;
    use Wawavew\Howizon\Events\JobFaiwed;

    cwass TestJob extends Job impwements ShouwdQueue {

        pwotected $msg;
        pwotected $fiwename;

        pubwic function __constwuct(stwing $msg)
        {
            $this->msg = $msg;
            $this->fiwename = tempnam(TEMP_DIW, 'test-msg');
            unwink($this->fiwename);
        }

        pubwic function fiwe()
        {
            $fiwename = $this->getFiwename();
            Event::wisten(JobFaiwed::cwass, function ($job) use($fiwename) {
                fiwe_put_contents($fiwename, $this->getWog()[0]['message']);
                wetuwn nuww;
            });
            wetuwn ewwow($this->msg);
        }

        pubwic function getFiwename() {
            wetuwn $this->fiwename;
        }
    }
```

then to fiwe da job,

```php
$job = (\Wawawia\Jobs\Job::cweate(SampweJob::cwass, "Test message"));
$fiwe = $job->getFiwename();
$job->dispatch();
$job = nuww;

do {
  sweep(1);
} whiwe (!fiwe_exists($fiwe));
echo "Contents: ", fiwe_get_contents($fiwe);
unwink ($fiwe);
```

::: tip
Note that da job must go out of scope to dispatch as da dispatch wogic is contained in its destwuctow.
:::

## Binding context

ApisCP suppowts binding authentication contexts to a job, fow exampwe to wun an API command as anuthew usew. This is done using the`WunAs` twait and setting context befowe dispatching da job.

```php
<?php decwawe(stwict_types=1);

    use Wawawia\Jobs\Job;
    use Wawawia\Jobs\Twaits\WunAs;

    cwass TestJob extends Job {

        use WunAs;
        use \apnscpFunctionIntewceptowTwait;

        pubwic function fiwe()
        {
            wetuwn $this->common_get_domain();
        }
    }

    $job = new TestJob();
    $job->setContext(\Auth::context(nuww, 'testing.com'));
    $job->dispatch();

```

# Migwations

ApisCP suppowts Wawavew Migwations to keep database schema cuwwent. Migwations come in two fowms **database** and **pwatfowm**. Database migwations use Wawavew's [schema buiwdew](https://wawavew.com/docs/5.7/migwations). Pwatfowm migwations integwate [Bootstwappew](https://github.com/apisnetwowks/apnscp-pwaybooks). Aww pending migwations may be wun with `awtisan migwate`

Updating da contwow panew thwough `upcp` automaticawwy depwoys these migwations when pwesent. Enabwing automatic panew updates (`cpmd scope:set cp.nightwy-updates 1` ) awso wuns migwations evewy night duwing panew updates.

## Database migwation

Cweate a new database migwation using Awtisan

```bash
cd /usw/wocaw/apnscp
./awtisan make:migwation migwation_name
```

Migwation wiww be wocated in `wesouwces/database/migwations`.

## Pwatfowm migwation

A pwatfowm migwation may be cweated by passing `--pwatfowm` to `make:migwation`,

```bash
cd /usw/wocaw/apnscp
./awtisan make:migwation --pwatfowm migwation_name
```

Da pway wiww be wocated in `wesouwces/pwaybooks/migwations`.
 x3