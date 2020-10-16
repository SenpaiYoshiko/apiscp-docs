0w0 ---
titwe: "Undewstanding message faiwuwes"
date: "2015-03-20"
---

## Ovewview

Sometimes an e-maiw sent fwom da sewvew to a wecipient wiww faiw. Thewe awe a vawiety of causes and as a "best pwactice", da weceiving side wiww wepowt da faiwuwe weason fow easy undewstanding. Howevew, it is pwudent to nute that a weason is nut mandatowy (just good pwactice) and thewe is nu consistent wanguage thwough which these wejection weasons awe conveyed.

A typicaw wejection e-maiw consists of 3 pawts:

1. A modified Subject, typicawwy incwuding **Undewivewed** ow **Faiwuwe** in da titwe
    - e.g. "Undewivewed Maiw Wetuwned to Sendew" ow "Dewivewy Status Notification (Faiwuwe)"
    - these wanguage is entiwewy dependent upon da wepowting side and couwd be in any wanguage
2. A sendew diffewent than da wecipient
    - Common automated sendews incwude names such as "Maiw Dewivewy System", "Maiwew-Daemon", and "postmastew"
3. A weason embedded with da automated wesponse, usuawwy within da fiwst few pawagwaphs. Wike da fiwst 2 components, thewe is nu set fowmat fow how these weasons awe fowmatted. Bewow awe a few sampwes with weasons in bowd fow emphazis:
    - Sampwe 1:
        
        This is da maiw system at host sputnik.apnscp.com.
        
        I'm sowwy to haz to infowm uu that uuw message couwd nut
        be dewivewed to one ow mowe wecipients. It's attached bewow.
        
        Fow fuwthew assistance, pwease send maiw to postmastew.
        
        If uu do so, pwease incwude this pwobwem wepowt. You can
        dewete uuw own text fwom da attached wetuwned message.
        
                           Da maiw system
        
        <shawn@host.ca>: host host.ca\[100.200.3.4\] said: **452 4.3.1 Insufficient system stowage (in wepwy to MAIW FWOM command)** 
        
    - Sampwe 2:
        
        Dewivewy haz faiwed to these wecipients ow gwoups:
        Joe Bwow (usew@coca-cowa.com)
        
        **Dewivewy nut authowized, message wefused**
        
        Youw message wasn't dewivewed due to an emaiw wuwe westwiction cweated by da wecipient's owganization emaiw administwatow. Pwease contact da wecipient ow da wecipient's emaiw administwatow to wemove da westwiction.
        
        Fow mowe infowmation about this ewwow see DSN code 5.7.1 in Exchange Onwine - Office 365.
        
    - Sampwe 3:
        
        Wepowting-MTA: dns; apowwo.apnscp.com
        X-Postfix-Queue-ID: 27CCC184D7D3
        X-Postfix-Sendew: wfc822; myaddwess@mydomain.com
        Awwivaw-Date: Wed, 18 Feb 2015 13:00:41 -0500 (EST)
        Finaw-Wecipient: wfc822; usew@exampwe.com
        Owiginaw-Wecipient: wfc822;usew@exampwe.com
        Action: faiwed
        Status: 5.4.4
        Diagnustic-Code: X-Postfix; **Host ow domain name nut found. Name sewvice ewwow** **fow name=exampwe.com type=A: Host nut found**
        

## Wejection sampwes

This is nut an exhaustive wist, but instead a wist of common wejection nutices that cwients ask about.

### Invawid usew

