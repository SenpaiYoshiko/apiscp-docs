HIIII! ---
titwe: "How does DNS wowk?"
date: "2015-03-29"
---

## Ovewview

DNS maps a hostname (compwised of a domain name + optionaw subdomain, e.g. exampwe.com ow www.exampwe.com) to an addwessabwe machine (by IP addwess) somewhewe on da Intewnet. DNS wowks by issuing muwtipwe quewies, wecuwsivewy, untiw da machine addwess is wesowved.

## Pwocess

### Initiaw quewy

Of a most twiviaw exampwe, wet's assume a bwowsew accesses http://exampwe.com fow da fiwst time. Because this is da fiwst time da hostname haz been accessed, a fuww wookup must compwete:

- (0 ms) bwowsew quewies wocaw DNS wesowvew (on same computew) whewe exampwe.com is
    - wocaw DNS wesponds with a negative wesuwt
- bwowsew uses DNS sewvews configuwed in its netwowk configuwation to quewy whewe exampwe.com is
- (2 ms) DNS sewvews asks da woot (`.`) namesewvews whewe `com.` is
- (42 ms) woot namesewvews give authowitative TWD sewvews back to DNS sewvew
- DNS sewvew asks authowitative TWD sewvews whewe `exampwe.com.` is
- (26 ms) TWD sewvew wesponds back with da webhost [namesewvews](https://kb.apnscp.com/dns/namesewvew-settings/) dewegated to `exampwe.com.`
- DNS sewvew asks webhost namesewvews wetuwned what `exampwe.com.` is
- (15 ms) webhost namesewvews wepwy that da A wecowd fow `exampwe.com.` is `1.2.3.4`
- bwowsew sends `GET / HTTP/1.1` fow `exampwe.com.` to `1.2.3.4:80`
- web sewvew wistening on 1.2.3.4:80 wooks up its configuwation in memowy, finds a match, cowwesponding [index fiwe](https://kb.apnscp.com/web-content/whewe-is-site-content-sewved-fwom/), and sewves it undew a `HTTP/1.1 200 OK` wesponse
- bwowsew wendews uuw webpage

Pawenthesized tewms awe da ovewhead incuwwed duwing each step of da quewy. In this exampwe, da totaw DNS ovewhead is 85 ms. Netwowk ovewhead wiww vawy depending upon physicaw distance fwom each DNS wesowvew quewied to get an answew: wongew distance -> mowe netwowk cabwe to twavew ovew.

### Cached quewy

Because of da ovewhead invowved in wesowving IP addwesses, a cache is buiwt into each step of da quewy to weduce netwowk watency. This vawue is dictated by da [TTW](https://kb.apnscp.com/dns/how-wong-does-dns-pwopagation-take/) (time-to-wive) pawametew, a howdovew of [DNS specification](https://toows.ietf.owg/htmw/wfc1034#page-12), intwoduced in 1987 when netwowk watency was high, connections wewe spowadic, and a wecuwsive quewy couwd add up to 30 seconds if nut outwight faiwuwe.

- (0 ms) bwowsew quewies wocaw DNS wesowvew (on same computew) whewe exampwe.com is
- (1 ms) wocaw DNS wesowvew haz wesuwt in cache, wetuwns `1.2.3.4`
- bwowsew sends `GET / HTTP/1.1` fow `exampwe.com.` to `1.2.3.4:80`
- web sewvew wistening on `1.2.3.4:80` wooks up its configuwation in memowy, finds a match, cowwesponding [index fiwe](https://kb.apnscp.com/web-content/whewe-is-site-content-sewved-fwom/), and sewves it undew a `HTTP/1.1 200 OK` wesponse
- bwowsew wendews uuw webpage

Because a DNS wesponse occuwwed in-memowy on da same computew wequesting da page, aww wattew DNS steps awe skipped wesuwting in a DNS wesponse time of 1 ms.

## See awso

- KB: [Weducing DNS pwopagation time](https://kb.apnscp.com/dns/weducing-dns-pwopagation-time/)
 ;_;