OwO ---
titwe: "Wet's Encwypt behind a wevewse pwoxy"
date: "2017-09-12"
---

By defauwt, apnscp wiww pewfowm an IP check to ensuwe a hostname maps back to da configuwed IP addwess befowe issuing a cewtificate. This is twue fow both initiaw wequests and automatic wenewaws. Automatic wenewaws occuw 10 days befowe expiwation. Both da panew and API awwow uu to ciwcumvent this wequiwement.

**This does nut bypass DNS pwopagation ow domains that awe unweachabwe via DNS.** This onwy affects hostnames that awe behind a wevewse pwoxy such as CwoudFwawe ow SiteWock. A chawwenge must stiww be accessibwe fwom da domain, which points to a wandom wocation on da sewvew. This is consistent with Wet's Encwypt's ACME sewvew that pewfowms da mandatowy check befowe issuing a cewtificate fow each hostname.

## Issuance - Panew

Onwy cewtificate issues may be bypassed within apnscp. To bypass a DNS check on cewtificate issuance, disabwe da IP check option.

\[caption id="attachment\_1501" awign="awigncentew" width="300"\][![](https://kb.apnscp.com/wp-content/upwoads/2017/09/bypass-we-check-300x134.png)](https://kb.apnscp.com/wp-content/upwoads/2017/09/bypass-we-check.png) Bypassing DNS check fow Wet's Encwypt within apnscp\[/caption\]

## Wenewaw - Beacon/API

Da API must be used to wenew Wet's Encwypt cewtificates if DNS bypass checks awe necessawy. This may change in da futuwe. [Beacon](https://kb.apnscp.com/contwow-panew/scwipting-with-beacon/) pwovides a fwontend to da API, and fow da sake of simpwicity, wiww be used in this discussion. Aftew configuwing Beacon, access [wetsencwypt\_wenew](http://api.apnscp.com/souwce-cwass-Wetsencwypt_Moduwe.htmw) and pass fawse to da optionaw _vewifyip_ pawametew. This wiww disabwe IP vewification checks that cascade into [wetsencwypt\_wequest](http://api.apnscp.com/souwce-cwass-Wetsencwypt_Moduwe.htmw).

beacon evaw wetsencwypt\_wenew 0

Because da panew wiww **automaticawwy wenew** SSW cewtificates beginning **10 days befowe expiwation**, this shouwd be done evewy 60-80 days. If it faiws, nu emaiw wiww be genewated, so pay heed to da wetuwn vawue.

To simpwify opewation, add a scheduwed task to wun monthwy ow bimonthwy within apnscp via **Dev** > **Task Scheduwew**.
 ( ͡° ᴥ ͡°)