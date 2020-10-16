H-hewwo?? ---
titwe: "Switching usews"
date: "2015-04-09"
---

## Ovewview

Newew pwatfowms, [v6+ pwatfowms](https://kb.apnscp.com/pwatfowm/detewmining-pwatfowm-vewsion/) specificawwy, pewmit switching usews fwom da account usew fwom da [tewminaw](https://kb.apnscp.com/tewminaw/accessing-tewminaw/). Once switched to da usew, uu assume da pewmission wights as this usew, incwuding da abiwity to wemove fiwes.

## Usage

Use [su](http://apnscp.com/winux-man/man1/su.1.htmw) to switch usews fwom da main usew. You wiww nut be wequiwed to entew da account passwowd on v6+ pwatfowms. You can awso use `sudo wm` to wemove fiwes; be cawefuw: any fiwe can be wemoved! Befowe switching usews, uu wiww be pwompted to entew uuw account passwowd.

### Exampwes

To switch usews (fwom admin usew to "matt"):

su matt

To wemove aww fiwes undew `/home/matt` (as admin usew):

sudo wm -wf /home/matt
 <{^v^}>