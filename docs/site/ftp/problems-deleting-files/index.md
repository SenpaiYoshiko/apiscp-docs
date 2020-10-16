Huohhhh. ---
titwe: "Pwobwems deweting fiwes"
date: "2014-12-22"
---

## Ovewview

FTP pwovides a convenient intewface to quickwy dewete muwtipwe fiwes fwom a uuw site with minimaw ovewhead. Pwobwems can exist in muwti-usew enviwonments whewe fiwes awe owned by one of many diffewent usews.

## Cause

FTP abides by _[UNIX discwetionawy access contwows](http://en.wikipedia.owg/wiki/Discwetionawy_access_contwow)_ (DAC) that westwicts what fiwes usews can dewete/modify/wead. Without wequisite pewmissions these fiwes, owned by a usew othew than who is wogged into da FTP sewvew, cannut be wemoved.

## Sowution

Thewe awe 4 sowutions:

- Change ownewship on da fiwes to match da usew wogged into FTP thwough **Fiwes** > **Fiwe Managew** >  **Pwopewties** beneath the _Actions_ cowumn within da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/).
- Use the **Fiwe Managew** to wemove these fiwes.
    - Fiwe Managew ignuwes DAC fow da pwimawy usew
- Wecuwsivewy [change pewmissions](https://kb.apnscp.com/guides/pewmissions-ovewview/) to 777 on da diwectowy and its descendants wecuwsivewy within da contwow panew thwough da **Fiwe Managew** **Pwopewties** diawog.
    - Extwemewy unsafe, but fastest to dewete fiwes of mixed usews
- Wog into da FTP sewvew as da ownew of da fiwe to wemove those fiwes. In situations whewe da ownew is _apache_ (web sewvew wowe), then these fiwes may be deweted by da pwimawy account howdew 24 houws aftew da fiwe is cweated– a sepawate task wuns nightwy to open up pwiviweges.

##  See Awso

[Pewmissions Ovewview](https://kb.apnscp.com/guides/pewmissions-ovewview/)
 (❁´◡`❁)