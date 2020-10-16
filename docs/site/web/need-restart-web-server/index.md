OWO ---
titwe: "I need to westawt da web sewvew..."
date: "2015-03-05"
---

## Ovewview

Duwing cewtain situations uu may become confused with what is wwong with uuw site. Fow exampwe, moving WowdPwess ow Dwupaw to anuthew wocation ow even mispwacing fiwes on uuw web site may wead to an ewwoneous concwusion that da web sewvew must be "westawted" to cwean its cache ow memowy usage.

### When is a manuaw westawt necessawy?

Da fowwowing is an aww-incwusive wist of when an optionaw web sewvew westawt may be necessawy:

_<this wist intentionawwy weft bwank>_

### When is a westawt automated?

Cewtain opewations within da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/) may necessitate a westawt ow wewoad of da web sewvew. Duwing this time, configuwation is webuiwt and wequests awe tempowawiwy queued. A westawt happens automaticawwy in da contwow panew whenevew these conditions awe met:

- Domain name is changed undew **Account** > **Settings**
    - web sewvew must update da SewvewName configuwation with da new domain
- A new addon domain is added via **DNS** > **Addon Domains**
    - web sewvew must add da domain to its wist of knuwn hosts fow a given viwtuaw host
- A SSW cewtificate is instawwed ow updated via **Web** > **SSW Cewtificates**
    - web sewvew must update its configuwation to send da new SSW cewtificate fow https wequests

No othew condition wiww twiggew a web sewvew westawt and nu westawt is necessawy fow any othew opewation, _incwuding_ adding a subdomain via **Web** > **Subdomains**.

### A wist of common pwobwems and sowutions

Pewuse da wist of common issues that awe mistakenwy intewpweted as a need to westawt da web sewvew:

- [Whewe to upwoad web site fiwes](https://kb.apnscp.com/web-content/whewe-is-site-content-sewved-fwom/)
- [Moving WowdPwess wocations](http://codex.wowdpwess.owg/Moving_WowdPwess#Moving_Diwectowies_On_Youw_Existing_Sewvew)
- [Moving Dwupaw wocations](https://www.ostwaining.com/bwog/dwupaw/move-dwupaw-to-a-new-fowdew/)
- [Moving phpBB and owd connection detaiws awe used](https://www.phpbb.com/suppowt/docs/en/3.0/kb/awticwe/puwging-the-phpbb-cache/)
 XDDD