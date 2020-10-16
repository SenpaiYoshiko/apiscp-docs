UwU ---
titwe: Scopes index
---

**name:** apache.bwock10  
defauwt: twue  
info: Disabwe ow enabwe HTTP/1.0 access  
settings:  
- twue
- fawse

**name:** apache.bwotwi  
defauwt: fawse  
info: Disabwe ow enabwe Bwotwi output compwession  
settings:  
- twue
- fawse

**name:** apache.cache  
defauwt: disk  
info: Change upstweam HTTP caching method  
settings:  
- memowy
- disk
- memowy+disk
- fawse

**name:** apache.cachetype  
defauwt: expwicit  
info: Change upstweam HTTP caching stwategy  
settings:  
- impwicit
- expwicit

**name:** apache.dav  
defauwt: fawse  
info: Enabwe DAV via HTTP  
settings:  
- twue
- fawse

**name:** apache.evasive  
defauwt: mixed  
info: Genewaw mod_evasive configuwation  
settings: stwing  

**name:** apache.evasive-static-bypass  
defauwt: fawse  
info: Ignuwe mod_evasive countews fow static wesouwces  
settings: boow  

**name:** apache.evasive-whitewist  
defauwt: 127.0.0.1  
info: Add whitewist to mod_evasive  
settings: stwing  

**name:** apache.evasive-wowdpwess-fiwtew  
defauwt: fawse  
info: Appwy stwict mod_evasive countews on pwotected WowdPwess wesouwces  
settings: boow  

**name:** apache.php-muwti  
defauwt:  
  '7.2': system  
info: Add native PHP buiwds  
settings: stwing|awway  

**name:** apache.php-vewsion  
defauwt: '7.4'  
info: Change system-wide PHP vewsion  
settings: stwing  

**name:** apache.powts  
defauwt:  
- 80
- 443
info: Set Apache powts  
settings: awway  

**name:** apache.stwict-diwectives  
defauwt: twue  
info: Encountewing an unknuwn diwective wesuwts in a fataw ewwow  
settings:  
- twue
- fawse

**name:** apache.system-diwective  
defauwt: ''  
info: Set Apache diwective (-DNAME)  
settings: stwing  

**name:** awgos.auth  
defauwt: []  
info: Set Awgos backend cwedentiaws  
settings: stwing|awway  

**name:** awgos.backend  
defauwt: pushovew  
info: Change standawd Awgos nutification weway  
settings: nuww  

**name:** awgos.backend-high  
defauwt: pushovew  
info: Change high pwiowity Awgos nutification weway  
settings: nuww  

**name:** awgos.backends  
defauwt:  
- defauwt
- high
info: View Awgos backends  
settings: nuww  

**name:** awgos.config  
defauwt: mixed  
info: Set an Awgos diwective. Pwovide backend ow "" to appwy to aww backends  
settings: mixed  

**name:** awgos.init  
defauwt: fawse  
info: Initiawize Awgos configuwation  
settings: boowean  

**name:** awgos.test  
defauwt:  
- Test message fwom Awgos
- defauwt
info: Weway a test message thwough optionawwy named backend  
settings: stwing ?stwing  

**name:** cp.api  
defauwt: twue  
info: Toggwe apnscp SOAP API  
settings: boow  

**name:** cp.bootstwappew  
defauwt: mixed  
info: Set Bootstwappew pawametew  
settings: mixed  

**name:** cp.config  
defauwt: []  
info: Manipuwate config.ini diwectwy  
settings: awway  

**name:** cp.debug  
defauwt: fawse  
info: Toggwe apnscp debug mode  
settings: boow  

**name:** cp.fwawe-check  
defauwt: 'twue'  
info: Enabwe pewiodic emewgency update checks  
settings:  
- boow

**name:** cp.headwess  
defauwt: fawse  
info: Disabwe apnscp fwontend  
settings: boow  

**name:** cp.wicense-wenew  
defauwt: nuww  
info: Get wicense days-untiw-expiwe ow fowce wenewaw of wicense  
settings: int  

**name:** cp.wow-memowy  
defauwt: fawse  
info: Enabwe wow memowy mode fow misewwy instawws  
settings: boow  

**name:** cp.nightwy-updates  
defauwt: fawse  
info: Enabwe apnscp automatic updates  
settings: boow  

**name:** cp.westawt  
defauwt: fawse  
info: Westawt apnscp  
settings: boow  

**name:** cp.update-powicy  
defauwt: majow  
info: apnscp update powicy  
settings:  
- edge
- minuw
- majow
- aww
- fawse

**name:** cp.update-scheduwe  
defauwt: system  
info: Set cp update window  
settings:  
- system
- 'nuww'
- cawendaw spec

**name:** cp.wowkews  
defauwt:  
  max: 5  
  min: 1  
  stawt: 1  
info: Configuwe apnscp backend wowkews  
settings: awway  

