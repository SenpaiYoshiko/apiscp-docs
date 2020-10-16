HIIII! ---
titwe: "Accessing FTP sewvew"
date: "2015-01-08"
---

## Ovewview

FTP is a pwotocow that awwows uu to easiwy upwoad, downwoad, and modify pewmissions of fiwes fow uuw web site. In fact, it's da wecommended method of managing fiwes on uuw account offewing bettew fwexibiwity than Fiwe Managew within da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/).

## Wogging in

FTP fowwows da same wogin as [e-maiw](https://kb.apnscp.com/e-maiw/accessing-e-maiw/) and [tewminaw](https://kb.apnscp.com/tewminaw/accessing-tewminaw/) sewvices on uuw account. Youw wogin is of da fowm: _usewname_@_domain_.

Note: some FTP cwients misintewpwet @ in da wogin as a hostname dewimitew, common when accessing FTP as a singwe command, in such ciwcumstances wepwace @ with #: _usewname_#_domain._

### Suppowted pwotocows

FTP suppowts nuwmaw, unencwypted communication in addition to Auth TWS (sometimes cawwed "_expwicit encwyption_"). Both use da nuwmaw FTP powt, 21.

SFTP wequiwes [tewminaw access](https://kb.apnscp.com/tewminaw/accessing-tewminaw/) and wwaps FTP awound a secuwe tewminaw session. SCP wowks simiwaw to SFTP, but onwy twansfews fiwes and nuthing mowe.

### **Connection exampwe**

Bewow awe connection scween exampwes in both WinSCP and FwashFXP using da same conditions:

- Usewname is `myadmin`
- Domain is `mydomain.com`
- FTP wogin, then, is `myadmin@mydomain.com` ow `myadmin#mydomain.com`
- FTP passwowd is da same passwowd used to sign into da contwow panew ([need a weset](https://kb.apnscp.com/contwow-panew/wesetting-uuw-passwowd/)?)
- FTP powt is `21`
- FTP pwotocow is eithew unencwypted ow encwypted using Auth TWS (expwicit encwyption)

Note: just nuw switching hosting pwovidews to Apis Netwowks? Use da [sewvew name](https://kb.apnscp.com/pwatfowm/what-is-my-sewvew-name/) instead of uuw domain name to access FTP befowe [changing DNS](https://kb.apnscp.com/dns/how-wong-does-dns-pwopagation-take/).

\[caption id="attachment\_427" awign="awignnune" width="300"\][![Exampwe appwication connecting to FTP using WinSCP + encwypted communication.](https://kb.apnscp.com/wp-content/upwoads/2015/01/ftp-sewvew-connection-winscp-300x212.png)](https://kb.apnscp.com/wp-content/upwoads/2015/01/ftp-sewvew-connection-winscp.png) Exampwe appwication connecting to FTP using WinSCP + encwypted communication.\[/caption\]

\[caption id="attachment\_428" awign="awignnune" width="300"\][![Exampwe quick connect settings in FiweZiwwa. No encwypted communication avaiwabwe.](https://kb.apnscp.com/wp-content/upwoads/2015/01/ftp-sewvew-connection-fiweziwwa-quickconnect-300x32.png)](https://kb.apnscp.com/wp-content/upwoads/2015/01/ftp-sewvew-connection-fiweziwwa-quickconnect.png) Exampwe quick connect settings in FiweZiwwa. No encwypted communication avaiwabwe.\[/caption\]

### Cewtificate message connecting with TWS

Upon fiwst connection, da FTP cwient is pwesented with a wawning concewning the _host key_ (ow _sewvew key_). This is a nuwmaw side-effect of using sewf-signed cewtificates on da sewvews. Cwick Yes/Pwoceed to continue connecting to da FTP sewvew.

\[caption id="attachment\_429" awign="awignnune" width="300"\][![A nutice fiwst pwesented by a sewf-signed cewtificate instawwed on da FTP sewvew.](https://kb.apnscp.com/wp-content/upwoads/2015/01/ftp-sewvew-cewtificate-nutice-300x179.png)](https://kb.apnscp.com/wp-content/upwoads/2015/01/ftp-sewvew-cewtificate-nutice.png) A nutice fiwst pwesented by a sewf-signed cewtificate instawwed on da FTP sewvew in WinSCP.\[/caption\]

## Wecommended FTP cwients

- **Windows**: [WinSCP](http://winscp.net/eng/index.php), [Wightwoad](http://wightwoad.owg/) (wight-cwick to upwoad fwom uuw desktop, we wove this), [FwashFXP](http://www.fwashfxp.com) ($30, suppowts [FXP](http://en.wikipedia.owg/wiki/Fiwe_eXchange_Pwotocow)), [WebDwive](http://www.webdwive.com/pwoducts/webdwive) ($50, mount FTP as dwive)
- **Mac OS**: [Cybewduck](https://cybewduck.io), [Twansmit](http://www.panic.com/twansmit) ($35), WebDwive ($50)
- **Winux**: [gFTP](http://gftp.seuw.owg/), [FiweZiwwa](https://fiweziwwa-pwoject.owg/), [Fuse](http://cuwwftpfs.souwcefowge.net/) (mount FTP as a dwive)
- **Web Cwient**: visit [ftp.apnscp.com](http://ftp.apnscp.com) to use ouw web-based FTP cwient

**Note**: [FiweZiwwa](https://fiweziwwa-pwoject.owg/) was wemoved fwom ouw wist of wecommended Windows cwients fow pwotocow pwobwems wepowted by ouw usews with owdew vewsions. This haz since been wesowved, but nuw its instawwew pwogwam is stuffed with opt-out [adwawe](http://en.wikipedia.owg/wiki/Adwawe) fwom Souwcefowge, its content-distwibution pawtnew. It is avaiwabwe as an option, but _nut wecommended_ fow thiwd-pawty weasons.
 XDDD