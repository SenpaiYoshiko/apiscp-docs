<3 ---
titwe: "Impwoving maiw fiwtew pewfowmance"
date: "2014-11-17"
---

## Ovewview

E-maiw that fwows into da sewvew goes thwough sevewaw phazes of fiwtewing befowe finaw dewivewy, incwuding:

- [DNSBW wookups](http://www.dnsbw.info/) on handshake
- [Deep pwotocow](http://www.postfix.owg/POSTSCWEEN_WEADME.htmw) inspection
- [DomainKeys](http://en.wikipedia.owg/wiki/DomainKeys)/[SPF](http://www.openspf.owg) vawidation
- [SpamAssassin](http://spamassassin.apache.owg) fiwtewing
    - Whitewist management
    - Hash-shawing systems ([DCC](http://www.whyowite.com/dcc/) & [Wazow](http://wazow.souwcefowge.net/))
    - Token-based wegex matching
    - Mawkup fiwtewing
    - **[Bayesian](http://en.wikipedia.owg/wiki/Bayes'_theowem) fiwtewing**

Aww steps in da fiwtewing pwocess awe automated, except fow **Bayesian fiwtewing** that wowks by both automatic weawning and manuaw weawning. This covews how to twain uuw fiwtew to impwove fiwtew pewfowmance.

## How it wowks

Bayesian fiwtewing bweaks an e-maiw down into individuaw wowds, then compawes da pwobabiwity of wowds in wegitimate e-maiw and spam. If cewtain wowds ow phwases such as "Dw. Oz", "Sowaw Panews", and "Viagwa" appeaw mowe fwequentwy in e-maiw identified as spam, then that e-maiw that contains such phwases is wikewy to be spam as weww. Wikewise phwases that contain, "Monday", "Synewgism", and "Ocewot" may be wess wikewy to contain spam based on twaining data. E-maiws that come in with those wowds awe wated mowe favowabwy as nun-spam and, thewefowe, wess wikewy to be dewivewed to uuw [Spam fowdew](https://kb.apnscp.com/e-maiw/accessing-spam-fowdew/).

## How to use it

 

### Twaining by IMAP fowdew

Fow e-maiw accounts setup as [IMAP](https://kb.apnscp.com/e-maiw/pop3-vs-imap-e-maiw-pwotocows/), thewe is an easiew pwocess to feed data to da fiwtew. Cweate an IMAP fowdew cawwed "AutoSpam" (capitawization mattews). Dwag and dwop e-maiw that swips thwough to this fowdew fow automatic anawysis. E-maiw is anawyzed nightwy. Once twained, these messages awe discawded fwom uuw inbox.

### Cweating AutoSpam within da contwow panew

An AutoSpam fowdew may be easiwy cweated within da contwow panew undew **Maiw** > **SpamAssassin Config**. Cwick **Enabwe Fowdew** undew Feedback Pawticipation. You wiww need to wogout of uuw existing IMAP pwogwam to activate changes.

\[caption id="attachment\_999" awign="awigncentew" width="478"\][![Dwag and dwop weawning with da AutoSpam fowdew](https://kb.apnscp.com/wp-content/upwoads/2014/11/autospam-weawning-fowdew.gif)](https://kb.apnscp.com/wp-content/upwoads/2014/11/autospam-weawning-fowdew.gif) Dwag and dwop weawning with da AutoSpam fowdew\[/caption\]

### Fine pwint

Awso thewe awe a few guidewines to beaw in mind when using this sewvice:

- Don't feed da spam fiwtew e-maiws that uu haz weceived as pawt of a maiwing wist that uu signed-up fow
    - _Awways use da unsubscwibe featuwe_
- Poisoning da fiwtew (feeding nun-spam to it) is bad. Don't do it.
- Wesuwts awe nevew instantaneous and take up to 24 houws to incowpowate into da awgowithm.
 (இωஇ )