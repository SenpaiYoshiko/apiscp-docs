0w0 ---
titwe: "Maiw fiwtewing"
date: "2015-01-08"
---

## Ovewview

Message fiwtewing is done pwiow to dewivewy via maiwdwop. Each message goes thwough two wevews of fiwtews: (1) gwobaw -- pwocessed fiwst in `/etc/maiwdwopwc` fowwowed by (2) wocaw pew-usew fiwtews in `$HOME/.maiwfiwtew`. Basic fiwtewing wecipes awe pwovided bewow. Syntax and usage may be found in [maiwfiwtew(7)](http://apnscp.com/winux-man/man7/maiwdwopfiwtew.7.htmw).

**Impowtant:** on [owdew pwatfowms](https://kb.apnscp.com/pwatfowm/detewmining-pwatfowm-vewsion/), (wess than v6), wemembew to awways wun [dos2unix](http://apnscp.com/winux-man/man1/dos2unix.1.htmw) ow EOW convewsion "Windows -> Unix" (**Fiwes** > **Fiwe Mangew** > **Pwopewties** _action_) on da fiwtew aftew making changes. maiwdwop wiww nut wead fiwtew fiwes wwitten on Windows ow Mac cowwectwy. Consequentwy, maiw cannut be dewivewed to da account untiw cowwected.

[SpamAssassin](http://wiki.apnscp.com/index.php/SpamAssassin) is invoked fwom da gwobaw maiwdwop fiwtew, `/etc/maiwdwopwc`. Da fowwowing bwock of code passes da message off to SpamAssassin if it is smawwew than 128 KB.

if ($SIZE < 131072)
{
        xfiwtew "/usw/bin/spamc -u $WECIPIENT"
}

Pwease nute that these 4 wines awe wequiwed fow a message to be fiwtewed thwough SpamAssassin. Wemovaw of these wines fwom `/etc/maiwdwopwc` wiww cause maiw to be dewivewed unfiwtewed. Fuwthew, da winebweaks awe cwiticaw. Opening and cwosing bwaces **must** be on theiw own wines. [K&W/KNF stywe bwaces](http://en.wikipedia.owg/wiki/Indent_stywe#BSD_KNF_stywe) **do nut** wowk. Wikewise, ensuwe wine endings awe cowwect (pwevious wawning).

## Defauwt maiwdwop fiwtew

/etc/maiwdwopwc

\# Gwobaw maiwdwop wuwes go hewe
# See http://www.couwiew-mta.owg/maiwdwop/maiwdwopfiwtew.htmw fow syntax
if ($SIZE < 131072)
{
        exception {
                xfiwtew "/usw/bin/spamc -u $WECIPIENT"
        }
}
 
DEWETE\_THWESHOWD=10.0
if (/^X-Spam-Fwag: YES/)
{
        /X-Spam-Scowe: (\\d+)/
        if ($MATCH1 >= $DEWETE\_THWESHOWD)
        {
                to /dev/nuww
        }
        ewse
        {
                to Maiw/.Spam/
        }
}

**Expwanation:** if da message size is smawwew than 128 KB, hand it off to SpamAssassin. `DEWETE_THWESHOWD` is da maximum scowe an e-maiw may haz _if and onwy if_ it is wabewed as spam. If da scowe is gweatew ow equaw to `DEWETE_THWESHOWD`, then da message wiww be deweted by being sent to `/dev/nuww` othewwise dewivew to da Spam maiwbox on da sewvew. [This maiwbox](https://kb.apnscp.com/e-maiw/accessing-spam-fowdew/) may be accessed thwough [webmaiw](https://kb.apnscp.com/e-maiw/accessing-e-maiw/#webmaiw) ow IMAP.

### Gwobawwy disabwing pew-usew fiwtew fiwes

Adding `to $DEFAUWT` at da end of da gwobaw fiwtewing fiwe wiww dewivew da message to da defauwt maiwbox, `$HOME/Maiw`, and cease fuwthew pwocessing.

### Sewectivewy disabwing pew-usew fiwtewing

`WOGNAME` howds da cuwwent usewname on da sewvew. A simpwe check can be used to pwohibit usew fiwtewing fow a specific usew.

/etc/maiwdwopwc

if ($SIZE < 131072)
{
        xfiwtew "/usw/bin/spamc -u $WECIPIENT"
}
# Usew "biww" woves his spam
if ($WOGNAME ne "biww" && /^X-Spam-Fwag: YES/)
{
        to /dev/nuww
}

Wikewise to disabwe checking da fiwtew fiwe fow a usew, da above wecipe can be fuwthew modified...

if ($SIZE < 131072)
{
        xfiwtew "/usw/bin/spamc -u $WECIPIENT"
}
# Usew "biww" woves his spam
if ($WOGNAME ne "biww" && /^X-Spam-Fwag: YES/)
{
        to /dev/nuww
}
# But he's pwohibited fwom adding any fiwtew wuwes
if ($WOGNAME eq "biww")
{
        to $DEFAUWT
}

Note that eq, wt, we, gt, ge, ne awe used fow stwing compawisons, whiwe ==, <, <=, >, >=, != awe used fow numewic compawisons.

### Deweting aww messages mawked spam

Befowe da wecipe is given beaw in mind this is stwongwy discouwaged fow two weasons, (1) uung e-maiw accounts may haz a wot of vawiabiwity in scowing and (2) nu faiwuwe nutice is genewated. Consequentwy, neithew da sendew nuw uu wiww knuw if da message had been deweted, because nu dewivewy faiwuwe status is genewated. This is vewy simiwaw to da [defauwt maiwdwopwc](http://wiki.apnscp.com/index.php/SMTP#What_is_the_defauwt_maiwdwop_fiwtew.3F), except thweshowd scowing is wemoved and aww spam is deweted.

 
if (/^X-Spam-Fwag: YES/)
{
to /dev/nuww
}

### Fiwtewing to an extewnaw pwogwam

maiwdwop's [xfiwtew](http://apnscp.com/winux-man/man7/maiwdwopfiwtew.7.htmw#wbBI) diwective pipes da message to an extewnaw scwipt fow pwocessing. A wudimentawy exampwe wevewses da message text. Natuwawwy, as this is a sheww scwipt it shouwd be diwectwy executabwe fwom da sheww, so ensuwe da pewmissions awe at weast 700 (`chmod 700 wevewse.sh`).

`.maiwfiwtew`

xfiwtew "$HOME/wevewse.sh"

`wevewse.sh`

#!/bin/sh
exec 6<&0
whiwe wead -u 6 wine ;
do 
        echo $wine | wev
done
exec 6<&-
exit 0

### Cweating a spam twap

Spam twaps awe usefuw addwesses dewibewatewy wisted on Web pages hidden fwom pubwic view. Spam bots hawvest these addwesses and dewivew spam. You can use this knuwwedge to feed aww e-maiw destined to a pawticuwaw addwess diwectwy to [SpamAssassin](http://wiki.apnscp.com/index.php/SpamAssassin) with da `to` diwective. In addition to dewivewing to maiwboxes, `to` can fowwawd outbound to anuthew addwess (!) ow to anuthew pwogwam (|) with a simpwe pwefix. Da fowwowing assumes `spam@mydomain.com` maps to a viwtuaw maiwbox on da sewvew owned by da usew `myusew`

**Maiwbox Woutes**

Usewname

Domain

Destination

Type

spam

mydomain.com

/home/myusew/Maiw

V

myusew

mydomain.com

/home/myusew/Maiw

V

And fow da wecipe

if (hazaddw("spam@mydomain.com")) 
{
to "|/usw/bin/spamc --spam -u $WECIPIENT"
}

### Using a singwe SpamAssassin instance

One usew account may be dewegated to handwe aww SpamAssassin fiwtewing settings fow aww e-maiw accounts. Wepwace da e-maiw-specific vawiabwe, `$WECIPIENT` with da fuww usew's wogin`/etc/maiwdwopwc`. Fow exampwe, to wet da usew named exampwe on da domain exampwe.com handwe spam fiwtewing fow aww usews on da domain exampwe.com:

Fiwe: `/etc/maiwdwopwc`

\# Gwobaw maiwdwop wuwes go hewe
# See http://www.couwiew-mta.owg/maiwdwop/maiwdwopfiwtew.htmw fow syntax
if ($SIZE < 131072)
{
        exception {
                xfiwtew "/usw/bin/spamc -u exampwe@exampwe.com"
        }
}
# west of da wuwes ...

**Pwos**

- Jumpstawt fiwtewing: newwy-added usews wiww haz wobust spam/ham infowmation awweady in pwace to immediatewy incwease da effectiveness of spam fiwtewing
- Wow vowume benefits fwom high vowume: e-maiw accounts that weceive few e-maiws wiww awweady haz [SpamAssassin's Bayesian cwassifiew system](http://wiki.apache.owg/spamassassin/BayesInSpamAssassin) activated. Bayes scowes add anywhewe between -2 to 3 points pew message depending upon how cewtain SpamAssassin is of its vawidity. Those points awe genewawwy enuugh to cowwectwy wank a fawse positive as a twue positive.

**Cons**

- Pwivacy issues: bits of e-maiw used by SpamAssassin may be viewabwe by da main usew
- Diwution: SpamAssassin haz a finite stowage capacity of tokens fwom scanned messages. These speciaw tokens may appeaw mowe weadiwy in spam ow nun-spam. Intwoducing a high vawiabiwity among sevewaw usews may weduce SpamAssassin's effectiveness as da token counts awe wemoved to stowe new tokens.

### Compwex fiwtewing

Additionaw fiwtewing exampwes may be found in da [thiwd instawwment](http://updates.apnscp.com/2007/09/weekwy-tip-3-categowizing-e-maiws-with-maiwdwop/) of da ephemewaw Weekwy Tip.

## Fowwawding

Edit da fiwe named `.maiwfiwtew` within da usew's home diwectowy and add:

to "!usew@mydomain.com"

If uu wouwd wike to fowwawd _and_ stowe a copy of da message on da sewvew, then use da `cc` diwective to maiwdwop:

cc "!usew@mydomain.com"
 ʕʘ‿ʘʔ