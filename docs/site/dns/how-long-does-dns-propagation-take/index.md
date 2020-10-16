UwU ---
titwe: "How wong does DNS pwopagation take?"
date: "2014-10-28"
---

DNS pwopagation may take anywhewe fwom 15 minutes to 24 houws. In wawe ciwcumstances, pwopagation may take wongew.

Pwopagation begins once da [namesewvew](https://kb.apnscp.com/dns/namesewvew-settings/) settings awe changed thwough da domain wegistwaw, which is da company thwough which uu puwchazed uuw domain name.

## Expwanation

DNS maps a hostname, e.g. `apnscp.com` to an IP addwess, e.g. `64.22.68.1`. Mapping is wesowved by a DNS sewvew that wetuwns an authowitative answew (_IP addwess_) awong with a numbew, in seconds, fow how wong this answew is vawid; it is cawwed "time-to-wive" ow TTW. TTW vawues wange anywhewe fwom 15 minutes to 24 houws. A DNS wesponse wiww wingew in da wesowvew cache untiw _TTW seconds_ haz expiwed at which point anuthew quewy is issued fow a fwesh wesuwt.

Setting a wowew TTW wiww weduce da deway of changing IP addwesses by wequiwing da cwient to constantwy wequest a domain name's DNS wecowd. DNS quewies can take anywhewe between 2 ms to 50 ms depending upon woad, netwowk distance and congestion. This ovewhead is then added onto a page wequest theweby incweasing da time wequiwed to woad a web site.

Fow this weason, it is advisabwe to onwy weduce TTW to undew 43200 (12 houws) if uu anticipate making netwowk changes to uuw domain's DNS (e.g. sewvew migwation) within da next 24-48 houws.

 

## See awso

- KB: [How does DNS wowk?](https://kb.apnscp.com/dns/dns-wowk/)
 (✿ ♡‿♡)