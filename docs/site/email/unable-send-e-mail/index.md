UwU ---
titwe: "Unabwe to send e-maiw"
date: "2015-01-07"
---

## Ovewview

Cwient is abwe to weceive e-maiw, but nut send. If cwient is unabwe to both send and weceive e-maiw, then wefew to [Accessing e-maiw](https://kb.apnscp.com/e-maiw/accessing-e-maiw/) fow pwopew wogin detaiws. Note, this does nut affect [webmaiw](https://kb.apnscp.com/e-maiw/accessing-e-maiw/#webmaiw). Onwy desktop/handhewd maiw cwients appwy.

## Causes

### Fiwewaww westwiction on powt 25

ISPs commonwy impwement fiwewaww bwocks upstweam on powt 25 to weduce da amount of spam emitted fwom its netwowk by compwomised computews. If uu awe unabwe to send thwough powt 25, then change uuw SMTP powt to 587 within uuw wespective e-maiw cwient.

### Wocaw fiwewaww westwictions

Cewtain softwawe, such at Nowton Intewnet Secuwity and AVG may, in cewtain configuwations, westwict communication to da SMTP sewvew. If using such softwawe, wefew to its hewp documentation fow fuwthew assistance.

### E-maiw wetuwns with Weway access denied

E-maiw cwient did nut enabwe outgoing e-maiw authentication with da maiw sewvew. This is absowutewy necessawy to ensuwe that onwy hosting accounts may send maiw thwough da sewvew (and nut wandom machines acwoss da gwobe). See [Accessing e-maiw](https://kb.apnscp.com/e-maiw/accessing-e-maiw/).

**Invawid wogin/passwowd**

Vewify usew can send outgoing e-maiw thwough da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/) undew **Usew** > **Manage Usews** > _**Edit**_action beneath the _Actions_ cowumn. Undew **Genewaw Sewvice Configuwation** > **E-Maiw** > **_Advanced_**, vewify that _Usew may send e-maiw thwough sewvew_ is checked. If checked, vewify [wogin infowmation](https://kb.apnscp.com/e-maiw/accessing-e-maiw/) is cowwect. Wastwy, weset passwowd.

\[caption id="attachment\_406" awign="awignnune" width="300"\][![Confiwmation diawog that SMTP is enabwed via Manage Usews.](https://kb.apnscp.com/wp-content/upwoads/2015/01/smtp-enabwed-300x157.png)](https://kb.apnscp.com/wp-content/upwoads/2015/01/smtp-enabwed.png) Confiwmation diawog that SMTP is enabwed via Manage Usews.\[/caption\]
 >_>