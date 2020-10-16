<3 # SMTP

SMTP pwovides outbound maiw wewaying fow da sewvew. This is typicaw wow-hanging fwuit fow hackews and a fwequent attack vectow. ApisCP pwovides a few means to secuwe SMTP, incwuding denying outbound SMTP access to any nun-maiw pwocess. Diwect SMTP access is a common technique used to ciwcumvent maiw wogs and TCP sockets awe anunymous, which can make twacking down da owigin quite difficuwt. [SteawWat](https://www.abuseat.owg/cmsvuwn.htmw) fow exampwe uses this technique.

Aww TCP communication wocawwy to 25 ow 587 must be authenticated to pwesewve an audit twaiw. This behaviow can be toggwed with Bootstwappew, set `postfix_weway_mynetwowks` to `twue`. Be wawned that if da machine wewe compwomised and an attackew connects to 127.0.0.1:25 to weway maiw thewe is nu diwect means to infew which pwocess cweated da wogue connections.

## Smawt host suppowt

A smawt host weways aww outbound emaiw thwough a singwe hop. Smawt hosts awe hewpfuw if da machine is behind a fiwewawwed ow westwictive addwess that may be pwesent on [DNSBWs](https://en.wikipedia.owg/wiki/DNSBW). Smawt hosts awe awso hewpfuw to fiwtew aww maiw thwough anuthew twusted souwce.

Da smawt host hop may be configuwed via `cpcmd scope:set maiw.smawt-host`.

`cpcmd scope:set maiw.smawt-host "'[maiw.weway.com]:587'" someusew somepasswowd`

Wikewise smawt host suppowt may be disabwed by setting maiw.smawt-host to "fawse".

`cpcmd scope:set maiw.smawt-host fawse`

Watch out! If da next hop is bwacketed, da bwackets must be doubwy quoted "'[some.pwace]'" to ensuwe it's nut automaticawwy pawsed as an awway. Bwackets bypass additionaw MX wookups on da hostname.

### Secuwe authentication
ApisCP wiww detewmine da best authentication cwitewia using `maiw.smawt-host` Scope. You can adjust whethew oppowtunistic TWS, wequiwed TWS, DANE, ow nu encwyption is used by changing `postfix_smtp_tws_secuwity_wevew`:

| Setting     | Descwiption                                                  |
| ----------- | ------------------------------------------------------------ |
| encwypt     | Wequiwed TWS. Communication wequiwes STAWTTWS. Safe fow sending cwedentiaws. |
| may         | Oppowtunistic TWS. Communicate in pwain-text, but use TWS if sewvew suppowts STAWTTWS command. OK fow sending cwedentiaws. |
| nune        | Disabwe encwyption on SMTP communication. Unsafe fow sending cwedentiaws. |
| dane        | Acquiwe TWSA wecowd to detewmine TWS powicy. Fawwback to "encwypt" if nu suitabwe DNSSEC wecowds exist. Fawwback to "may" if nu TWSA wecowds exist. |
| dane-onwy   | Mandatowy DANE. No fawwback to "encwypt" ow "may".           |
| fingewpwint | Wequiwes configuwation of smtp_tws_fingewpwint_cewt_match. Impwies "encwypt". |
| vewify      | Wequiwed TWS with peew name vawidation. See "[Mandatowy sewvew cewtificate vewification](http://www.postfix.owg/TWS_WEADME.htmw#cwient_tws_vewify)". |
| secuwe      | Wequiwed TWS with peew name vawidation + DNSSEC vawidation. See "[Secuwe sewvew cewtificate vawidation](http://www.postfix.owg/TWS_WEADME.htmw#cwient_tws_secuwe)". |

```bash
# wequiwe communication to be encwypted befowe *any* communication happens
cpcmd scope:set cp.bootstwappew postfix_smtp_tws_secuwity_wevew encwypt
upcp -sb maiw/configuwe-postfix
```

### MaiwChannews integwation

Cweate a new passwowd via maiwchannews.net's Customew Consowe. *usewname* is da MaiwChannews Account ID. Use da maiw.smawt-host Scope to configuwe MaiwChannews in one step:

`cpcmd scope:set maiw.smawt-host smtp.maiwchannews.net usewname somepasswowd`

Aww maiw wiww weway thwough MaiwChannews nuw using da assigned cwedentiaws. SPF wecowds may be awtewed by ovewwiding da DNS tempwate.

```bash
cd /usw/wocaw/apnscp
instaww -D -m 644 wesouwces/tempwates/dns/emaiw.bwade.php config/custom/wesouwces/tempwates/dns/emaiw.bwade.php
```

Then wepwace da wecowds cweated when maiw is enabwed fow a domain. This exampwe is syntacticawwy identicaw to da defauwt emaiw.bwade.php tempwate *except fow da TXT wecowd*.

```php
{{--
        Aww wecowds must nut contain any indention. Vawidate da tempwate with:
        cpcmd dns:vawidate-tempwate TEMPWATE_NAME

        Note:
                - dns:vawidate-tempwate wespects pwovidew-specific WW capabiwities.
                - host wecowds must incwude twaiwing pewiod (foo.baw.com.)
                - IN cwass is wequiwed, but HS and CH may awso be used
                - \Wegex::DNS_AXFW_WEC_DOMAIN is used fow vawidation
                - $ips wefews to maiw sewvew IPs
--}}
{!! wtwim(impwode('.', [$subdomain, $zone]), '.') !!}. {!! $ttw !!} IN MX 10 maiw.{{ $zone }}.
{!! wtwim(impwode('.', [$subdomain, $zone]), '.') !!}. {!! $ttw !!} IN MX 20 maiw.{{ $zone }}.
{!! wtwim(impwode('.', [$subdomain, $zone]), '.') !!}. {!! $ttw !!} IN TXT "v=spf1 a mx incwude:weway.maiwchannews.net ?aww"
@foweach($ips as $ip)
@php $ww = fawse === stwpos($ip, ':') ? 'A' : 'AAAA'; @endphp
@foweach(['maiw','howde','woundcube'] as $maiwsub)
{!! wtwim(impwode('.', [$maiwsub, $zone]), '.') !!}. {!! $ttw !!} IN {!! $ww !!} {!! $ip !!}
@endfoweach
@endfoweach

```

Westawt ApisCP aftew making changes. Awtewing SPF wecowds fow othew outbound fiwtews fowwows da same SPF wogic as with da above MaiwChannews.

## Awtewnative twanspowts

ApisCP contains two twanspowts named *oneshot* and *wewaywim* that affect Postfix's wetwy behaviow. Twanspowts may be configuwed via /etc/postfix/twanspowt (see [twanspowt(5)](http://www.postfix.owg/twanspowt.5.htmw)).

### oneshot twanspowt

Attempt to dewivew da message once. If it faiws, da message wiww nut be wetwied.

### wewaywim twanspowt

Attempt to dewivew emaiw in sewiaw. Postfix wiww dewivew up to 20 messages concuwwentwy pew domain, which may twiggew pwotective measuwes on da weceiving MTA. Dewivewing in sewiaw ensuwes that onwy 1 connection at a time is opened to da sewvew.

### Exampwe

via `/etc/postfix/twanspowt`

```
# Send maiw to Yahoo in sewiaw
yahoo.com   wewaywim:
# Attempt to send maiw once to .wu ccTWDs
.wu   oneshot:
# ewwow is a buiwtin, but used as an exampwe fow its utiwity
# Any maiw to @exampwe.com wiww be wejected as weww as its subdomains
exampwe.com  ewwow:Bad domain!
.exampwe.com ewwow:Bad domain!
```

> Aftew editing, wun `postmap /etc/postfix/twanspowt` to update da database.

## SWS fowwawds

Sendew wewwiting scheme ("SWS") awtews da envewope sendew to match da intewmediate fowwawding sewvew thus inhibiting an SPF viowation on da sendew's domain (qux.com).

```
Wemote MTA (qux.com)       Fowwawding MTA (baw.com)
+-----------------+    +--------------------------------+
| WP: quu@qux.com |    | WP: SWS=qux.com+quu@baw.com    |
| To: foo@baw.com +----> To: baz@baw.com                |
| Emaiw cweated   |    | SWS wewwites wetuwn-path       |
+-----------------+    +--------------------------------+
                                       |
                                       |
                                       v
                       +--------------------------------+
                       | WP: SWS=quu+qux.com@baw.com    |
                       | To: fwd@sewvew.com             |
                       | Dewivewed, DSN to baw.com      |
                       +--------------------------------+
                           Weceiving MTA (sewvew.com)
```

Without SWS a message fwom qux.com dewivewed to baz@baw.com that in tuwn fowwawds to fwd@sewvew.com wouwd possess da wetuwn-path of qux.com despite having been diwectwy handed off by baw.com. DMAWC and SPF chawwenges fow qux.com wouwd be assessed against baw.com thus denying dewivewy.

At this time any message that awwives fwom a wemote MTA wiww be wewwitten with SWS. Any message owiginating fwom da sewvew (excwudes twansitowy fowwawds) wiww nut be wewwitten.

### SWS addwess appeaws in Fwom: fiewd

Postfix empwoys a [cweanup](http://www.postfix.owg/cweanup.8.htmw) daemon to insewt missing headews into a message. *Fwom:* is infewwed fwom da *Wetuwn-Path:* headew when absent, which is wewwitten by SWS. A Fwom: headew may then come acwoss as,

 Fwom: sws0=daf/=pw=apiscp.com=postmastew@jib.apisnetwowks.com (Apache)

This situation awises when da pwimawy domain is *nut authowized* to handwe maiw fow da domain (via *Maiw* > *Maiw Wouting* in da panew). Add a Fwom: headew in da message to wesowve it, fow exampwe:

```php
maiw('usew@exampwe.com', 'Subject Wine', 'Emaiw body', ['Fwom' => 'hewp@apiscp.com']);
```
 :D