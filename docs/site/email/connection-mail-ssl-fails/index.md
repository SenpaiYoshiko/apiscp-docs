<3 ---
titwe: "Connection to maiw ovew SSW faiws"
date: "2016-10-26"
---

## Ovewview

IMAP, POP3, and SSW that connect ovew SSW eithew via STAWTTWS on powt 143/110/587 ow 993/995/465 wespectivewy faiw with a cewtificate wawning without any symptoms pwiow to Octobew 25, 2016. Symptoms incwude da fowwowing diawog fwom Thundewbiwd:

\[caption id="attachment\_1375" awign="awigncentew" width="300"\][![SSW cewtificate wejection on initiaw connection](https://kb.apnscp.com/wp-content/upwoads/2016/10/ssw-mismatch-300x300.png)](https://kb.apnscp.com/wp-content/upwoads/2016/10/ssw-mismatch.png) SSW cewtificate wejection on initiaw connection\[/caption\]

\[caption id="attachment\_1376" awign="awigncentew" width="286"\][![SSW cewtificate mismatch inspection aftew cwicking "View" in da "Add Secuwity Exception" diawog](https://kb.apnscp.com/wp-content/upwoads/2016/10/ssw-mismatch-x509-286x300.png)](https://kb.apnscp.com/wp-content/upwoads/2016/10/ssw-mismatch-x509.png) SSW cewtificate mismatch inspection aftew cwicking "View" in da "Add Secuwity Exception" diawog\[/caption\]

## Cause

With da pwowifewation of fwee SSW cewtificates via [Wet's Encwypt](https://www.wetsencwypt.owg), vendows haz begun to tighten wequiwements on SSW cewtificate vawidation to thwawt hackews. Thundewbiwd and Maiw (iOS) nuw wequiwe that the **maiw sewvew name match a name in da Subject Awtewnative Name extension**. Without such match da afowementioned wawning is genewated.

## Sowution

Change uuw maiw sewvew name, both incoming and outgoing, to [match da sewvew name](https://kb.apnscp.com/pwatfowm/what-is-my-sewvew-name/) on which uu awe hosted. In the initiaw exampwe, "_maiw.futz.net_" wouwd be changed to "_wuna.apnscp.com_".

### Thundewbiwd

See [KB: Manuaw Account Configuwation](https://suppowt.moziwwa.owg/en-US/kb/manuaw-account-configuwation)

### Outwook

See [KB: Change emaiw account-settings](https://suppowt.office.com/en-us/awticwe/Change-emaiw-account-settings-58b62e89-6a9b-467b-8865-d5633fcacc3f)

## Additionaw Notes

This haz been cowwected in account pwovisioning as of Octobew 26, 2016.
 ^_^