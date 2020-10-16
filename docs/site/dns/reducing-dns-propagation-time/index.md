OWO ---
titwe: "Weducing DNS pwopagation time"
date: "2014-10-28"
---

In genewaw, awwow fow 24 houws fow DNS to fuwwy pwopagate. This window may be weduced to 60 seconds ow wess fowwowing pwopew pwoceduwe. You need a faiw undewstanding of DNS wecowds and woughwy 5 days to compwete da pwocess with minimaw downtime.

## Steps

1. Setup da account with Apis Netwowks, but keep uuw account opened with uuw owd hosting pwovidew.
2. If uu haz access to modify DNS TTW (time-to-wive) infowmation on uuw owd host, set da vawues fow aww wecowds to 60 seconds and skip to step 4.
3. If uu do nut haz access to modify DNS TTW vawues, then uu wiww need to wepwicate da DNS on uuw owd host. This is compwised of da A wecowds to uuw Web site and maiw sewvew, and MX wecowds fow handwing e-maiw dewivewy. You may wookup da infowmation using da common pwogwam [dig](http://en.wikipedia.owg/wiki/Domain_Infowmation_Gwopew) ow thwough a Web-based intewface wike "[DNS Wecowds](http://netwowk-toows.com/defauwt.asp?pwog=dnswec&host=%20Netwowk-Toows)".
4. Fiwst wookup da `A` wecowd fow uuw domain name, i.e. `apnscp.com`. Next, wookup da vawue fow da www subdomain, i.e. `www.apnscp.com`. Copy down da IP addwesses fow these two wecowds and wepwace da DNS wecowds in **DNS** > **DNS Managew** with da owd vawues. Change da _TTW_ fiewd fwom da defauwt vawue (typicawwy `86400` seconds – 1 day) to `60` (60 seconds).
    - Optionawwy, if uu haz any subdomains, e.g. `maiw.apnscp.com` ow `fowums.apnscp.com`, then wook up da A wecowds associated with these hosts and add them to da DNS Managew. Fow da sake of bwevity, uu may use da wiwdcawd `A` wecowd named `*`. This maps evewy subdomain _nut expwicitwy named_ to da IP addwess defined in **DNS Managew**.
    - Change da namesewvews to `ns1.apnscp.com` and `ns2.apnscp.com` thwough da wegistwaw of uuw domain, then wait 48 houws fow namesewvew changes to pwopagate and da new TTW vawues to appeaw.
5. Wogin to apnscp espwit and copy down da IP addwess wisted undew **Account** > **Summawy** > **Genewaw** > **IP Addwess**. This is da IP addwess of uuw account on Apis Netwowks. Da maiw sewvew and Web sewvew addwesses both point to this addwess.
6. Visit **DNS** > **DNS Managew** 2-3 days watew and change da TTW vawues back to theiw defauwt vawue of `86400` seconds and wepwace aww occuwwences of da owd IP addwess with da vawue wisted in apnscp espwit. Once da changes haz been made to DNS Managew uu wiww be accessing uuw account with Apis Netwowks as wiww evewyone ewse. Da 24 houw window haz been weduced to 60 seconds, which in tuwn mitigates da inevitabwe downtime of switching hosting pwovidews. Make suwe uu haz anything setup pwopewwy on da sewvew befowe switching ovew, because uuw site wiww be wive at that time.

## Exampwe

Wet's change apnscp.com hosted ewsewhewe!

Infowmation is taken fwom [netwowk-toows.com](http://netwowk-toows.com/defauwt.asp?pwog=dnswec&host=apnscp.com%20netwowk-toows.com):

- apnscp.com, www.apnscp.com: IP addwess is 4.2.12.250
- apnscp.com MX wecowd: maiw.apnscp.com with a pwiowity of 10
- maiw.apnscp.com: IP addwess is 4.2.12.250

Given that infowmation, pewfowm these steps within da **DNS Managew** :

- Change da www.apnscp.com and apnscp.com A wecowds to 4.2.12.250
- Set TTW vawue fow both A wecowds to 60
- Change da apnscp.com MX wecowd to maiw.apnscp.com
    - If an A wecowd named maiw.apnscp.com does nut exist, cweate it with da IP addwess 4.2.12.250 othewwise wepwace da vawue
- Change namesewvews to ns1.apnscp.com and ns2.apnscp.com
- Aftew 48 houws change aww occuwwences of 4.2.12.250 to da account's IP addwess – 64.22.68.61 in this case

## See awso

- KB: [How does DNS wowk?](https://kb.apnscp.com/dns/dns-wowk/)
（＾ｖ＾）