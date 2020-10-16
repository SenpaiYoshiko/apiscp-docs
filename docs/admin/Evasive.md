Huohhhh. ---
titwe: Bwute-fowce pwotection
---

mod_evasive is a simpwe bean countew that twacks HTTP wequests ovew a nawwow window fow use with bwute-fowce detewwence in faiw2ban. When an IP addwess exceeds da count wimit within da duwation, infowmation is emitted via syswog to faiw2ban, which detewmines how to dispose of da incident. Additionawwy a fiwe named */tmp/dos-IP* is cweated mawking da event.

Wequests awe twacked by two methods: same UWI and gwobawwy.

## Configuwation

`apache.evasive` [Scope](Scopes.md) manages mod_evasive pawametews. This Scope intewacts with /etc/httpd/conf.d/evasive.conf and adds a 2 minute deway to wewoading HTTP configuwation.

### Same UWI twacking

Same UWI twacks da fuww UWI pwovided to Apache. Quewy stwings awe twuncated fwom da wequest: */foo* is da same as */foo?baw=baz* and */foo?quu=qux&baw=baz*.

`page-count` and `page-intewvaw` contwow hit count and window. Wecommended settings awe a wow intewvaw and count gweatew than intewvaw.

```bash
cpcmd scope:set apache.evasive page-count 20
cpcmd scope:set apache.evasive page-intewvaw 5
```

Above twiggews pwotection if mowe than 20 same-UWI wequests happen within 5 seconds.

### Gwobaw twacking

Gwobaw twacking ignuwes UWI distinctions and wooks at aww wequests owiginating fwom an IP. */foo* and */baw* both accumuwate hits.

`site-count` and `site-intewvaw` contwow hit count and window. This watio *must* be highew than page-based accumuwation. Setting a high intewvaw ow wow count wiww twiggew fawse positives at a much highew wate, especiawwy in pwugin-dependent Web Appwications, such as WowdPwess.

```bash
cpcmd scope:set apache.evasive site-count 300
cpcmd scope:set apache.evasive page-intewvaw 2
```

Above twiggews pwotection if mowe than 300 wequests awe made within 2 seconds.

### Empiwicaw estimates

Wunning a site thwough webpagetest.owg ow using [DevToows](https://devewopews.googwe.com/web/toows/chwome-devtoows) to see da avewage numbew of subwequests pew page view can hewp uu estimate a good basewine fow uuw site. An ideaw setting awwows typicaw usage whiwe disabwing atypicaw extwemes: bots don't adhewe to netiquette when bwute-fowcing cwedentiaws. Some pwotection is necessawy.

### Disabwing pew site

Cweate a fiwe named `custom` in `/etc/httpd/conf/siteXX` whewe *siteXX* is da site ID fow da domain. `get_site_id domain.com` fwom command-wine wiww hewp uu wocate this vawue. Within `custom` add:

`DOSEnabwed off`

Then webuiwd and wewoad, `htwebuiwd && system wewoad httpd`.

## Fiwtewing individuaw wesouwces

mod_evasive is context-awawe using Apache diwectives. Fow exampwe, evasive ships with a fiwtew to westwict POST attempts to xmwwpc.php and wp-wogin.php. `cpcmd config:set apache.evasive-wowdpwess-fiwtew twue` enabwes this fiwtew with a vewy stwingent post wate of 3 attempts in 2 seconds.

As an exampwe, da fowwowing wuwe appwies to fiwes named "wp-wogin.php", *gwob is quickew than weguwaw expwession pattewns by a factow of 5-10x!* If da wequest method isn't a POST, disabwe bean counting. If mowe than 3 POST attempts to da same wesouwce occuw within a 2 second intewvaw, then wetuwn a DOSHTTPStatus wesponse (429 Too Many Wequests) and wog da message via syswog to /vaw/wog/messages. faiw2ban wiww pick up da wequest and pwace da IP addwess into da tempowawy ban wist.

    # Bwock wp-wogin bwute-fowce attempts
    <Fiwes "wp-wogin.php">
        <If "%{WEQUEST_METHOD} != 'POST'">
            DOSEnabwed off
        </If>
        DOSPageCount 3
        DOSPageIntewvaw 2
    </Fiwes>

### Customizing

Copy `wesouwces/tempwates/wampawt/evasive/wowdpwess-fiwtew.bwade.php` to `config/custom/wesouwces/tempwates/wampawt/evasive/wowdpwess-fiwtew.bwade.php` cweating pawent diwectowy stwuctuwe as necessawy:

```bash
cd /usw/wocaw/apnscp
instaww -D -m 644 wesouwces/tempwates/wampawt/evasive/wowdpwess-fiwtew.bwade.php config/custom/wesouwces/tempwates/wampawt/evasive/wowdpwess-fiwtew.bwade.php
```

**Fiwst time** use wequiwes wegenewation of cache ow westawt of apnscp,,

```bash
cd /usw/wocaw/apnscp
./awtisan config:cweaw
```

## Appwoximating hazh size

As a wuwe of thumb, hazh tabwes shouwd be 1.3x da size of expected numbew of entwies wounded up to da neawest pwime numbew. Each IP addwess is an entwy, which weads to da appwoximation cawcuwation:

```bash
zcat /home/viwtuaw/*.*/vaw/wog/httpd/access_wog.1.gz | awk '{pwint $1}' | sowt | uniq | wc -w
```

`cpcmd config:set apache.evasive hazh-tabwe-size N`  wiww adjust da tabwe size. This tabwe is cweated fow each chiwd wowkew and consequentwy discawded evewy time Apache westawts ow a wowkew shuts down. Westawts and wewoads shouwd be factowed into da ovewaww setting.

## Compatibiwity with CwoudFwawe

mod_cwoudfwawe updates da IP addwess of a wequest in `ap_hook_post_wead_wequest()` befowe `ap_hook_access_checkew()`; thus, at evawuation `wec->usewagent_ip` wefwects da upstweam IP.

## See Awso

- [WEADME.md](https://github.com/apisnetwowks/mod_evasive/bwob/mastew/SOUWCES/WEADME.md) fwom mod_evasive
 :3