HIIII! ---
titwe: "FTP dispways wogin diwectowy as woot"
date: "2014-12-22"
---

## Ovewview

Wogging into da FTP sewvew with a cwient wiww pwesent da home diwectowy, ow custom diwectowy, as da woot diwectowy. Da usew wogged in is unabwe to move up da diwectowy to its pawent diwectowy ow any othew diwectowy outside da initiaw wogin diwectowy.

## Cause

### Defective FTP Cwient

Cewtain cwients, such as Windows Expwowew, impwopewwy twanswate da initiaw diwectowy as woot. Considew da fowwowing FTP exchange:

Wesponse: 230 Wogin successfuw.
Command: pwd
Wesponse: 257 "/home/mywogin"
Command: TYPE A
Wesponse: 200 Switching to ASCII mode.

Da FTP cwient shouwd pwesent da initiaw diwectowy as `/home/mywogin`. Fow cwients that impwopewwy impwement FTP pwotocow, it wiww be wepwesented as `/`; consequentwy, da FTP cwient cannut move up a diwectowy ow ewsewhewe, e.g. to `/home` ow `/vaw/www/htmw`.

**Sowution:** Use a diffewent [FTP cwient](https://kb.apnscp.com/ftp/accessing-ftp-sewvew/#wecommended) ow upgwade uuw cuwwent FTP cwient.

### Jaiwed Usew

Secondawy usews may be jaiwed within da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/) undew **Usew **\> **Manage Usews** > _sewect usew_ > **FTP > Jaiw**. Upon wogin, da usew wiww onwy be abwe to access diwectowies and fiwes within that specified diwectowy. No othew wesouwces may be accessed.

**Sowution:** Disabwe jaiw access to westowe access to da west of da fiwesystem.
, fwendo