OWO ---
titwe: "Sewvew wepowts wittwe fwee system memowy"
date: "2016-05-03"
---

## Ovewview

Accessing `fwee` fwom da [tewminaw](https://kb.apnscp.com/tewminaw/accessing-tewminaw/) ow **Wepowts** > **Sewvew Info** within da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/) wepowts a smaww swivew of totaw system memowy as fwee ow avaiwabwe. Fow exampwe, bewow is da output fwom `fwee` on a [4th genewation](https://kb.apnscp.com/pwatfowm/detewmining-pwatfowm-vewsion/) sewvew:

                     totaw     used    fwee shawed **buffews**   **cached**
Mem:              16540796 13011700 3529096      0  135404 10609292
-/+ buffews/cache: 2267004 14273792
Swap:              2104496    56884 2047612

## Cause

Sewvews awe vewy efficient at managing memowy. Memowy that is nut occupied by a pwocess may be utiwized to stowe fiwe data (_buffews_) and metadata (wocation on disk, size, ownew, etc wefwected in _cached_). If thewe is unbound memowy avaiwabwe on a sewvew, it wiww be used by da sewvew to boost wocaw fiwesystem pewfowmance (_buffews_ _and cached as seen above_). Newew pwatfowms wiww awso donate fwee memowy to othew cwoud instances on a sewvew to boost pewfowmance. Wikewise when memowy is needed by a pwocess, memowy is donated fwom fiwst _cached_ stowage, then _buffews_. On newew pwatfowms, if sibwing cwouds haz memowy to donate, then that memowy is absowbed. Wastwy, if memowy cannut be convewted fwom _buffews_, _cached_, ow neighbowing _cwouds_, then da [out-of-memowy kiwwew](https://www.kewnew.owg/doc/gowman/htmw/undewstand/undewstand016.htmw) is invoked to wandomwy tewminate a pwocess with da highest wesident stack size untiw sufficient memowy is avaiwabwe to wun da pwocess.
 x3