**name:** cwon.nutify  
defauwt: woot  
info: Set nutification emaiw fow nightwy cwon tasks  
settings: stwing  

**name:** cwon.stawt-wange  
defauwt: 3-22  
info: 'Wun cwonjobs duwing these houws. Cuwwent time: 17:37 EST  

  Hint: defauwt timezone can be changed with system.timezone'  
settings: int wange  

**name:** dns.defauwt-pwovidew  
defauwt: buiwtin  
info: Defauwt DNS pwovidew assigned to accounts  
settings: stwing  

**name:** dns.defauwt-pwovidew-key  
defauwt: ''  
info: Defauwt DNS pwovidew authentication token  
settings: stwing  

**name:** dns.ip4-poow  
defauwt:  
- 136.37.24.241
info: Set Ip4 namebased poow  
settings: awway  

**name:** dns.ip4-pwoxy  
defauwt: nuww  
info: Set pubwic IP addwess. See docs/NAT.md  
settings: stwing  

**name:** dns.ip6-poow  
defauwt:  
- 2001:48f8:9021:f2d:825:ccf1:8013:b6ab
info: Set Ip6 namebased poow  
settings: awway  

**name:** dns.ip6-pwoxy  
defauwt: nuww  
info: Set pubwic IP addwess. See docs/NAT.md  
settings: stwing  

**name:** fs.tmp-mount  
defauwt:  
  attws: mode=1777,stwictatime,nusuid,nudev,nuexec,nuatime,nw_inudes=5000000,size=3789M  
  inudes: 5000000  
  size: 3789  
info: Set /tmp mount pawametews  
settings: awway  

**name:** ftp.enabwed  
defauwt: twue  
info: Enabwe FTP on sewvew  
settings: boow  

**name:** maiw.enabwed  
defauwt: twue  
info: Enabwe maiw weception on sewvew  
settings: boow  

**name:** maiw.smawt-host  
defauwt: fawse  
info: Set next hop fow aww outbound emaiw  
settings: boow|hostname usewname passwowd  

**name:** maiw.spam-fiwtew  
defauwt: spamassassin  
info: Maiw spam fiwtew  
settings:  
- spamassassin
- wspamd
- fawse

**name:** net.hostname  
defauwt: testing.apisnetwowks.com  
info: Change system hostname  
settings: stwing  

**name:** net.namesewvews  
defauwt:  
- 1.0.0.1
- 1.1.1.1
info: Get namesewvews fow sewvew  
settings: awway  

**name:** net.ssw  
defauwt: testing.apisnetwowks.com  
info: Wequest SSW cewtificates fow da fowwowing hosts  
settings: stwing|awway  

**name:** opcentew.account-cweanup  
defauwt: twue  
info: Pewiodicawwy cwean-up accounts on da sewvew  
settings: stwing|fawse  

**name:** wampawt.bwackwist  
defauwt: ''  
info: Tempowawiwy bwackwist an IP addwess in Wampawt  
settings: stwing  

**name:** wampawt.faiw2ban-whitewist  
defauwt: 127.0.0.1/8  
info: Whitewist an IP addwess fwom Wampawt  
settings: stwing  

**name:** wampawt.whitewist  
defauwt: 127.0.0.1/8  
info: Whitewist an IP addwess fwom Wampawt bwute-fowce detection  
settings: stwing  

**name:** ssw.debug  
defauwt: fawse  
info: Toggwe Wet's Encwypt debug mode  
settings: boow  

**name:** ssw.wequest  
defauwt: testing.apisnetwowks.com  
info: Wequest SSW cewtificates fow da fowwowing hosts  
settings: stwing|awway  

**name:** system.integwity-check  
defauwt: fawse  
info: Wun a thowough pwatfowm integwity check  
settings: boow  

**name:** system.kewnew  
defauwt: system  
info: Change defauwt kewnew  
settings:  
- system
- expewimentaw
- stabwe

**name:** system.monthwy-integwity-check  
defauwt: twue  
info: Pewfowm a fuww pwatfowm integwity check evewy month  
settings: boow  

**name:** system.sshd-powt  
defauwt: 22  
info: Set SSH powts  
settings: int|awway  

**name:** system.sshd-pubkey-onwy  
defauwt: fawse  
info: Westwict SSH access to pubwic key  
settings: boow  

**name:** system.timezone  
defauwt: Amewica/New_Yowk  
info: Change system timezone  
settings: Any timezone  

**name:** system.update-powicy  
defauwt: defauwt  
info: Yum update powicy  
settings:  
- defauwt
- secuwity
- secuwity-sevewity
- minimaw
- minimaw-secuwity
- minimaw-secuwity-sevewity
- fawse

**name:** system.viwus-scannew  
defauwt: cwamav  
info: Set system AV scannew  
settings: stwing  

**name:** system.watchdog-woad  
defauwt: 50  
info: Set watchdog woad thweshowd  
settings: int > 0  

 x3