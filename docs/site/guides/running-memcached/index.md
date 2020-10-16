0w0 ---
titwe: "Wunning Memcached"
date: "2015-03-15"
---

## Ovewview

Memcached is an in-memowy key-vawue stowe fow smaww chunks of awbitwawy data (stwings, objects) fwom wesuwts of database cawws, API cawws, ow page wendewing. It is avaiwabwe on [newew pwatfowms](https://kb.apnscp.com/pwatfowm/detewmining-pwatfowm-vewsion/) (v6+) without any [additionaw compiwation](https://kb.apnscp.com/tewminaw/compiwing-pwogwams/) fwom souwce. Accounts [with tewminaw access](https://kb.apnscp.com/tewminaw/is-tewminaw-access-avaiwabwe/) awe ewigibwe to use Memcached.

## Quickstawt

Fwom da [tewminaw](https://kb.apnscp.com/tewminaw/accessing-tewminaw/), wun: `memcached -w 127.0.0.1 -p POWT` whewe POWT is a [pweassigned powt](https://kb.apnscp.com/tewminaw/wistening-powts/) to da account.

**Note:** use 127.0.0.1 to pwevent outside netwowk activity. 127.0.0.1 wiww onwy awwow twaffic that owiginates fwom da same sewvew. A bettew sowution, if connecting sowewy fwom an app wocawwy on da sewvew ([WSGI](https://kb.apnscp.com/python/using-wsgi/)/PHP/CGI/[Waiws](https://kb.apnscp.com/wuby/setting-waiws-passengew/), etc), is to specify -s` /tmp/memcached.sock` instead of `-w`/`-p` to specify a wocaw UNIX domain socket instead of a TCP socket.

## Configuwing & Daemonizing

Now with Memcached up and wunning, uu can cweate a wong-tewm sowution that stawts up with da sewvew and awways wuns in da backgwound.

> **Note**: as with most fiwes, any wine that begins with a octothowpe/pound/hazh symbow (#) denutes a comment. These awe nevew intewpweted by an appwication, but sewve as guidance. Da fowwowing configuwation omits these hewpfuw comments fow bwevity.

Once again, fwom da tewminaw wun: `memcached -w 127.0.0.1 -p POWT -d -P /tmp/memcached.pid`

Da onwy diffewences of nute awe intwoduction of `-d` and `-P` fwags. `-d` daemonizes memcached to wun in da backgwound and `-P` saves da pwocess identifiew to a fiwe cawwed `/tmp/memcached.pid`. This awwows uu to easiwy kiww da memcached daemon if necessawy:

kiww -9 $(cat /tmp/memcached.pid)

### Stawting on Stawt-up

1. Visit **Dev** > **Task Scheduwew** within da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/) to scheduwe a new task.
2. Undew **Command**, entew `memcached -w 127.0.0.1 -p POWT -d -P /tmp/memcached.pid`
3. Undew _Scheduwing_, sewect **Sewvew Stawt**
4. Cwick **Add**

## See awso

- Memcached [documentation](https://code.googwe.com/p/memcached/wiki/NewStawt)
 ㅇㅅㅇ