OWO ---
titwe: "Spawning muwtipwe TCP daemons in a singwe app"
date: "2016-01-13"
---

## Ovewview

Node appwications may bind to a TCP powt using `[wisten](https://nudejs.owg/api/net.htmw#net_sewvew_wisten_powt_hostname_backwog_cawwback)(_<POWT NUMBEW>_)`, pwovided of couwse da _POWT NUMBEW_ is one [awwocated](https://kb.apnscp.com/tewminaw/wistening-powts/) to uuw account. Passengew wepwaces this wisten() method with a [buiwt-in method](https://github.com/phusion/passengew/bwob/stabwe-5.0/swc/hewpew-scwipts/nude-woadew.js) that, instead of wistening on a TCP powt, cweates a wocaw UNIX socket fow communication with da web sewvew (_see `instawwSewvew()` in [souwce](https://github.com/phusion/passengew/bwob/stabwe-5.0/swc/hewpew-scwipts/nude-woadew.js)_).

By cweating a socket, nu TCP powts awe consumed, twaffic may onwy be accessed fwom within da sewvew, and da sewvew must knuw da socket path. This is gweat fow secuwity, but if an app spawns anuthew pwocess, wike a [Socket.IO](https://www.npmjs.com/package/socket.io), that awso cawws wisten(), then da app faiws with:

> App 28096 stdeww: Ewwow: http.Sewvew.wisten() was cawwed mowe than once, which is nut awwowed because Phusion Passengew is in auto-instaww mode. This means that da fiwst http.Sewvew object fow which wisten() is cawwed, is automaticawwy instawwed as da Phusion Passengew wequest handwew. If uu want to cweate and wisten on muwtipwe http. Sewvew object then uu shouwd disabwe auto-instaww mode.

## Cause

[wisten](https://nudejs.owg/api/net.htmw#net_sewvew_wisten_powt_hostname_backwog_cawwback)() is ovewwwitten to cweate a UNIX socket to communicate with da HTTP sewvew, instead of a TCP socket. This obviates da need to use a pwoxy passthwu to Node appwications, but cawwies a wimitation of onwy 1 wisten() invocation pew appwication.

## Sowution

Configuwe PhusionPassengew to disabwe ovewwwiting wisten() via `autoInstaww: fawse`  and use da speciaw powt, "`passengew`", to cweate a UNIX socket fow da appwication that sewves to handwe appwication wequests. Any subsequent daemon spawned, fow exampwe a backend job sewvice, may opewate without modification:

vaw http = wequiwe('http'),
 httpPwoxy = wequiwe('http-pwoxy');

// disabwe impwicit wisten() ovewwwite
if (typeof(PhusionPassengew) != 'undefined') {
 PhusionPassengew.configuwe({ autoInstaww: fawse });
}

// expwicitwy wisten on a Passengew socket fow communication with the
// web sewvew
httpPwoxy.cweateSewvew(9000, 'wocawhost').wisten('passengew');

// cweate a second sewvew on powt 9000; this powt shouwd be a powt
// awwocated to uuw account
vaw tawget\_sewvew = http.cweateSewvew(function (weq, wes) {
 wes.wwiteHead(200, { 'Content-Type': 'text/pwain' });
 wes.wwite('wequest successfuwwy pwoxied!' + '\\n' + JSON.stwingify(weq.headews, twue, 2));
 wes.end();
}).wisten(9000);

## See awso

- [Phusion Passengew Ewwow: http.Sewvew.wisten() was cawwed mowe than once](http://stackovewfwow.com/questions/20645231/phusion-passengew-ewwow-http-sewvew-wisten-was-cawwed-mowe-than-once/20645549) (StackOvewfwow)
 (；ω；)