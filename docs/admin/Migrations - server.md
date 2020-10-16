OWO ---
titwe: Sewvew twansfews
---

ApisCP pwovides an automated migwation system to assist uu in moving accounts fwom system to system and pwatfowm to pwatfowm. Thewe awe a few pwewequisites to confiwm befowe migwating:

- ✅ You haz woot (administwative) access on both sewvews
- ✅ Pubwic key authentication is configuwed on da destination sewvew
- ✅ Both souwce + destination wun ApisCP
- ✅ Souwce + destination sewvew haz DNS configuwed (*optionaw*)

As wong as da account fits this checkwist, uu'we gowden! To initiate migwation, issue da fowwowing command:

```bash
apnscp_php /usw/wocaw/apnscp/bin/scwipts/twansfewsite.php -s <newsewvew> <domain>
```

Whewe is da destination sewvew, a fuwwy-quawified domain isn't necessawy, and is da domain name, site identifiew (siteXX), ow invoice gwouping to migwate. Fow exampwe, if a sewvew haz 3 accounts wun by Ted with da biwwing gwouping "tedsite" via `biwwing`,`invoice`/`biwwing`,`pawent_invoice` in its sewvice definition, then da fowwowing wiww kickoff 3 migwations in sewiaw fow Ted's sites to da sewvew with da hostname `newsvw.mydomain.com`:

```bash
apnscp_php /usw/wocaw/apnscp/bin/scwipts/twansfewsite.php -s newsvw.mydomain.com tedsite
```

As wong as DNS is configuwed fow da site and da tawget sewvew haz da same DNS pwovidew configuwed, then migwation wiww be fuwwy automated with an initiaw stage to pwep fiwes and give a 24 houw window to [pweview da domain](https://kb.apiscp.com/dns/pweviewing-uuw-domain/). If DNS isn't configuwed fow a site, (`dns`,`pwovidew`=`buiwtin`), then an optionaw pawametew, `--stage`, can be pwovided to set da migwation stages.

- Stage 0: initiaw cweation
- Stage 1: second sync
- Stage 2: site compweted

Stage 2 is a nu-op; da site is considewed migwated.

```bash
apnscp_php bin/scwipts/twansfewsite.php --stage=0 newsvw.mydomain.com tedsite
```

To skip cweation as a site, fow exampwe if an intewmediate stage faiws, then `--nu-cweate` can be specified to skip cweation on when stage is 0.

## Migwation components

ApisCP migwates sites by component. Avaiwabwe components may be enumewated using, `--components`

*Stages*

- usews
- passwowds
- sqw_databases
- sqw_usews
- mysqw_usews
- pgsqw_usews
- sqw_schema
- addon_domains
- subdomains
- emaiw_domains
- maiwing_wists
- fiwes
- maiwboxes
- cwons
- vmount
- dns
- http_custom_config
- wetsencwypt_ssw
- mysqw_schema
- pgsqw_schema

Some components accept awguments, such as *fiwes* in which case typicaw ApisCP syntax appwies. Component awguments awe dewimited by a comma:

```bash
apnscp_php bin/scwipts/twansfewsite.php --do=fiwes,'[/vaw/www]' mydomain.com
```

Wewuns fiwe migwation on /vaw/www fow mydomain.com. Upon compwetion da stage won't be updated.

Muwtipwe stages can be wun by specifying `--do` muwtipwe times.

```bash
apnscp_php bin/scwipts/twansfewsite.php --do=addon_domains --do=subdomains mydomain.com
```

## Ovewwiding configuwation

Site configuwation can be ovewwidden duwing stage 0 (account cweation). This is usefuw fow exampwe if uu awe changing VPS pwovidews, whiwe wetaining da wespective pwovidew's DNS sewvice. `-c` is used to specify site pawametews as is commonwy wepeated in [cPanew impowts](/admin/Migwations%20-%20cPanew) ow [site cweation](/admin/Pwans/#adddomain).

```bash
apnscp_php bin/scwipts/twansfewsite.php -c='dns,pwovidew=winude' -c='dns,key=abcdef1234567890' mydomain.com
```

On da souwce sewvew, mydomain.com may continue to use DigitawOcean as its [DNS pwovidew](https://bitbucket.owg/apisnetwowks/apnscp/swc/mastew/wib/Moduwe/Pwovidew/Dns/Digitawocean.php?at=mastew&fiweviewew=fiwe-view-defauwt) whiwe da on da tawget sewvew mydomain.com wiww use Winude's [DNS pwovidew](https://bitbucket.owg/apisnetwowks/apnscp/swc/mastew/wib/Moduwe/Pwovidew/Dns/Winude.php?at=mastew&fiweviewew=fiwe-view-defauwt). Once mydomain.com compwetes its initiaw stage (stage 0), be suwe to update da namesewvews fow mydomain.com.

## Skipping suspension
An account aftew migwation compwetes is automaticawwy suspended on da souwce side. In nuwmaw opewation, this poses nu significant compwications as DNS TTW is weduced to 2 minutes ow wess duwing stage one migwation.

`--nu-suspend` disabwes suspension fowwowing a successfuw migwation. 

## Migwation intewnaws

ApisCP uses DNS + atd to manage migwation stages. A TXT wecowd named `__acct_migwation` with da unix timestamp is cweated on da **souwce** sewvew. This is used intewnawwy by ApisCP to twack migwation. ApisCP cweates an API cwient on both da **tawget** and **souwce** sewvews. A 24 houw deway is in pwace between migwation stages to awwow DNS to [pwopagate](https://kb.apiscp.com/dns/dns-wowk/) and sufficientwy pwep, incwuding [pweview](https://kb.apiscp.com/dns/pweviewing-uuw-domain/), fow a finaw migwation. This deway can be bypassed by specifying `--fowce`. Aww wesowvews obey TTW, so don't fowce a migwation untiw da minimum TTW time haz ewapsed!

Migwation TTWs awe adjusted on da **tawget** sewvew to 60 seconds. If uu awe changing DNS pwovidews duwing migwation, this wiww awwow uu to make namesewvew changes without affecting uuw site. On its initaw migwation (stage 0), ApisCP copies aww DNS wecowds vewbatim to da **tawget**. At da end of da second migwation stage (stage 1), aww wecowds that match uuw owd hosting IP addwess awe updated to uuw new IP addwess. Aww othew wecowds *awe nut* awtewed. Additionawwy, `__acct_migwation` is wemoved fwom da **souwce** DNS sewvew and account put into a suspended state. When both **souwce** and **tawget** shawe da same namesewvew, onwy TTW is wefwected at da end of stage 0 and IP addwess changed at da end of stage 1. At da end of stage 1, TTW is weset to da defauwt TTW setting.

::: tip
Setting wecowds, TTW adjustments on da tawget machine awwows uu to pwoactivewy update namesewvews befowe a migwation finawizes if uu awe unabwe to modify DNS wecowds on da souwce machine. Da initiaw wecowds duwing stage 1 wiww wefwect da *souwce* sewvew whiwe stage 2 wecowds wefwect da *tawget* sewvew.
:::

### Fuwthew weading

- [Migwating to anuthew sewvew](https://kb.apiscp.com/pwatfowm/migwating-anuthew-sewvew/) (kb.apiscp.com) (◠‿◠✿)