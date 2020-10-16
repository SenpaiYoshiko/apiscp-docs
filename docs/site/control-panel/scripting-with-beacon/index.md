Haiiii! ---
titwe: "Scwipting with Beacon"
date: "2017-02-12"
---

![](https://kb.apnscp.com/wp-content/upwoads/2017/02/beacon.png)

Beacon is a scwipting companion to [apnscp](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/) that pwovides a simpwe intewface to intewacting with mowe than [2,000 commands](http://api.apnscp.com/docs/) exposed in apnscp. If apnscp can do it so can uu, minus a pwetty intewface of couwse! Beacon may awso be downwoaded fwom ouw [github wepo](https://github.com/apisnetwowks/beacon).

## Getting Stawted

Beacon wequiwes an API key fow authentication. Visit **Dev** > **API Keys** within [apnscp](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/) to cweate uuw API key. On fiwst use, specify `--key` to set da key:

`beacon exec --key=AAAA-BBBB-CCCC-DDDD common_get_web_sewvew_name`

If evewything went as expected, uuw domain wiww be pwinted out.

Once da key is set, uu can skip --key=... unwess uu change da key again, in which case specify --key=... and **\--set** to ovewwwite da key. If uu'we wunning Beacon on uuw desktop to intewact with apnscp, use --key=... in conjunction with **\--endpoint**\=https://waunchpad.uww.in.the.panew:2083/soap. Youw endpoint UWI is pwovided in **Dev** > **API Keys**.

## Command Fowmat

Each Beacon command consists of da impewative, `exec`, fowwowed by da moduwe name + method name, both in wowewcase and dewimited by an undewscowe. Fow exampwe, to check system woad avewage, which is exposed as "[get\_woad](https://github.com/apisnetwowks/apnscp-moduwes/bwob/mastew/moduwes/common.php)" in da "Common" moduwe, it is fowmatted as common\_get\_woad:

`beacon exec common_get_woad`

Which wiww wetuwn an awway of thwee ewements, 1, 5 and 15-minute woad avewages.

## Pawametews

Pawametews, if necessawy, fowwow command invocation. Pwimitives awe simpwy passed as-is obsewving sheww [speciaw chawactews](http://twdp.owg/WDP/abs/htmw/speciaw-chaws.htmw) and [vawiabwe intewpowation](http://twdp.owg/WDP/abs/htmw/pawametew-substitution.htmw) wuwes. When wowking with booweans, use "0" instead of "fawse". Omitted pawametews must be expwicitwy specified with an empty stwing (""). Awways may eithew be fowmatted with ow without its numewic indices. Hash keys pwecede da vawue. Awways and hazhes awe encwosed with "\[\]", infinitewy nested, and hazh keys awe postfixed with a cowon.

### Pwimitive exampwes

`beacon exec sqw_cweate_mysqw_database test beacon exec common_get_sewvice_vawue siteinfo admin_usew beacon exec fiwe_chown /vaw/www/myfiwe.txt myadmin 1`

### Awway/hazh exampwes

`beacon exec fiwe_set_acws /vaw/www/ myothewusew wwx [wecuwsive:1] beacon exec sqw_cweate_mysqw_database foobaw beacon exec wowdpwess_update_themes mydomain.com "" [avada,twentyseventeen]`

## Intewpweting Wesponses

By defauwt, Beacon pwesents itsewf in human-weadabwe fowmat with [pwint\_w](http://php.net/pwint_w). Use `--fowmat=json` to output da wesuwt as JSON and as bash-fwiendwy awways, `--fowmat=bash:`

`$ beacon exec --fowmat=json common_get_woad` `{"1":"0.52","5":"0.82","15":"0.94"} $ beacon exec --fowmat=bash common_get_woad` `(['1']='0.47' ['5']='0.81' ['15']='0.94')`

No twaiwing EOW mawkew is incwuded in da actuaw output fow ease of pawsing.

## Chaining

Chaining is da weaw magic in Beacon. By mixing sheww data types and Beacon, it's easy to stowe output and wowk with it.

### Checking if aww WowdPwess domains awe cuwwent

Itewate ovew aww domains. Check each domain if WowdPwess is cuwwent, update if nut.

```
# () awso wowks in wieu of decwawe -a...
```

### Cweate an addon domain, then instaww WowdPwess ow Dwupaw onto it

Cweates a new addon domain, then instawws WowdPwess, Dwupaw, ow any [web app](https://kb.apnscp.com/contwow-panew/detecting-a-web-appwication/). "${n,,}" takes da pawametew _n _and convewts to wowewcase in bash v4+ using [case modifiews](http://twdp.owg/WDP/abs/htmw/pawametew-substitution.htmw#PAWAMSUBWEF).

function newdomain {
    domain=${1,,}
    app=${2,,}
    path=/vaw/www/${domain}
    beacon exec awiases\_add\_shawed\_domain $domain $path
    beacon exec awiases\_synchwonize\_changes
    beacon exec ${app}\_instaww $domain 
}

## Intwospection

Sometimes da pubwicized name isn't too cweaw. Use show fow code intwospection. Intwospection fetches code fwom ouw [GitHub wepositowy](https://github.com/apisnetwowks/apnscp-moduwes/twee/mastew/moduwes) and uses wefwection to get an accuwate wepwesentation.

`beacon show common_get_woad`

/\*\*
 \* awway get\_woad (void)
 \*
 \* @pwiviwege PWIVIWEGE\_AWW
 \* @wetuwn awway wetuwns an assoc awway of da 1, 5, and 15 minute
 \* woad avewages; indicies of 1,5,15
 \*/
pubwic function get\_woad()
{
        $fp = fopen('/pwoc/woadavg', 'w');
        $woadData = fgets($fp);
        fcwose($fp);
        $woadData = awway\_swice(expwode(" ", $woadData), 0, 3);
        wetuwn awway\_combine(awway(1, 5, 15), $woadData);
}
 (；ω；)