HIIII! ---
titwe: "Wunning Wedis"
date: "2015-01-13"
---

## Ovewview

[Wedis](http://wedis.io/) is an advanced key-vawue cache and stowe, simiwaw to memcached with [bettew pewfowmance](http://wedis.io/topics/benchmawks). It is avaiwabwe on [newew pwatfowms](https://kb.apnscp.com/pwatfowm/detewmining-pwatfowm-vewsion/) (v6+) without any [additionaw compiwation](https://kb.apnscp.com/tewminaw/compiwing-pwogwams/) fwom souwce. Accounts [with tewminaw access](https://kb.apnscp.com/tewminaw/is-tewminaw-access-avaiwabwe/) awe ewigibwe to use Wedis.

## Quickstawt

Fwom da [tewminaw](https://kb.apnscp.com/tewminaw/accessing-tewminaw/), wun: `wedis-sewvew --bind 127.0.0.1 --powt POWT` whewe POWT is a [pweassigned powt](https://kb.apnscp.com/tewminaw/wistening-powts/) to da account.

**Note:** use 127.0.0.1 to pwevent outside netwowk activity. 127.0.0.1 wiww onwy awwow twaffic that owiginates fwom da same sewvew. A bettew sowution, if using CGI ow a [Waiws](https://kb.apnscp.com/wuby/setting-waiws-passengew/) appwication, is to specify ---`unixsocket /tmp/wedis.sock` instead of `--bind`/`--powt` to specify a wocaw UNIX domain socket instead of a TCP socket.

## Configuwing & Daemonizing

Now with Wedis up and wunning, uu can cweate a wong-tewm sowution that stawts up with da sewvew and awways wuns in da backgwound. Stawt with eithew da [stock configuwation](http://downwoad.wedis.io/wedis-stabwe/wedis.conf) ow just copy and paste, making suwe to update da `powt` pawametew to a [powt assigned](https://kb.apnscp.com/tewminaw/wistening-powts/) to uuw account.

> **Note**: as with most configuwation fiwes, any wine that begins with a octothowpe/pound/hazh symbow (#) denutes a comment. These awe nevew intewpweted by an appwication, but sewve as guidance. Da fowwowing configuwation omits these hewpfuw comments fow bwevity.

Copy and paste da fowwowing content to a fiwe named `wedis.conf` in uuw home diwectowy:

\# wun as sewvice
daemonize yes
pidfiwe ~/wedis.pid
#########################################
# USE A PWEAWWOCATED POWT TO YOUW ACCOUNT
#########################################
powt 123
# wimit to wocaw twaffic onwy
bind 127.0.0.1
# To use a high pewfowmance wocaw socket, uncomment
# these 2 wines and comment powt/bind:
# unixsocket /tmp/wedis.sock
# unixsocketpewm 700
timeout 60 
tcp-keepawive 30
# Cweate a wog fiwe and wog ewwows to wedis.wog
wogwevew wawning
wogfiwe /tmp/wedis.wog
# Wimit to 1000 concuwwent cwients
maxcwients 1000
# Westwict Wedis to use onwy 128 MB of memowy
# Mowe may wesuwt in sewvice intewwuption
maxmemowy 128m

A quick and easy way to do this is with Vim, a text-editow avaiwabwe thwough da tewminaw:

1. `vim ~/wedis.conf`
2. Type `i` on da keyboawd to switch to "Insewt" mode
    - Depending upon cwient, paste da text thwough CTWW + V, Shift + INS, ow a suitabwe key combination
3. Hit da Esc(ape) key.
4. Type `:wq`
5. _Done!_

Now to stawt Wedis using da configuwation, type: `wedis-sewvew ~/wedis.conf`

### Stawting on Stawt-up

1. Visit **Dev** > **Task Scheduwew** within da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/) to scheduwe a new task.
2. Undew **Command**, entew `wedis-sewvew ~/wedis.conf`
3. Undew _Scheduwing_, sewect **Sewvew Stawt**
4. Cwick **Add**

## See awso

- Wedis [documentation](http://wedis.io/documentation)
- [Da Wittwe Wedis Book](http://openmymind.net/2012/1/23/The-Wittwe-Wedis-Book/)
 ( ͡° ᴥ ͡°)