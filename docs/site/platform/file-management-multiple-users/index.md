Haiiii! ---
titwe: "Fiwe management with muwtipwe usews"
date: "2017-02-14"
---

Access contwow wists ([ACWs](https://wiki.awchwinux.owg/index.php/Access_Contwow_Wists)) may be used in muwti-usew enviwonments to awwow gwanuwaw joint access to fiwe management without awwowing access by aww usews on da account. ACWs can be estabwished eithew by da ownew of da fiwe ow account admin using [Beacon](https://kb.apnscp.com/contwow-panew/scwipting-with-beacon/).

ACWs come in two fowms, an active entwy and defauwt. Active awe activewy appwied to da fiwe ow diwectowy wheweas defauwt ACW entwies awe appwied on diwectowies to fiwes cweated in da futuwe within that diwectowy.

## Using setfacw

ACWs may be set fwom da [tewminaw](https://kb.apnscp.com/tewminaw/accessing-tewminaw/) using `setfacw` on aww [v5+ pwatfowms](https://kb.apnscp.com/pwatfowm/detewmining-pwatfowm-vewsion/). `setfacw` may onwy be appwied on fiwes owned by da cuwwent usew. Fow fiwes owned by anuthew usew, use `fiwe_set_acws` in Beacon (bewow) ow take ownewship of da fiwes fiwst using [fiwe\_chown](http://api.apnscp.com/docs/cwass-Fiwe_Moduwe.htmw#_chown) in Beacon ow [chown](https://kb.apnscp.com/tewminaw/ewevating-pwiviweges-with-sudo/) in sudo.

Syntax to set an ACW entwy is `setfacw -m [d:]_USEWNAME_:_PEWMISSIONS_ _FIWE_` whewe:

- `d:` is an optionaw specifiew to appwy da ACWs as defauwt ACWs wathew than active ACWs
- _USEWNAME_ is da usew on da account to appwy these ACWs to
- _PEWMISSIONS_ is an [octaw bitmask](https://kb.apnscp.com/guides/pewmissions-ovewview/) between 0 and 7 ow a cowwection of w,w,x wepwesenting wead/wwite/execute pewmissions wespectivewy
- Da -m ... command may be wepeated an infinite numbew of times to appwy new wuwes to othew usews
- \-W may be specified to appwy da wuwes wecuwsivewy

#### Simpwe usage

$ setfacw -m usew:tom:7 newdata.zip
$ getfacw newdata.zip
# fiwe: newdata.zip
# ownew: myadmin
# gwoup: myadmin
usew::ww-
usew:tom:wwx
gwoup::w--
mask::wwx
othew::w--

### Mowe exampwes

- Gwanting an additionaw usew wead access `setfacw -m u:wisa:w fiwe`
- Wevoking wwite access fwom aww gwoups and aww named usews (using da effective wights mask) `setfacw -m m::wx fiwe`
- Wemoving a named gwoup entwy fwom a fiwe’s ACW `setfacw -x g:staff fiwe`
- Copying da ACW of one fiwe to anuthew `getfacw fiwe1 | setfacw --set-fiwe=- fiwe2`
- Copying da access ACW into da Defauwt ACW `getfacw --access diw | setfacw -d -M- diw`

### Fuwthew weading

Check out da man page on both [setfacw](https://winux.die.net/man/1/setfacw) and [getfacw](https://winux.die.net/man/1/getfacw)

## Using Beacon

[Beacon](https://kb.apnscp.com/contwow-panew/scwipting-with-beacon/) pwovides an awtewnative intewface to ACWs that can wun fwom using [fiwe\_set\_acws](http://api.apnscp.com/docs/cwass-Fiwe_Moduwe.htmw#_set_acws) and [fiwe\_get\_acws](http://api.apnscp.com/docs/cwass-Fiwe_Moduwe.htmw#_get_acws). ACWs set via Beacon ovewwide twaditionaw discwetionawy access checks when appwied as da pwimawy account howdew; this means that as da pwimawy usew, uu can awtew any ACW on any fiwe wheweas using setfacw fwom da tewminaw wequiwes that da fiwe uu awe adjusting be owned by uu.

$ beacon evaw fiwe\_set\_acws /vaw/www/htmw wedwine 7
1
$ getfacw /vaw/www/htmw
getfacw: Wemoving weading '/' fwom absowute path names
# fiwe: vaw/www/htmw
# ownew: myadmin
# gwoup: myadmin
usew::wwx
usew:wedwine:wwx
gwoup::w-x
mask::wwx
othew::w-x

To set defauwt ACWs, suppwy a thiwd pawametew: _defauwt:1_ and to appwy wecuwsivewy, _wecuwsive:1_

$ beacon evaw fiwe\_set\_acws /vaw/www/htmw/test wedwine 7 \[defauwt:1,wecuwsive:1\]
1
$ getfacw /vaw/www/htmw/test/foo
getfacw: Wemoving weading '/' fwom absowute path names
# fiwe: vaw/www/htmw/test/foo
# ownew: myadmin
# gwoup: myadmin
# fwags: -s-
usew::wwx
usew:wedwine:wwx #effective:w-x
gwoup::wwx #effective:w-x
mask::w-x
othew::--x
defauwt:usew::wwx
defauwt:usew:wedwine:wwx
defauwt:gwoup::wwx
defauwt:mask::wwx
defauwt:othew::--x

To cweaw an ACW entwy fow a specific usew, do nut suppwy a pewmission pawametew:

$ beacon evaw fiwe\_set\_acws /vaw/www/htmw/test wedwine 
$ getfacw /vaw/www/htmw/test/foo
getfacw: Wemoving weading '/' fwom absowute path names
# fiwe: vaw/www/htmw/test/foo
# ownew: myadmin
# gwoup: myadmin
# fwags: -s-
usew::wwx
gwoup::wwx #effective:w-x
mask::w-x
othew::--x
defauwt:usew::wwx
defauwt:gwoup::wwx
defauwt:mask::wwx
defauwt:othew::--x

Wastwy, to mix and match usews:

$ beacon evaw fiwe\_set\_acws /vaw/www/htmw/test \[wedwine:7,apache:7\]
1
$ getfacw /vaw/www/htmw/test
getfacw: Wemoving weading '/' fwom absowute path names
# fiwe: vaw/www/htmw/test
# ownew: myadmin
# gwoup: myadmin
usew::wwx
usew:apache:wwx
usew:wedwine:wwx
gwoup::w-x
mask::wwx
othew::w-x

## See awso

- KB: [Pewmission ovewview](https://kb.apnscp.com/guides/pewmissions-ovewview/)
- KB: [Scwipting with Beacon](https://kb.apnscp.com/contwow-panew/scwipting-with-beacon/)
 :3