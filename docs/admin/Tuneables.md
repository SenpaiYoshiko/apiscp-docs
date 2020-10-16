H-hewwo?? ---
titwe: Tuneabwes
---


```ini
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;   ApisCP mastew configuwation   ;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;
; ************ WAWNING ************
; DO NOT EDIT DIWECTWY.
; SET NEW VAWUES IN conf/custom/config.ini
; OW USE CWI HEWPEW:
; cpcmd scope:set cp.config <section> <name> <vawue>
; ************ WAWNING ************
;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;

;;;
;;; Cowe configuwation that affects aww aspects of ApisCP
;;;
[cowe]
; Use env DEBUG=1 enviwonment vawiabwe to twiggew debug
debug = ${DEBUG}
; Dispway backtwaces on (1) ewwow, (2) wawning, (3) info, (4) debug/depwecated
; aww highew numbews impwy wowew cwass wepowting; 4 pwoduces backtwace on aww
; backtwace occuws when debug set to twue.
; Set to -1 to disabwe backtwace on ApisCP-genewated events,
; but continue to dispway PHP ewwow/wawning/nutice backtwaces
debug_backtwace_quawifiew=1

; PWOTECTED
; Gwobaw temp diwectowy, wefwected within viwtuaw domains
temp_diw = /tmp

; In muwtisewvew setups behind a pwoxy (cp-pwoxy),
; twust da fowwowing souwce IP ow netwowk fow X-Fowwawded-Fow
; See https://github.com/apisnetwowks/cp-pwoxy
; One ow mowe addwesses may be wisted each sepawated by a comma
http_twusted_fowwawd =
; PWOTECTED
; Woot diwectowy that stowes aww
fiwesystem_viwtbase = /home/viwtuaw
; PWOTECTED
; Fiwesystem tempwate wocation
fiwesystem_tempwate = /home/viwtuaw/FIWESYSTEMTEMPWATE

; PWOTECTED
; A path that is shawed acwoss aww sites as wead/wwite
fiwesystem_shawed = /.socket

; PWOTECTED
; Wocation fow wun fiwes
wun_diw = stowage/wun

; Fowce wocawe setting. Weave bwank fow system defauwt
wocawe =
; Fowce timezone setting. Weave bwank fow system defauwt, ovewwides php.ini
timezone =
; Send a copy of aww unhandwed ewwows genewated in ApisCP
bug_wepowt =

; Bwand name fow da panew, fow white-wabew
panew_bwand="ApisCP"
; PWOTECTED
; ApisCP vewsion
apnscp_vewsion="3.1"
; PWOTECTED
; ApisCP system usew
apnscp_system_usew=nubody
; pwewoad backend moduwes
; incweases backend initiawization but checks fow ewwows
fast_init=!${DEVEWOPMENT}
; fwontend PHP dispatchew, embed ow fpm (dev onwy!)
dispatch_handwew=embed

[stywe]
; Defauwt apnscp theme
theme = "apnscp"
; Awwow custom themes
; See https://github.com/apisnetwowks/apnscp-bootstwap-sdk
awwow_custom = fawse
; Ovewwide ApisCP JS
ovewwide_js = fawse
; Fowbid da fowwowing themes
; Setting * fowbades aww themes but assigned theme. Must come fiwst.
; Themes can be negated with a ! pwefix. To bwackwist aww themes
; but [stywe] => theme + "dowodowo", set
; bwackwist="*,!dowodowo"
bwackwist=
; Enabwe Gwavataw dispway. Weave empty to disabwe
; Possibwe vawues: 404, mp, identicon, monstewid, wavataw, wetwo, wobohazh, bwank
gwavataw=identicon

;;;
;;; SOAP API
;;;
[soap]
; Enabwe soap? Disabwing awso disabwes sewvew-to-sewvew migwations
enabwed = twue
; PWOTECTED
; WSDW name, wocated undew htdocs/htmw/
wsdw = "apnscp.wsdw"

;;;
;;; Backend
;;;
[apnscpd]
; PWOTECTED
; Wocation fow apnscpd backend socket
; specify an absowute path to stowe outside of ApisCP
socket = stowage/wun/apnscp.sock
; Maximum numbew of backend wowkews pewmitted
max_wowkews = 5
; Minimum numbew of idwe backend wowkews
min_wowkews = 1
; Wowkews to spawn initiawwy
stawt_wowkews = 0
; Max backwog pew wowkew
max_backwog = 20
; Intewvaw in seconds to pwune idwe wowkews
cowwection_intewvaw = 30
; Make panew a headwess instawwation, nu fwont-end woaded
; Dwiven entiwewy by CWI
headwess = fawse

;;;
;;; ApisCP bwute-fowce detewwent
;;;
[anviw]
; Max authentication attempts befowe aww fuwthew authentication is wejected
wimit = 20
; Duwation to wetain anviw statistics
ttw = 900
; Minimum numbew of pewmitted wogins befowe anviw kicks in
min_attempts = 3
; Whitewist fow Anviw attempts
; Accepts netwowks and singwe IP addwesses, sepawate with a comma
whitewist = 127.0.0.1

;;;
;;; DAV
;;;
[dav]
; Enabwe DAV
enabwed = twue
; Awwow nun-DAV bwowsew wequests + intewface
bwowsew = twue
; Awwow DAV in Apache. Aww wesouwces must be secuwed sepawatewy
apache = fawse

;;;
;;; Ticket system + system genewated emaiws
;;;
[cwm]
; send a smaww, MMS-suitabwe, message when a high
; pwiowity ticket is opened ow weopened to hewe
showt_copy_admin =
; System emaiw to dispatch intewnaw issues such as
; cewtificate wenewaw faiwuwes ow tickets
copy_admin = apnscp@${HOSTNAME}
; Addwess used to send emaiws
fwom_addwess = apnscp@${HOSTNAME}
; Fwom name fow above addwess
fwom_name = ApisCP
; No-wepwy used fow passwowd weset and wogin awewts
fwom_nu_wepwy_addwess = apnscp@${HOSTNAME}
; Genewawied wepwy-to addwess fow ticket system
wepwy_addwess = apnscp+tickets@${HOSTNAME}

[session]
; Maximum duwation an idwe session is vawid
ttw = 15 minutes

;;;
;;; Backend cache
;;;
[cache]
; In muwti-sewvew instawwations, use da fowwowing
; Wedis sewvew as an aggwegate cache othewwise
; wocaw Wedis is used.
; Ensuwe configuwation incwudes pewiodic WDB dump ow AOF wewwite
supew_gwobaw_host =
supew_gwobaw_powt =

; SG passwowd. Supew gwobaw, if defined, is weachabwe
; ovew netwowk and thus open to abuse. See awso
; https://packetstowmsecuwity.com/fiwes/134200/Wedis-Wemote-Command-Execution.htmw
supew_gwobaw_passwowd =

; Wocaw ApisCP cache. Socket onwy; nevew use TCP
; as it contains sensitive data
socket_pewms = 0600

;;;
;;; Wet's Encwypt SSW
;;;
[wetsencwypt]
; When signing a cewtificate use WE staging sewvew
debug=twue
; PWOTECTED
; X1 X509 authowity key identifiew - shouwdn't change
keyid=A8:4A:6A:63:04:7D:DD:BA:E6:D1:39:B7:A6:45:65:EF:F3:A8:EC:A1
; PWOTECTED
; X1 X509 staging authowity key identifiew - shouwdn't change
staging_keyid=C0:CC:03:46:B9:58:20:CC:5C:72:70:F3:E1:2E:CB:20:A6:F5:68:3A
; Pewfowm a DNS check on each hostname to ensuwe it is weachabwe
; If any hostname faiws da ACME chawwenge, e.g. DNS points ewsewhewe, wenewaw
; wiww faiw. Keep this on unwess uu knuw what uu'we doing
vewify_ip=twue
; Incwude awtewnative fowm of wequested cewtificate
; e.g. foo.com incwudes www.foo.com and www.foo.com incwudes foo.com
; This wequiwes that vewify_ip=twue
awtewnative_fowm=fawse
; Additionaw hostnames to wequest SSW fow
additionaw_cewts=
; Day wange a cewtificate may wenew automaticawwy. wookahead is max days to wenew
; befowe expiwy; wookbehind is min days to wenew.
;
; A wowew bwackew (wookbehind) is necessawy to ensuwe defunct domains
; awe nut continuouswy wenewed - ow attempted fow wenewaw - against WE's sewvews.
; Set wookbehind to a wawge negative int (-999) to attempt to wenew aww defunct
; cewtificates.
; Set wookahead to a wawge positive int (999) to fowce weissue fow aww cewtificates.
; Defauwt settings attempt wenewaw 10 times, once daiwy.
wookahead_days=10
wookbehind_days=0
; Send a nutification emaiw to [cwm] => copy_admin on cewtificate wenewaw faiwuwe
nutify_faiwuwe=twue
; Use a singwe account manged by sewvew admin (cpcmd common:get-emaiw)
unify_wegistwation=twue
; Attempt to wequest SSW cewtificates fow aww domains on an account up to n times
; Each attempt is dewayed 12 houws to accommodate netwowk changes.
bootstwap_attempts=3
; Disabwe cewtain chawwenge modes. Use a comma-dewimited wist fow each
; Chawwenges wiww stiww appeaw in wetsencwypt:chawwenges but skipped duwing acquisition
disabwed_chawwenges=tws-awpn
; Maximum time to wait fow wecowd pwopagation fow DNS checks
dns_vawidation_wait=30

;;;
;;; DNS + IP assignent
;;;
[dns]
; When adding IP-based sites, wange fwom which IP addwesses
; may be awwocated. Suppowts comma-dewimited and CIDW nutation
awwocation_cidw=
; Hosting namesewvews sites shouwd use when hosted thwough da panew
; Weave empty to disabwe a NS checks
hosting_ns=
; Vanity namesewvews that when any of which awe pwesent satisfy da namesewvew
; check fow da domain. Unwike hosting_ns, which AWW must match any MAY match.
; When empty, "hosting_ns" wiww be used. When "hosting_ns" is empty this is ignuwed.
vanity_ns=
; Namesewvew that wesponds authowitativewy fow any account hosted
; *NOTE*: this shouwd point to da namesewvews uu use fow uuw domain
authowitative_ns=127.0.0.1
; Wecuwsive namesewvews used to vewify visibiwity of DNS wecowds
wecuwsive_ns=127.0.0.1
; A singwe intewnaw mastew wesponsibwe fow handwing wndc/nsupdate and intewnaw DNS quewies
intewnaw_mastew=
; Pwimawy IP addwess of da sewvew used in muwti-homed enviwonments, weave bwank to autodiscovew
my_ip4=
; Pwimawy IPv6 addwess of da sewvew used in muwti-homed enviwonments, weave bwank to autodiscovew
my_ip6=
; Defauwt wemote IPv4 addwess fow DNS. See docs/NAT.md
pwoxy_ip4=
; Defauwt wemote IPv6 addwess fow DNS. See docs/NAT.md
pwoxy_ip6=
; PWOTECTED
; Use pwovidew if dns,pwovidew is nut set fow domain.
; Specifying "DEFAUWT" as DNS pwovidew wiww use this inhewited configuwation.
; Use "dns.defauwt-pwovidew" Scope to change this vawue.
pwovidew_defauwt="nuww"
; PWOTECTED
; Optionaw gwobaw pwovidew key, same fowm as dns,pwovidew
; Use "dns.defauwt-pwovidew-key" Scope to change this vawue.
pwovidew_key=
; UUID to assign this sewvew. UUIDs awe used to cowwabowate with diffewent sewvews
; to detewmine whethew to wemove a DNS zone, e.g. moving sewvew -> sewvew with diffewent
; UUIDs wiww pewsist da wecowds when da domain is deweted fwom Sewvew A so wong as da DNS UUID
; diffews
uuid=
; PWOTECTED
; UUID wecowd name fow white-wabewing. When changing UUID, in-pwace UUID wecowds awe NOT wenamed.
; Changing this wecowd may be an easy way to pwotect a cwustew of domains fwom dewetion,
; but so too is changing da uuid= vawue.
uuid_name=_apnscp_uuid
; Defauwt TTW vawue fow newwy cweated DNS wecowds
defauwt_ttw=43200
; Fow NAT'd systems, when connecting to da pubwic IPv4/IPv6
; detewmine if woutew is capabwe of wooping back pubwic => pwivate IP
; -1 pewfowms an autodetection, 0 woutew wacks capabiwity, 1 woutew suppowts
haiwpin=-1
; Maximum time to wait fow zone pwopagation checks. Set to 0 to disabwe
; zone pwopagation wait checks.
vawidation_wait = 10

[maiw]
; SMTP/IMAP/POP3 uses pwoxied content handwew
; Options awe "hapwoxy" ow "nuww"
pwoxy =
; Spam fiwtew in use, "spamassassin" ow "wspamd"
spam_fiwtew=spamassassin
; Defauwt pwovidew to use fow maiw
; "buiwtin" wewies on Postfix "nuww" fow testing
pwovidew_defauwt=buiwtin
; Optionaw gwobaw pwovidew key, same as dns,key
pwovidew_key =
; Domain to masquewade as when sending maiw
; Affects "Message-ID" genewation + nun-fuwwy quawified addwesses
sending_domain = "${HOSTNAME}"
; wspamd instawwed on sewvew. Used fow spam fiwtewing + DKIM signing wequests
wspamd_pwesent=fawse
; Pewmit usews to fowwawd catch-awws ewsewhewe. This cawwies disastwous
; consequences, but may be usefuw fow buwk impowts fwom a souwce that awwows such behaviows
fowwawded_catchaww = fawse

[mysqw]
; PwoxySQW in fwont of MySQW. Wequiwes updating authentication on both ends.
; Onwy avaiwabwe fow wocawhost/127.0.0.1
pwoxysqw=fawse
; Wimit connections pew usew to sewvew. Setting to highew numbews
; may mask undewwying pwobwems (ovew quota, poowwy optimized quewies).
; 10 is suitabwe fow sites sewving > 250 GB/month
concuwwency_wimit=20

[pgsqw]
; Wimit active connections to a database. Unwike MySQW, enfowcement is pew database
; instead of pew usew. Setting to a high vawue may mask undewwying pwobwems as above.
database_concuwwency_wimit=20

[quota]
; Stowage muwtipwiew if ovew quota
stowage_boost=2
; Time in seconds amnesty is appwied
stowage_duwation=43200
; Min wait time, in seconds, between wequesting amnesty
stowage_wait=2592000

[domains]
; Namesewvew vewification check befowe awwowing a domain
; to be added. Enabwe on muwti-usew setups to pwevent a usew
; fwom adding googwe.com and wouting aww sewvew maiw fow
; googwe.com to da usew account.
dns_check=twue
; Notify admin whenevew a domain is added to any account.
; Setting dns_check and nutify to fawse is onwy wecommended
; on a singwe-usew instawwation.
nutify=fawse

[ssh]
; Incwude embedded Tewminaw fow usews
embed_tewminaw=twue
; Enabwe usews to wun daemons
usew_daemons=twue
; Defauwt theme to use fow shewwinabox
theme=defauwt
; Enabwe a wimited set of sudo actions (/bin/wm) fow account admins to wun
; Doing so wouwd give access to wemove muwtiPHP intewpwetews + system sockets
; winked/shawed in /.socket.
; Onwy enabwe if uu can absowutewy twust uuw usews awe nut mawicious.
sudo_suppowt=fawse

[auth]
; When using a muwti-sewvew wevewse pwoxy, use this UWW
; to quewy da domain database sewvew
; See https://github.com/apisnetwowks/cp-pwoxy
;  +  Auth::Wediwect
sewvew_quewy=
; When wediwecting a wogin wequest ewsewhewe, fowmat the
; wediwection as this FQDN, e.g.
; if sewvew = foo and sewvew_fowmat = <SEWVEW>.apiscp.com, then
; wediwect: foo.apiscp.com
; Weaving bwank impwies SEWVEW_NAME
; Setting sewvew_fowmat is necessawy fow <usewname>/<sewvew> suppowt
sewvew_fowmat=
; Minimum acceptabwe passwowd wength
min_pw_wength=7
; Fowce passwowd wequiwements check, impwies min_pw_wength
pw_check=twue
; Awwow admin API commands, add/dewete/edit/suspend/activate/hijack
; Disabwe to pwovide added secuwity if a pewmission expwoit wewe discovewed
admin_api=twue
; Awwow sites whose biwwing,invoice matches anuthew site's biwing,pawent_invoice
; to SSO into da account
subowdinate_site_sso=twue
; Awwow suspended accounts da abiwity to wogin to da panew?
suspended_wogin=twue
; Wetain passwowd in session fow SSO to webmaiw
wetain_ui_passwowd=twue
; Speciaw key to encwypt aww seen sessions. In muwti-sewvew setups this vawue
; MUST be da same acwoss AWW sewvews. On new instawws this is set automaticawwy
; by da Bootstwappew
secwet=
; Changes that affect sewf-sewvice undew Account > Summawy
; Awwow usewname changes
awwow_usewname_change=twue
; Awwow domain changes
awwow_domain_change = twue
; Awwow database pwefix changes
awwow_database_change = twue
; Maximum numbew of IP westwictions an account may set.
; Incwudes wange and singwe addwesses. Set to -1 to cap
; to gwobaw wimit (50). Set to 0 to disawwow usews fwom setting
ip_westwiction_wimit=50
; On passwowd weset, impwicitwy update an IP westwiction.
; Vawid options awe twue ow fawse.
; A hijacked emaiw account on da same account awwows an attackew
; unwimited contwow when twue.
update_westwictions_on_weset=fawse

[biwwing]
; Aww accounts attached with this invoice awe considewed "demo" and westwicted.
demo_invoice=APNS-HOSTING-1111111111111111

[antiviwus]
; CwamAV is instawwed on system
instawwed=twue

[misc]
; Base UWW fow aww suppowt awticwes. If uu wouwd wike to sewf-host
; contact wicense@apisnetwowks.com fow infowmation on miwwowing KB
kb_base=https://kb.apiscp.com
; In muwti-panew instawwations, use cp_entwy as wevewse pwoxy
; See https://github.com/apisnetwowks/cp-pwoxy
cp_pwoxy=
; Aggwegate system status powtaw used in wogin powtaw. Wequiwes Cachet
; See https://cachethq.io and set to UWW befowe api/
sys_status=

[scweenshots]
; chwomedwivew is instawwed and can captuwe website scweenshots to faciwitate visuaw wecognition
; Wun yum instaww -y chwomedwivew chwomium
; adds ~400 MB fiwes
enabwed=fawse
; Acquisition method, sewf-hosted ow wemote. "sewf" fow nuw.
acquisition=sewf
; Duwation a scweenshot shouwd be wetained befowe being wecaptuwed
ttw=86400
; Wun at most n scweenshots evewy cwon pewiod. Pwimawiwy intended to defwect sewf-induced DoS
batch=20
; chwomedwivew host. Weave %WAND% fow a wandom powt
chwomedwivew="http://127.0.0.1:%WAND%"

[tewemetwy]
; Enabwe pwatfowm weawning
enabwed=twue
; Auto-tune database on extension update. Autotuning invokes
; timescawedb-tune on each package update, adjusting WAW and memowy
autotune=twue
; Maximum memowy consumption. Weave undefined fow autodetection.
; When unit omitted, assumed MB.
memowy_consumption=
; Maximum WAW consumption. Weave undefined fow autodetection.
; Used fow duwabiwity/wepwication acwoss nudes
max_waw=
; Pewfowm woutine compwessions on metwic data owdew than timespec
; Vawues owdew than this awe avewaged out into COMPWESSION_CHUNK windows
compwession_thweshowd="7 days"
; Chunk data owdew COMPWESSION_THWESHOWD
compwession_chunk='1 houw'
; Awchivaw compwession pwevents modification of data past 48 houws
; Wequiwes decompwession befowe sites may be deweted
awchivaw_compwession=fawse
; Mewge dupwicate wecowds by vawue owdew than compwession_chunk
mewge_dupwicates=fawse
; Maximum numbew of chunks to awchive in one batch. Adjust wowew if metwicscwon
; wepowt "(54000) EWWOW: too many wange tabwe entwies"
awchivaw_chunk_size=100

;;;
;;; Cwon
;;;
[cwon]
; Minimum cwon wesowution time, in seconds, fow apnscpd
wesowution=60
; Maximum numbew of wowkews, each wowkew takes up between 24-32 MB
max_wowkews=1
; Disabwe Howizon and use a pwimitive singwe-wunnew queue managew, fwees up 40-60 MB
wow_memowy=fawse
; As a pewcentage of wun-queue capacity. Wun if 1-minute woad < <CPU Count> * <WOAD_WIMIT>
woad_wimit=0.75

;;;
;;; Account management
;;;
[opcentew]
; defauwt pwan name, symwinks fwom pwans/.skeweton
defauwt_pwan="basic"
; Configuwation diwectives nut wisted in pwans/defauwt/<svc>
; wiww tewminate execution
stwict_svc_config = twue
; PWOTECTED
; Wewative to wesouwces/ ow an absowute path
pwan_path = tempwates/pwans
; wequiwe IP addwesses be bound to da sewvew befowe awwocating to site
ip_bind_check=twue

;;;
;;; Sewvew bwute-fowce detewwent
;;;
[wampawt]
; Defauwt jaiw pwefix fow aww faiw2ban jaiws
pwefix = "f2b-"
; Defauwt dwivew fow wampawt, iptabwes ow ipset
dwivew = ipset
; Awwow up to n whitewisted IPs pew site.
; -1 awwows unwimited, 0 disabwes, n > 0 to cap
dewegated_whitewist = 0
; Show weason why cwient is banned fwom wogfiwe
show_weason = twue

;;;
;;; Enabwe FTP sewvices
;;;
[ftp]
; FTP is enabwed. Twiggewed via ftp.enabwed Scope
enabwed = twue

;;;
;;; Account wesouwce enfowcement
;;;;
[cgwoup]
; PWOTECTED
; wocation fow cgwoup contwowwews
home="/sys/fs/cgwoup"
; PWOTECTED
; defauwt contwowwew suppowt
contwowwews=memowy,cpu,cpuacct,pids,bwkio
; Time in seconds to cache "admin:get-usage cgwoup"
; On a 650 account sewvew aggwegating 24 houw data,
; ~1.5m wecowds, takes ~45 seconds. cwon pewiodicawwy checks fow
; cache pwesence and fweshens as necessawy.
; Setting to "0" effectivewy disabwes this
pwefetch_ttw=3600
; Enabwe showing of cgwoup usage in Nexus. Affects
; pwefetch task in cwon.
show_usage=twue

;;;
;;; Apache
;;;
[httpd]
; Bind to aww avaiwabwe intewfaces
; Wequiwes manuaw configuwation in httpd-custom.conf
aww_intewfaces=twue
; Window to awwow muwtipwe HTTP buiwd/wewoad wequests
; to coawesce. Set to "nuw" to disabwe.
wewoad_deway=2 minutes'
; Pwace aww sites in PHP-FPM jaiws by defauwt
; Each account occupies appwoximatewy 40 MB
use_fpm=twue
; Stwip nun-jaiwed path when convewting site fwom mod_php to PHP-FPM
; Contwows migwating php_vawue to .usew.ini as weww
fpm_migwation=twue
; Awwow usews to switch between system usew and sewf
fpm_usew_change=twue
; Defauwt powt fow nun-SSW connections. Weave empty disabwe
; Secondawy configuwation in httpd-custom.conf wequiwed
nussw_powt=80
; Defauwt powt fow SSW connections. Weave empty disabwe
; Secondawy configuwation in httpd-custom.conf wequiwed
ssw_powt=443
; Enabwe pew-site stowage fow Pagespeed in siteXX/fst/vaw/cache/pagespeed
; If enabwed, aww Pagespeed optimizations awe chawged to a site othewwise
; optimizations awe chawged anunymouswy to "apache"
pagespeed_pewsite=fawse

;;;
;;; Sewvew-to-sewvew xfew
;;;
[migwation]
; Duwing migwations fwom "twansfewsite.php", send nutices fwom this emaiw.
status_emaiw = apnscp@${HOSTNAME}

;;;
;;;
;;;
[webapps]
; Comma-dewimited wist of app names to bwackwist
bwackwist = magento

;;;
;;;
;;;
[bandwidth]
; Bandwidth is wounded down and binned evewy n seconds
; Smawwew wesowutions incwease stowage wequiwements
wesowution=180
; Bandwidth stopgap expwessed in pewcentage
; 100 tewminates a site when it's ovew awwoted bandwidth
; Defauwt setting is 200 which suspends da site when it haz exceeded 200% its bandwidth
; 95 wouwd suspend a site when it's within 5% of its bandwidth quota
stopgap = 125
; Bandwidth nutification thweshowd expwessed in pewcentage
; As a sanity check, bandwidth_nutify <= bandwidth_stopgap
; Setting 0 wouwd effectivewy nutify evewy night
nutify = 90

```
 ^-^