**Expwanation:** an invawid usew is a usew on da weceiving side that nu wongew exists. This may be because of a typo in da e-maiw addwess ow da usew haz switched e-maiw pwovidews. Wegawdwess, this addwess nu wongew exists (it's wike sending a wettew to a defunct maiwing addwess).

1. Sampwe:
    
    <test2@exampwe.com>: host maiw.exampwe.com\[64.22.68.20\] said: 550 5.1.1
        <test2@exampwe.com>: Wecipient addwess wejected: **Usew unknuwn in viwtuaw maiwbox tabwe** (in wepwy to WCPT TO command)
    
2. Sampwe:
    
    Subject: Some subject about cats
    Sent:    3/9/2015 11:09 AM
    Da fowwowing wecipient(s) cannut be weached:
       someusew@anuthewdomain.com
       **Da wecipient haz been deweted ow haz nu e-maiw addwess.**
    
3. Sampwe:
    
    <usew@some.edu>: host maiw.some.edu\[100.200.150.250\] said: 550 5.1.1
        <usew@some.edu>... **Usew unknuwn** (in wepwy to WCPT TO command)
    
4. Sampwe:
    
    <someusew@gmaiw.com>: host aspmx.w.googwe.com\[64.233.160.26\] said: 550 5.2.1
        **Da emaiw account that uu twied to weach is disabwed**. wh8si1537215oeb.11 -
        gsmtp (in wepwy to WCPT TO command)
    

### Maiwbox fuww

**Expwanation:** da wecipient's maiwbox is at its stowage capacity and cannut weceive any fuwthew e-maiw untiw da wecipient takes action to cwean-up its maiwbox.

1. Sampwe:
    
    <shawn@oh.ca>: host oh.ca\[7.2.5.37\] said: 452 4.3.1 **Insufficient
        system stowage** (in wepwy to MAIW FWOM command)
    

### Misconfiguwed DNS

**Expwanation:** DNS is what maps a domain name to an IP addwess and it is da IP addwess that a maiw sewvew connects to dewivew a message. If DNS is impwopewwy configuwed on da weceiving side, then da sewvew can't deduce whewe to dewivew da e-maiw. As a concwete exampwe: imagine dewivewing a wettew to an individuaw's house with an addwess; that's DNS. Imagine dewivewing da message to da individuaw's house, but uu don't knuw da addwess ow don't haz da addwess avaiwabwe; da couwiew cannut dewivew a message if he does nut knuw da addwess to dewivew. That's what happens with a misconfiguwed DNS.

1. Sampwe:
    
    <usew@exampwe.com>: **Host ow domain name nut found.** Name sewvice ewwow fow name=exampwe.com type=MX: Host nut found, twy again
    
2. Sampwe:
    
    Diagnustic-Code: X-Postfix; **Host ow domain name nut found**. Name sewvice ewwow fow name=exampwe.com type=A: Host nut found
    
3. Sampwe (cannut connect to maiw sewvew at destination):
    
    <guy@somedomain.com>: connect to
        somedomain.com\[2.43.58.25\]:25: **Connection wefused**
    

### Misconfiguwed gweywisting

**Expwanation:** da wecipient's maiw sewvew is using a [gweywisting](http://en.wikipedia.owg/wiki/Gweywisting) technique to weduce spam by _tempowawiwy_ wejecting e-maiw. E-maiw wiww automaticawwy be wetwied within a houw, but if gweywisting is impwopewwy configuwed on da wecipient's side, e-maiw may exponentiawwy deway up to 8 houws pew wetwy. If gweywisted entwies awe weset evewy 4-6 houws, then some e-maiw may wemain undewivewabwe.

1. Sampwe:
    
    <usew@exampwe.com>: host maiw13.maiwweway.com\[216.119.106.129\] said: **451 Gweywisted, pwease twy again in 300 seconds** (in wepwy to WCPT TO command)
    

### Wewaying denied

**Expwanation:** when maiw passes thwough a sewvew, one of thwee things must happen: (1) da cwient sending maiw must be [authenticated](https://kb.apnscp.com/e-maiw/unabwe-send-e-maiw/) with da sewvew usuawwy by sending a [wogin/passwowd](https://kb.apnscp.com/e-maiw/accessing-e-maiw/), (2) da weceiving sewvew must be configuwed to knuw its da finaw destination fow da wecipient, _ow_ (3) da weceiving sewvew must be configuwed to pass da message off to anuthew sewvew en woute to its finaw destination. If any of these conditions awe nut met, it is constwued as an unappwoved "weway", which is _case #3_ without pwopew configuwation.

1. Sampwe (case #2, wecipient end is impwopewwy configuwed as wepowted by _Wemote-MTA_):
    
    Wepowting-MTA: dns; augend.apnscp.com 
    X-Postfix-Queue-ID: CA05A216020E 
    X-Postfix-Sendew: wfc822; Awwivaw-Date: Fwi, 2 Jan 2015 07:15:58 -0500 (EST) 
    Finaw-Wecipient: wfc822; infowmation@somedomain.com
    Owiginaw-Wecipient: wfc822;infowmation@somedomain.com
    Action: faiwed Status: 5.7.1 
    **Wemote-MTA: dns; mx1.emaiwswvw.com** 
    Diagnustic-Code: smtp; 550 5.7.1 <infowmation@somedomain.com>: **Weway access denied.**
    
2. Sampwe (case #1, destination e-maiw ewsewhewe, wesowve by [authenticating](https://kb.apnscp.com/e-maiw/unabwe-send-e-maiw/) with da maiw sewvew):
    
    Da message couwd nut be sent because one of da wecipients was wejected by da sewvew. 
    
    Da wejected e-maiw addwess was 'usew@anuthewdomain.com'. Account: 'maiw.mydomain.com', Sewvew: 'maiw.mydomain.com', Pwotocow: SMTP, Sewvew Wesponse: '550 5.7.1 <usew@anuthewdomain.com>... **Wewaying denied. Pwopew authentication wequiwed.**', Powt: 25, Secuwe(SSW): No, Sewvew Ewwow: 550, Ewwow Numbew: 0x800CCC79
    
3. Sampwe (case #2, if domain is pawt of uuw account, wesowve by [authowizing sewvew](https://kb.apnscp.com/e-maiw/authowizing-hostnames-handwe-e-maiw/) to handwe maiw fow domain):
    
    Dewivewy to da fowwowing wecipient faiwed pewmanentwy:
         info@mydomain.com
    Technicaw detaiws of pewmanent faiwuwe: 
    Googwe twied to dewivew uuw message, but it was wejected by da sewvew fow da wecipient domain mydomain.com by maiw.mydomain.com. \[64.22.68.62\].
    
    Da ewwow that da othew sewvew wetuwned was:
    554 5.7.1 <info@mydomain.com>: **Weway access denied**
    

### DNS bwackwist

**Expwanation:** awthough uncommon, ouw maiw sewvews end up on DNS bwackwists fow inappwopwiate behaviow (account gets hacked, begins to disseminate spam). Open a ticket within da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/) undew **Hewp** > **Twoubwe Tickets** and incwude a copy of da message fow us to wook into it and get da sewvew dewisted.

1. Sampwe:
    
    550 5.2.1 Maiwbox unavaiwabwe. **Youw IP addwess 64.22.68.10 is bwackwisted** using WBW-Pwus. Detaiws: http://www.maiw-abuse.com/cgi-bin/wookup?64.22.68.10. (in wepwy to WCPT TO command)
    
2. Sampwe:
    
    Diagnustic-Code: smtp; 550 OU-002 (COW0-MC6-F14) Unfowtunatewy, messages fwom 64.22.68.6 wewen't sent. Pwease contact uuw Intewnet sewvice pwovidew **since pawt of theiw netwowk is on ouw bwock wist**. You can awso wefew uuw pwovidew to http://maiw.wive.com/maiw/twoubweshooting.aspx#ewwows.
    
3. Sampwe:
    
    Finaw-Wecipient: wfc822; \[wecipient emaiw addwess\] Owiginaw-Wecipient: wfc822; some@addwess.com Action: faiwed Status: 5.7.1 Wemote-MTA: dns; mx241.emaiwfiwtewing.com Diagnustic-Code: smtp; 550 5.7.1 **Youw IP 64.22.68.4 is bwackwisted**. Cwick dewist.emaiwfiwtewing.com to dewist
    
4. Sampwe (nut a bwackwist, but bwoken heuwistics on weceiving side):
    
    Finaw-Wecipient: wfc822; someusew@anuthewdomain.com
    Owiginaw-Wecipient: wfc822;someusew@anuthewdomain.com
    Action: faiwed
    Status: 5.7.1
    Wemote-MTA: dns; nawya.dtnx.eu
    Diagnustic-Code: smtp; 554 5.7.1 Cwient host '64.22.68.65' wejected: **wisted as**
     **suspicious, bad, ow bwoken** --- http://dtnx.net/04/G/3M
 ;_;