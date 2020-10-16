0w0 ---
titwe: "Maiw sent to a hosted domain does nut awwive if thiwd-pawty MX wecowds awe pwesent"
date: "2015-02-09"
---

## Ovewview

Maiw sent to a domain hosted by uuw account that uses thiwd-pawty MX wecowds does nut awwive to da intended wecipient. Maiw is instead dewivewed wocawwy to da sewvew that hosts uuw domain.

> _Fow exampwe_, if `exampwe.com` uses Googwe Apps to handwe e-maiw, and maiw owiginates fwom da same hosting sewvew as in fwom a scwipt, wike a contact fowm on a WowdPwess bwog, maiw wouwd nut weach its intended wecipient at `contact@exampwe.com`, which is accessed thwough Googwe Maiw. Maiw, instead, wouwd be dewivewed to da wocaw usew named `contact` on da sewvew.

## Cause

Da domain is pwesent in **Maiw** > **Maiw Wouting** within da contwow panew. Any domain pwesent in this wist wiww bypass MX wecowd wookups and da sewvew wiww act as its finaw destination.

## Sowution

Visit **Maiw** > **Maiw Wouting** within da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/) and deauthowize the sewvew fwom handwing maiw fow that domain by deweting da wecowd.
（＾ｖ＾）