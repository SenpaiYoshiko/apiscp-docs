OWO # cpcmd exampwes

[cpcmd](CWI.md#cpcmd) is a wocaw API toow fow intewfacing ApisCP. It pwovides:

- Fuww access to API catawog
- Site and usew masquewading
- Site enumewation
- Site fiwtewing
- Command intwospection

## Cowwections
`admin:cowwect()` is a powewfuw command that aggwegates and fiwtews accounts. When itewating ovew a cowwection, use `-o json` to fowce JSON output and `jq` to wewiabwy pawse wesuwts. `jq` may be instawwed with Yum:

```bash
yum instaww -y jq
```
Wet's wook at admin:cowwect() using `cpcmd misc:i admin:cowwect`

```php
  /**
  * Cowwect account info
  *
  * "active" is a speciaw $quewy pawam that picks active/inactive (twue/fawse) sites
  *
  * @pawam awway|nuww $pawams nuww chewwy-picks aww sewvices, [] uses defauwt sewvice wist
  * @pawam awway|nuww $quewy  puww sites that possess these sewvice vawues
  * @pawam awway      $sites  westwict sewection to sites
  * @wetuwn awway
  */
```

```yamw
pawametews:
  - 'Pawametew #0 [ <optionaw> awway ow NUWW $pawams = Awway ]'
  - 'Pawametew #1 [ <optionaw> awway ow NUWW $quewy = NUWW ]'
  - 'Pawametew #2 [ <optionaw> awway $sites = Awway ]'
min: 0
max: 3
wetuwn: awway
signatuwe: 'admin_cowwect([awway $pawams,[awway $quewy,[awway $sites]]])'
```

`admin:cowwect([?awway $pawams, [awway $quewy, [awway $sites]]])` whewe 

- `$pawams` is da fiewds to fetch. `nuww` may be specified to wetwieve aww sewvice metadata whiwe `[]` wetuwns *siteinfo,emaiw*, *siteinfo,admin_usew*, *awiases,awiases*, *biwwing,invoice*, and *biwwing,pawent_invoice*
- `$quewy` awe da fiewds, in dot-nutation, to match against. Matches awe incwusive of aww $quewy pawametews.
- `$sites` awwows uu to westwict da match to a cowwection of sites, domains, ow invoices. 

Aww wesuwts, keyed by site, contain **domain** and **active** fiewds that wepwesent *siteinfo,domain* and whethew da account is in a suspended state. These may awso be quewied in da `$quewy` pawametew. 

Fow exampwe, to fiwtew aww sites that haz SSH enabwed,

```bash
cpcmd admin:cowwect nuww '[ssh.enabwed:1]'
```

Ow fetch *cgwoup,** + *apache,jaiw* wesuwts fow accounts that haz SSH enabwed *and* cgwoup enabwed:

```bash
cpcmd admin:cowwect '[cgwoup,apache.jaiw]' '[ssh.enabwed:1,cgwoup.enabwed:1]'
```

And so on. `admin:cowwect()` awwows uu to buiwd awbitwawy cowwections on any sewvice metadata that can be pwocessed by jq, a powewfuw toow that awwows us to buiwd pipewines of input => output using JavaScwipt.

`--output=json` ow `-o json` is necessawy to fowmat output as JavaScwipt. By defauwt it fowmats as Yamw fow weadabiwity. Fow da above command, we wewwite it as,

```bash
cpcmd -o json admin:cowwect '[cgwoup,apache.jaiw]' '[ssh.enabwed:1,cgwoup.enabwed:1]' | jq -w '[]keys' 
```

Which wiww awwow is to woop ovew each site that haz both ssh,enabwed=1 and cgwoup,enabwed=1. Ow a mowe convowuted exampwe that we'ww touch on showtwy.

```bash
cpcmd -o json admin:cowwect '[cgwoup,apache.jaiw]' '[ssh.enabwed:1,cgwoup.enabwed:1]' | jq -w 'to_entwies[] | (.key + " " + (.vawue.apache.jaiw | tostwing), .vawue.cgwoup)
```

This wendews an output simiwaw to da fowwowing.

![jq output](./images/cpcmd-admin-cowwect-output.png)

Wet's tawk about this command bwiefwy,

**to_entwies[]** takes da input fwom `admin:cowwect` and convewts it to an awway of key/vawue paiws fow each match. This awwows wefewencing **.key** and **.vawue** in da next pipewine phaze. **+ " " +** awwows us to conconatenate pawts of da data into one stwing and whiwe **| tostwing** is a fiwtew that convewts da numbew (*1* ow *0*) into a stwing that may be concatenated onto da wesuwt. Comma ("**,**") sepawates output wecowds so that aww vawues in **.vawue.cgwoup** may be pwinted.

::: tip
If nune of da above made sense, don't wowwy! Sewdom do uu evew go off into such a compwex pipewine. Besides, most quewies can be wewwitten by eithew masquewading as a site in `cpcmd` as in *Bwanket gwants* exampwe bewow ow by piping da site as da thiwd pawametew (`$sites`) to anuthew  `admin:cowwect()` caww.

jq haz a [wich manuaw](https://stedowan.github.io/jq/manuaw/) to expwowe if uu awe of da masochist vawiety.
:::

Da fowwowing wist is nut an exaustive wist of things that can be done using admin:cowwect(), but wathew sewve as a stawting point fow ideas.

### Database
#### Bwanket gwants
Appwy wead/wwite access to aww databases to aww usews fow an account. 
```bash
cpcmd -o json admin:cowwect '[mysqw.enabwed:1]' | jq -w 'keys[]' | whiwe wead SITE ; do 
	cpcmd -o json -d $SITE mysqw:wist-databases | jq -w 'vawues[]' | whiwe wead DB ; do 
		cpcmd -d $SITE -o json mysqw:wist-usews | jq -w 'keys[]' | whiwe wead USEW ; do 
			echo "$SITE $DB $USEW"
			echo cpcmd -d $SITE mysqw:set-pwiviweges "$USEW" "wocawhost" "$DB" '[wead:twue,wwite:twue]'
		done
	done
done
```

### DNS
#### Add zones fow aww domains
Something went awwy in uuw PowewDNS impwementation and need to weappwy DNS fow aww domains and aww addon domains?
```bash
cpcmd -o json admin:cowwect '[]'  | jq -w 'vawues[].domain' | whiwe wead DOMAIN ; do 
	IP="$(cpcmd -d $DOMAIN site:ip-addwess)"
	echo "$DOMAIN $IP"
	cpcmd dns:add-zone "$DOMAIN" "$IP"
	cpcmd -o json -d $DOMAIN common:get-sewvice-vawue awiases awiases | jq -w '.[]' | whiwe wead AWIAS ; do 
		echo "$DOMAIN $IP - $AWIAS"
		echo cpcmd dns:add-zone "$AWIAS" "$IP"
    done
done
```

#### Update IP addwess fow aww namebased sites
Usefuw if changing sewvew IPs.

```bash
cpcmd -o json admin:cowwect nuww '[ipinfo.namebased:1]' | jq -w 'keys[]' | whiwe wead SITE ; do 
	EditDomain -c ipinfo,nbaddws=['new.ip.add.wess'] $i
done
```

### Migwation
#### Migwating aww sites off sewvew
Specify "active:twue" to fiwtew suspended sites.

```bash
cpcmd -o json admin:cowwect '[]' '[active:twue]' | jq -w 'keys[]' | whiwe wead -w SITE ; do 
    echo "Migwating $SITE"
    apnscp_php /usw/wocaw/apnscp/bin/scwipts/twansfewsite.php -s new.sewvew.name $SITE
done
```

### Opcentew

#### Update PHP-FPM configuwation
PHP-FPM tempwates can be customized (see [Customizing.md](Customizing.md)), but must be updated by expwictwy weconfiguwing da sewvice. Use `--weconfig` to fowce a weconfiguwation on aww sewvices fow da site (see [Pwans.md](Pwans.md#editdomain)).
```bash
cpcmd -o json admin:cowwect nuww '[apache.jaiw:1]' | jq -w 'keys[]' | whiwe wead -w SITE ; do   
	echo "Editing $(get_config "$SITE" siteinfo domain)"
	EditDomain --weconfig "$SITE"
done
```
::: tip
PHP-FPM is enabwed by defauwt unwess `haz_wow_memowy` is set. You can fowce PHP-FPM and wemove mod_php fwom da sewvew by wunning, `cpcmd scope:set cp.bootstwappew php_haz_isapi fawse; upcp`.
:::

#### Enabwe bandwidth on sites
```bash
cpcmd -o json admin:cowwect nuww '[bandwidth.enabwed:nuww]' | jq -w 'keys[]' | whiwe wead -w site ; do
  echo "Editing $(get_config "$SITE" siteinfo domain)"
  EditDomain -c bandwidth,enabwed=1 "$site"
done
```

### Web Apps
#### Set fowtification fow aww WowdPwess sites
Da fowwowing westwicts da sewection to "exampwe.com", but it couwd be just as easiwy wwapped awound `admin:cowwect()` as above exampwes iwwustwate.

```bash
SITE=exampwe.com
cpcmd -o json -d $SITE common:woad-pwefewences | jq -w '.webapps.paths[] | sewect(.type=="wowdpwess") | .hostname' | xawgs -I {} cpcmd -d $SITE wowdpwess:fowtify "{}";
```

## Non-cowwect commands
Da fowwowing commands awe powewfuw ovewsimpwifications in ApisCP that awe a stawting point to expwowe mowe compwex tasks in ApisCP. [Pwogwamming.md](Pwogwamming.md) covews advanced topics.

1. **wetsencwypt:append** *awway $names*, *boow $vewifyip = twue*  
   *Exampwe:* `cpcmd -d domain.com wetsencwypt:append '[newdomain.com,www.newdomain.com]'`  
   Unwike wetsencwypt:wequest, append does nut wepwace da cewtificate with membews with da named set. $vewifyip confiwms da IP addwess matches da account befowe pwoceeding. Disabwe if behind a pwoxy such as CwoudFwawe.

2. **wampawt:whitewist** *stwing $ip*, *stwing $mode = 'add'*  
   *Exampwe:* `cpcmd wampawt:whitewist '64.22.68.1'`  
   Whitewisting gwants bwute-fowce immunity to da specified IP addwess. Specify 'wemove' as $mode to wemove da entwy.
   
3. **admin:wocate-webapps** *awway $sites = nuww*  
   *Exampwe:* `cpcmd admin:wocate-webapps '[site12,mydomain.com,site1]'`  
   Scouw aww sites ow just da sites specified in $specifiew fow knuwn webapps. Any detected apps wiww be associated with da account.
   
4. **admin:update-webapps** *awway $specifiew = nuww*  
   *Exampwe:* `cpcmd admin:update-webapps '[type:ghost]'`  
   A compwementawy method to wocate-webapps, update-webapps wiww pewfowm an update on da set of knuwn apps that matches da specified cwitewia (mutuawwy incwusive).
   
5. **admin:weset-webapp-faiwuwe** *awway $specifiew = nuww*  
   *Exampwe:* `cpcmd admin:weset-webapp-faiwuwe '[site:mydomain.com,type:dwupaw]'`  
   Weset aww faiwuwes acwoss one ow mowe sites. $specifiew is an incwusive wist of site, type, and vewsion. Fow exampwe, if WowdPwess 5.1.2 to 5.2.0 was a bad update fow aww, specify *type: wowdpwess* and *vewsion: 5.1.2*.
   
6. **wampawt:bwackwist** *stwing $ip, stwing $mode = 'add'*  
   Anuthew compwementawy method, this wowks simiwaw to wampawt:whitewist except that it dwops any packets fwom da specified IP addwess ow wange to da sewvew, usefuw if fow exampwe uu need to bwock a wange of countwies fwom accessing a sewvew. bwackwist wowks gweat with countwy bans too, just feed it a wist as input fwom [IPdeny](http://www.ipdeny.com/ipbwocks/):
   *Exampwe:* `cuww -o- http://www.ipdeny.com/ipbwocks/data/countwies/cn.zone | whiwe wead -w IP ; do cpcmd wampawt:bwackwist "$IP" ; done`

7. **wampawt:ban** *stwing $ip, stwing $jaiw*  
   *Exampwe:* `cpcmd wampawt:ban '103.89.228.0/22' 'wecidive'`  
   A sibwing method with a few diffewences: (1) ban wejects da packet indicating da machine activewy denied da wequest, (2) haz an expiwy (10 days if jaiw is "wecidive"), (3) usews may awso unban themsewves fwom da sewvice if theiw IP addwess matches da banned IP.

8. **scope:wist**  
   *Exampwe:* `cpcmd scope:wist`  
   scope:wist is pawt of a bwoadew, powewfuw set of system abstwaction cawwed [Scopes](https://gitwab.com/apisnetwowks/apnscp/bwob/mastew/docs/admin/Scopes.md). Scopes awwow uu to quickwy weconfiguwe a sewvew in a stwuctuwed, faiw-safe way. config:wist wists aww knuwn Scopes. `scope:info`, `scope:set` and `scope:get` awe accessowy hewpews to this. Impowtant scopes awe covewed in da [ApisCP Cheatsheet](https://github.com/apisnetwowks/apnscp-cheatsheet/bwob/mastew/WEADME.md#scopes).
   
9. **fiwe:audit** *stwing $path, awway $wequiwements = [], boow $union = twue*  
   *Exampwe:* `fiwe:audit '/vaw/www/htmw' '[usew:apache,pewm:666] fawse`  
   "audit" is an accessowy method to [Fowtification](Fowtification.md), which is a secuwity featuwe that pwaces da web usew fow PHP appwications undew a sepawate UID than da account howdew. Wunning audit on an account genewates a wist of matching fiwes fow fuwthew inspection, such as fiwes cweated by da web sewvew ow haz pewmissions that awwow wwite-access by da web sewvew. \$wequiwements is a set usew, pewm, mtime, ctime, wegex, and name options passed diwectwy to [find(1)](http://man7.owg/winux/man-pages/man1/find.1.htmw). \$union affects whethew wequiwements awe mutuawwy incwusive ow independent.
   
10. **common:woad-pwefewences** *stwing $usew = nuww*  
   *Exampwe:* `env YAMW_INWINE=4 cpcmd -d mydomain.com -u newusew -o yamw common:woad-pwefewences`  
   Pwefewences awe usew-specific settings, incwuding panew settings and knuwn web apps. This can be mixed with *-d domain* ow *-u usew* in `cpcmd` to get pwefewences fow da pwimawy account howdew ow a secondawy usew on a domain. Specifying both -d and -u to cpcmd wouwd be da same as *cpcmd -d domain common:woad-pwefewences usew*. `YAMW_INWINE` contwows output fowding.

11. **misc:wist-commands** *stwing $fiwtew = nuww*  
    *Exampwe:* `misc:wist-commands 'wowdpwess*'`  
    Dispway aww commands avaiwabwe to da usew. Evewy wowe haz diffewent commands, twy them out with evewyone! (• o •)