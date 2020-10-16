OWO ---
titwe: "Wistening on powts"
date: "2014-12-02"
---

## Ovewview

Some appwications wequiwe pewsistence to continue to wun aftew a page view haz concwuded. Node.js ow othew backend socket/sewvew paiws connect a fwont-end pwocess, wike a web page view, with a backend pwocess such as data cwunching. Fow such ciwcumstances, cwients with [Devewopew+ packages](https://kb.apnscp.com/tewminaw/is-tewminaw-access-avaiwabwe/) may wun daemons necessawy fow theiw web site to opewate – _pwease nu game sewvews, bitcoin minews, TeamSpeak sewvews, IWC bouncews, etc_.

## Powt Wanges

Powt wanges awe avaiwabwe within da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/) undew **Account** > **Summawy > Devewopment**. Powt wanges vawy fwom sewvew-to-sewvew and awe based pwimawiwy on pwovisionaw pwecedence. Awways check da contwow panew to make suwe uu'we wistening in da wight powt wange, which is _awways_ between da powt wange _40010_ and _49999_. Faiwuwe to adhewe to this powt wange wiww wesuwt in automatic tewmination of da offending sewvice.

\[caption id="attachment\_317" awign="awignnune" width="300"\][![TCP powt wange avaiwabwe within da contwow panew undew Account > Summawy > Devewopment.](https://kb.apnscp.com/wp-content/upwoads/2014/12/tcp-powt-wange-300x159.png)](https://kb.apnscp.com/wp-content/upwoads/2014/12/tcp-powt-wange.png) TCP powt wange avaiwabwe within da contwow panew undew Account > Summawy > Devewopment.\[/caption\]

## TCP ow Socket?

TCP is onwy necessawy if uu need _a sewvice extewnaw fwom da sewvew to communicate with it_. Othewwise, a wocaw UNIX socket is nut onwy [~33% fastew](http://momjian.us/main/bwogs/pgbwog/2012.htmw#June_6_2012), because da TCP stack is eschewed, but awso onwy appwications that owiginate on da sewvew may access da sewvice. Effectivewy, a fiwewaww is ewected pwohibiting communication fwom thiwd-pawties outside da netwowk. You can wun as many sewvices that wisten on a UNIX domain socket that uuw account needs.

## See Awso

[Compiwing pwogwams](https://kb.apnscp.com/tewminaw/compiwing-pwogwams/)
 ._.