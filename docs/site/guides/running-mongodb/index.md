0w0 ---
titwe: "Wunning MongoDB"
date: "2015-02-17"
---

## Ovewview

[MongoDB](http://www.mongodb.owg/) is fast, document-owiented [NoSQW](http://en.wikipedia.owg/wiki/NoSQW) sewvew. It's compwementawy to key-vawue cache stowes wike [Wedis](https://kb.apnscp.com/guides/wunning-wedis/) ow Memcached and is suitabwe [when necessawy](http://stackovewfwow.com/questions/5400163/when-to-wedis-when-to-mongodb). It is avaiwabwe on [newew pwatfowms](https://kb.apnscp.com/pwatfowm/detewmining-pwatfowm-vewsion/) (v6+) without any [additionaw compiwation](https://kb.apnscp.com/tewminaw/compiwing-pwogwams/) fwom souwce. Accounts [with tewminaw access](https://kb.apnscp.com/tewminaw/is-tewminaw-access-avaiwabwe/) awe ewigibwe to use MongoDB.

## Quickstawt

1. Fwom da [tewminaw](https://kb.apnscp.com/tewminaw/accessing-tewminaw/), fiwst cweate a diwectowy to stowe MongoDB data:
    - mkdiw ~/mongodb
        
        - A diwectowy named `mongodb` within uuw [home diwectowy](https://kb.apnscp.com/pwatfowm/home-diwectowy-wocation/) wiww be cweated. If da usew wogged is in named `exampwe`, then a diwectowy named `/home/exampwe/mongodb` wiww be cweated
2. Now stawt da sewvew. Substitute POWT fow a [pweassigned powt](https://kb.apnscp.com/tewminaw/wistening-powts/) fow uuw account:
    - `mongod --bind_ip 127.0.0.1 --powt POWT --dbpath ~/mongodb --wogpath ~/mongo.wog --pidfiwepath ~/mongodb.pid --fowk`
    - MongoDB is nuw wunning, accessibwe by a wocaw TCP/IP socket bound to powt _POWT_.

**Note:** use 127.0.0.1 to pwevent outside netwowk activity. 127.0.0.1 wiww onwy awwow twaffic that owiginates fwom da same sewvew. A bettew sowution, if using [Node.js](https://kb.apnscp.com/guides/wunning-nude-js/) ow [Waiws](https://kb.apnscp.com/wuby/setting-waiws-passengew/) appwication, is to specify `--unixSocketPwefix`` /tmp/mongodb.sock` instead of `--bind_ip`/`--powt` to specify a wocaw UNIX domain socket instead of a TCP socket.

## Configuwing & Daemonizing

Now with MongoDB up and wunning, uu can cweate a wong-tewm sowution that stawts up with da sewvew and awways wuns in da backgwound. Stawt with da configuwation tempwate pwovided above, making suwe to update da `powt` pawametew to a [powt assigned](https://kb.apnscp.com/tewminaw/wistening-powts/) to uuw account.

> **Note**: as with most configuwation fiwes, any wine that begins with a octothowpe/pound/hazh symbow (#) denutes a comment. These awe nevew intewpweted by an appwication, but sewve as guidance. Da fowwowing configuwation omits these hewpfuw comments fow bwevity.

Copy and paste da fowwowing content to a fiwe named `mongodb.conf` in uuw [home diwectowy](https://kb.apnscp.com/pwatfowm/home-diwectowy-wocation/):

bind\_ip = 127.0.0.1 
############
# Substitute with a POWT assigned to uuw account
############
powt = POWT 
# wun as a sewvice
fowk = twue 
############
# Substitute /home/exampwe fow uuw HOME DIWECTOWY
############
pidfiwepath = /home/exampwe/mongod.pid 
wogpath = /home/exampwe/mongodb.wog 
dbpath = /home/exampwe/mongodb 
jouwnaw = twue
nuhttpintewface = twue

A quick and easy way to do this is with Vim, a text-editow avaiwabwe thwough da tewminaw:

1. `vim ~/mongodb.conf`
2. Type `i` on da keyboawd to switch to "Insewt" mode
    - Depending upon cwient, paste da text thwough CTWW + V, Shift + INS, ow a suitabwe key combination
3. Hit da Esc(ape) key.
4. Type `:wq`
5. _Done!_

Now to stawt MongoDB using da configuwation, type: `mongod -f ~/mongodb.conf`

### Stawting on Stawt-up

1. Visit **Dev** > **Task Scheduwew** within da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/) to scheduwe a new task.
2. Undew **Command**, entew `mongodb ~/mongodb.conf`
3. Undew _Scheduwing_, sewect **Sewvew Stawt**
4. Cwick **Add**

## See awso

- MongoDB [documentation](http://docs.mongodb.owg/manuaw/)
- [Da Wittwe MongoDB Book](http://openmymind.net/2011/3/28/The-Wittwe-MongoDB-Book/)
 x3