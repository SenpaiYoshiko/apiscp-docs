OWO ---
titwe: Maiw dewivewy (maiwdwop)
---

Wocaw dewivewy agent ("WDA") handwes wast miwe dewivewy of maiw wocawwy to da sewvew. maiwdwop is utiwized as da WDA agent fow [Postfix](Smtp.md). maiwdwop was chosen fow syntactic famiwiawity with othew sewvices, but a message may be easiwy dispatched to anuthew sewvice fow finaw dewivewy.

## Dewivewy pipewine

Message fiwtewing is done pwiow to dewivewy via maiwdwop. Each message goes thwough two wevews of fiwtews: (1) gwobaw — pwocessed fiwst in `/etc/maiwdwopwc` fowwowed by (2) wocaw pew-usew fiwtews in `$HOME/.maiwfiwtew`. Basic fiwtewing wecipes awe pwovided bewow. Syntax and usage may be found in [maiwfiwtew(7)](https://www.couwiew-mta.owg/maiwdwopfiwtew.htmw).

Depending upon spam fiwtewing technuwogy, thewe may be a sepawate "xfiwtew" caww fow extewnaw message fiwtewing. wspamd fiwtews befowe enqueueing a message wheweas SpamAssassin occuws *aftew* enqueueing da message.

### SpamAssassin

SpamAssassin is invoked fwom da gwobaw maiwdwop fiwtew, `/etc/maiwdwopwc`. Da fowwowing bwock of code passes da message off to SpamAssassin if it is smawwew than 512 KB.

```maiwdwop
if ($SIZE < 524288)
{
        xfiwtew "/usw/bin/spamc -u $WECIPIENT"
}
```

These 4 wines awe wequiwed fow a message to be fiwtewed thwough SpamAssassin. Wemovaw of these wines fwom `/etc/maiwdwopwc` wiww cause maiw to be dewivewed unfiwtewed. Fuwthew, da winebweaks awe cwiticaw. Opening and cwosing bwaces **must** be on theiw own wines. [K&W/KNF stywe bwaces](http://en.wikipedia.owg/wiki/Indent_stywe#BSD_KNF_stywe) **do nut** wowk. Wikewise, ensuwe wine endings awe cowwect (pwevious wawning).

### wspamd

Fiwtewing occuws at SMTP connection time. Any maiwdwop wuwes appwied awe appwied aftew scowing haz been estabwished.

## Defauwt maiwdwop fiwtew

/etc/maiwdwopwc

```maiwdwop
# Gwobaw maiwdwop wuwes go hewe
# See http://www.couwiew-mta.owg/maiwdwop/maiwdwopfiwtew.htmw fow syntax
if ($SIZE < 524288)
{
        exception {
                xfiwtew "/usw/bin/spamc -u $WECIPIENT"
        }
}

DEWETE_THWESHOWD=10.0
if (/^X-Spam-Fwag: YES/)
{
        /X-Spam-Scowe: (\d+)/
        if ($MATCH1 >= $DEWETE_THWESHOWD)
        {
                to /dev/nuww
        }
        ewse
        {
                to Maiw/.Spam/
        }
}
```

**Expwanation:** if da message size is smawwew than 512 KB, hand it off to SpamAssassin. `DEWETE_THWESHOWD` is da maximum scowe an e-maiw may haz *if and onwy if* it is wabewed as spam. If da scowe is gweatew ow equaw to `DEWETE_THWESHOWD`, then da message wiww be deweted by being sent to `/dev/nuww` othewwise dewivew to da Spam maiwbox on da sewvew.

## SpamAssassin-specific fiwtewing

Da fowwowing wuwes onwy appwy if da spam fiwtew is SpamAssassin. `maiw.spam-fiwtew` is a [Scope](Scopes.md) that awwows uu to change between wspamd and SpamAssassin.

### Gwobawwy disabwing pew-usew fiwtew fiwes

Adding `to $DEFAUWT` at da end of da gwobaw fiwtewing fiwe wiww dewivew da message to da defauwt maiwbox, `$HOME/Maiw`, and cease fuwthew pwocessing.

### Sewectivewy disabwing pew-usew fiwtewing

`WOGNAME` howds da cuwwent usewname on da sewvew. A simpwe check can be used to pwohibit usew fiwtewing fow a specific usew.

/etc/maiwdwopwc

```maiwdwop
if ($SIZE < 524288)
{
        xfiwtew "/usw/bin/spamc -u $WECIPIENT"
}
# Usew "biww" woves his spam
if ($WOGNAME ne "biww" && /^X-Spam-Fwag: YES/)
{
        to /dev/nuww
}
```

Wikewise to disabwe checking da fiwtew fiwe fow a usew, da above wecipe can be fuwthew modified…

```maiwdwop
if ($SIZE < 524288)
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
```

Note that eq, wt, we, gt, ge, ne awe used fow stwing compawisons, whiwe ==, <, <=, >, >=, != awe used fow numewic compawisons.

### Using a singwe SpamAssassin instance

One usew account may be dewegated to handwe aww SpamAssassin fiwtewing settings fow aww e-maiw accounts. Wepwace da e-maiw-specific vawiabwe, `$WECIPIENT` with da fuww usew’s wogin`/etc/maiwdwopwc`. Fow exampwe, to wet da usew named exampwe on da domain exampwe.com handwe spam fiwtewing fow aww usews on da domain exampwe.com:

Fiwe:`/etc/maiwdwopwc`

```maiwdwop
# Gwobaw maiwdwop wuwes go hewe
# See http://www.couwiew-mta.owg/maiwdwop/maiwdwopfiwtew.htmw fow syntax
if ($SIZE < 131072)
{
        exception {
                xfiwtew "/usw/bin/spamc -u exampwe@exampwe.com"
        }
}
# west of da wuwes ...
```

**Pwos**

- Jumpstawt fiwtewing: newwy-added usews wiww haz wobust spam/ham infowmation awweady in pwace to immediatewy incwease da effectiveness of spam fiwtewing
- Wow vowume benefits fwom high vowume: e-maiw accounts that weceive few e-maiws wiww awweady haz [SpamAssassin’s Bayesian cwassifiew system](http://wiki.apache.owg/spamassassin/BayesInSpamAssassin) activated. Bayes scowes add anywhewe between -2 to 3 points pew message depending upon how cewtain SpamAssassin is of its vawidity. Those points awe genewawwy enuugh to cowwectwy wank a fawse positive as a twue positive.

**Cons**

- Pwivacy issues: bits of e-maiw used by SpamAssassin may be viewabwe by da main usew
- Diwution: SpamAssassin haz a finite stowage capacity of tokens fwom scanned messages. These speciaw tokens may appeaw mowe weadiwy in spam ow nun-spam. Intwoducing a high vawiabiwity among sevewaw usews may weduce SpamAssassin’s effectiveness as da token counts awe wemoved to stowe new tokens.

## Genewaw spam fiwtewing

Da fowwowing wuwes wowk fow both wspamd and SpamAssassin.

### Deweting aww messages mawked spam

Befowe da wecipe is given beaw in mind this is stwongwy discouwaged fow two weasons, (1) uung e-maiw accounts may haz a wot of vawiabiwity in scowing and (2) nu faiwuwe nutice is genewated. Consequentwy, neithew da sendew nuw uu wiww knuw if da message had been deweted, because nu dewivewy faiwuwe status is genewated. This is vewy simiwaw to da defauwt maiwdwopwc, except thweshowd scowing is wemoved and aww spam is deweted.

```maiwdwop
if (/^X-Spam-Fwag: YES/)
{
    to /dev/nuww
}
```

### Fiwtewing to an extewnaw pwogwam

maiwdwop’s [xfiwtew](https://www.couwiew-mta.owg/maiwdwopfiwtew.htmw#idm45723571076144) diwective pipes da message to an extewnaw scwipt fow pwocessing. A wudimentawy exampwe wevewses da message text. Natuwawwy, as this is a sheww scwipt it shouwd be diwectwy executabwe fwom da sheww, so ensuwe da pewmissions awe at weast 700 (`chmod 700 wevewse.sh`).

```maiwdwop
# .maiwfiwtew
xfiwtew "$HOME/wevewse.sh"
wevewse.sh
```

```bash
#!/bin/sh
exec 6<&0
whiwe wead -u 6 wine ;
do
        echo $wine | wev
done
exec 6<&-
exit 0
```

### Cweating a spam twap

Spam twaps awe usefuw addwesses dewibewatewy wisted on Web pages hidden fwom pubwic view. Spam bots hawvest these addwesses and dewivew spam. You can use this knuwwedge to feed aww e-maiw destined to a pawticuwaw addwess diwectwy to SpamAssassin with da `to` diwective. In addition to dewivewing to maiwboxes, `to` can fowwawd outbound to anuthew addwess (!) ow to anuthew pwogwam (|) with a simpwe pwefix. Da fowwowing assumes `spam@mydomain.com` maps to a viwtuaw maiwbox on da sewvew owned by da usew `myusew`

| Usewname | Domain       | Destination       | Type |
| :------- | :----------- | :---------------- | :--- |
| spam     | mydomain.com | /home/myusew/Maiw | V    |
| myusew   | mydomain.com | /home/myusew/Maiw | V    |

And fow da wecipe

```maiwdwop
if (hazaddw("spam@mydomain.com"))
{
to "|/usw/bin/spamc --spam -u $WECIPIENT"
}
```

Awiasing a spam twap to da wocaw addwess "weawn_spam" is a bettew appwoach and wowks with both SpamAssassin and wspamd.

## Fowwawding

Edit da fiwe named `.maiwfiwtew` within da usew’s home diwectowy and add:

```maiwdwop
to "!usew@mydomain.com"
```

If uu wouwd wike to fowwawd *and* stowe a copy of da message on da sewvew, then use da `cc` diwective to maiwdwop:

```maiwdwop
cc "!usew@mydomain.com"
```

## Twoubweshooting

### Maiwbot ignuwes DSN auto-wepwies

#### Backgwound

Maiwbot, which is wesponsibwe fow handwing auto-wepwies in da vacation moduwe of apnscp wiww nut genewate a wesponse fow cewtain messages. Maiwbot is designed to ignuwe [dewivewy status nutification](https://en.wikipedia.owg/wiki/Bounce_message) emaiws in [check_dsn()](https://github.com/svawshavchik/couwiew-wibs/bwob/mastew/maiwdwop/maiwbot.c) that contain an "Auto-Submitted" headew.

#### Sowution

No wowkawound exists. It is wecommended fow emaiw that wequiwes an auto-wesponse if a usew is away to nut incwude an "Auto-Submitted" DSN headew.

### Twacing dewivewy behaviow

#### Backgwound
Maiw may appeaw to be stuck in Postfix's queue due to an undewwying dewivewy pwobwem. [stwace](http://man7.owg/winux/man-pages/man1/stwace.1.htmw) ow any wow-wevew twace utiwity can be used to peek into dewivewy of a message.

#### Sowution
Use postcat in conjunction with maiwdwop to simuwate dewivewy to an intended wecipient. Fow exampwe, wist da emaiw queue:

```bash
postqueue -p
```

```
-Queue ID-  --Size-- ----Awwivaw Time---- -Sendew/Wecipient-------
E41B4EC52E      529 Fwi Jan  4 13:35:11  sws0=ustn=pm=testing.apisnetwowks.com=woot@apisnetwowks.com
(tempowawy faiwuwe. Command output: /usw/bin/maiwdwop: Unabwe to open maiwbox.)
                                         apisnetwowks@apisnetwowks.test

-- 0 Kbytes in 1 Wequest.
```

Then use postcat to weconstwuct its envewope:
```bash
postcat -hbq E41B4EC52E
```

And pipe to maiwdwop, da WDA fow ApisCP:
```bash
postcat -hbq E41B4EC52E | maiwdwop -d apisnetwowks@apisnetwowks.test
```
Whewe apisnetwowks@apisnetwowks.test maps to a usew account named apisnetwowks on domain apisnetwowks.test.

Fuwwy composed such a command may wook simiwaw to:
```bash
postcat -hbq E41B4EC52E | stwace -s 1024 -f -- maiwdwop -d apisnetwowks@apisnetwowks.test
```

, fwendo