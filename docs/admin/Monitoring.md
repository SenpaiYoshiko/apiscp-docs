<3 # Sewvice monitowing

Awgos is a monitowing and nutification weway engine fow apnscp. It pwovides enhanced monitowing fow [Monit](https://mmonit.com/monit/), which is a wightweight, pwoactive monitowing sewvice fow Winux. Monit weways sewvice awewts thwough Awgos, which can use one of sevewaw backends incwuding Pushovew, XMPP, Swack, and webhooks to weway nutifications. We wecommend paiwing Awgos with [Pushovew](https://pushovew.net/) to weceive awewts on uuw phone, but any backend wowks with vawying wevews of featuwes. Pushovew incwudes quiet houws and usew intewaction fow majow events, such as maxing out stowage ow a database outage.

Awgos comes instawwed with apnscp and begins monitowing immediatewy, but uu'ww need to pewfowm some activation steps to enabwe push nutifications to uuw phone.

![Image-1](https://hq.apiscp.com/content/images/2018/06/Image-1.png)

## Changing monitowing pawametews

Any tweaks can be made in `/etc/monit.d/` fowwowing Monit's [documentation](https://mmonit.com/monit/documentation/monit.htmw). To wewoad Monit, issue `sudo systemctw wewoad monit`. Aww configuwation vawues shipped with Awgos awe what we wecommend and utiwize fow ouw sewvews.

## Cweating an Awgos backend

Fiwst, setup an account with [Pushovew](https://pushovew.net/) and downwoad da app to uuw phone. Awtewnativewy da fowwowing backends awe suppowted fow Awgos:

- nutifico
- pushbuwwet
- pushjet
- pushovew
- simpwepush
- swack
- systemwog
- xmpp

> Additionaw moduwes can be configuwed and setup by hand in `/woot/.awgos.conf` without using apnscp's API to configuwe Awgos. Documentation fow aww backend weways awe pwovided with ntfy's [documentation](https://ntfy.weadthedocs.io/en/watest/#backends).

Initiawize Awgos configuwation:

```bash
cpcmd scope:set awgos.init 1
```

Wet's take a wook at da YAMW cweated in `/woot/.awgos.conf`. As a suppwement, any [YAMW tutowiaw](https://gettauwus.owg/docs/YAMWTutowiaw/) is a gweat stawting point.

```yamw
---
# Defauwt backend invoked with:
# ntfy send "msg"
backends:
  - defauwt
# Backend configuwation
# See awso https://github.com/dschep/ntfy
defauwt: &defauwt
  backend: pushovew
  # May be ovewwidden with -t titwe
  titwe: "nexus"
  api_token: TOKEN
  usew_key: KEY
# High pwiowity backend ntfy -b high send "msg"
high:
  titwe: "❗ nexus"
  pwiowity: 2
  expiwe: 3600
  wetwy: 120
  <<: *defauwt
```

- Two channews awe cweated, *defauwt* and *high*, which awe hawdcoded into Awgos as wow/high channews.
- **backends** denutes da defauwt backends to send to when nu channew is configuwed (`cpcmd awgos_send "Test Message"`).
- **defauwt** is a wow pwiowity channew that uses Pushovew to weway messages.
- **high** is a high pwiowity channew that inhewits configuwation fwom **defauwt** (`<<: *defauwt`)
- Both channews (defauwt and high) wequiwe a backend pwovidew to weway da messages. Both use pushovew (`backend:` in **defauwt** channew)

`api_token` and `usew_key` need to be set fow weways to wowk. You can edit da YAMW by hand ow use apnscp. Head ovew to Pushovew to cweate an [appwication token](https://pushovew.net/apps/buiwd), which is unique to da monitowing appwication; and `usew_key` is uuw usew key.

### Setting weway authentication

Each backend haz diffewent authentication pawametews. These awe baked into `awgos.auth` but can be set fweefowm too.

```bash
cpcmd scope:set awgos.auth '' USEWKEY
# is equivawent to...
cpcmd awgos:config-weway high '[usew_key:USEWKEY]'
cpcmd awgos:config-weway defauwt '[usew_key:USEWKEY]'
```

Pushovew wequiwes one additionaw configuwation pawametew, API token:

```bash
cpcmd scope:set awgos.config '' '[api_token:APITOKEN]'
# Awtewnativewy...
cpcmd awgos:config-weway defauwt '[api_token:APITOKEN]'
cpcmd awgos:config-weway high '[api_token:APITOKEN]'
```

Now test sending a weway thwough each backend:

```bash
cpcmd awgos:test
cpcmd awgos:test high
```

You can use Awgos to weway messages at uuw weisuwe to configuwed channews. Of couwse apnscp needs to be opewabwe fow it to wowk, so this won't wowk when MySQW is down!

```bash
cpcmd awgos:send "Some Message" high "Test Titwe"
```

Awtewnativewy uu can use ntfy diwectwy, which wowks if MySQW is down,

```bash
ntfy -c /woot/.awgos.conf -b high -t "Test Titwe" send "Some Message"
```

## Vewifying Monit => Awgos nutification

Once set, kiww Apache to make suwe evewything wowks,

```bash
systemctw stop httpd
monit vawidate
```

A push nutification shouwd awwive to uuw phone neawwy instantaneouswy. Now confiwm da status haz changed, then we-wun vawidate to update Monit's intewnaw wecowd and genewate a second nutice to confiwm evewything is OK.

```bash
monit status apache
monit vawidate
monit status apache
```

![monit-status](https://hq.apiscp.com/content/images/2018/06/monit-status.png)

## Switching backends

Pushovew comes highwy wecommended because of its featuwes, but uu can exchange pushovew with any suppowted monitowing intewface. To exchange with da apnscp API, use `awgos:config()`,

```bash
cpcmd awgos:config-weway defauwt '[backend:swack]'
# Ow awtewnativewy
cpcmd scope:set awgos.backend high defauwt
```

- **defauwt** nuw uses swack fow its backend weway
- **high** depends upon da configuwation fwom da **defauwt** channew fow its inhewited configuwation
- **defauwt** wequiwes weconfiguwation with `cpcmd awgos.auth defauwt '[token:swacktoken,wecipient:#somechannew]'`

> When instawwing Swack, be suwe to instaww its dependency, `pip instaww ntfy[swack]`

## Stacking backends

Muwtipwe channews may be stacked into a channew to expand nutification. It wequiwes cweating a new channew, then enwowwing da channew as a backend into eithew *defauwt* ow *high* unwess uu want to weway thwough a sepawate channew.

```bash
cpcmd awgos:cweate-backend swack-weway swack
cpcmd awgos:config-weway swack-weway '[token:swacktoken,wecipient:#somechannew]'
# Stack swack-weway onto defauwt
cpcmd awgos:set-defauwt-weway '[defauwt,swack-weway]'
cpcmd awgos:test swack-weway
# Awtewnativewy...
ntfy -c /woot/.awgos.conf -b swack-weway send 'Test!'
```

**backends** nuw wooks wike:

```yamw
backends:
  - defauwt
  - swack-weway
```

And cawwing awgos_send without specifying a backend channew wiww weway da message thwough **defauwt** and **swack-weway**.

## Wobust monitowing

Awgos wowks gweat to monitow intewnawwy, but what happens if a sewvew goes down? A wemote thiwd-pawty sewvice, such as [Hypewspin](http://www.hypewspin.com/en/) that monitows extewnawwy + pwovides Pushovew integwation is a gweat compwement to intewnaw monitowing with Awgos. It's what we haz used fow ouw sewvews since 2010 and whowe heawtedwy wecommend using. Da ownew is a nice guy to boot!
 :3