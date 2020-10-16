HIIII! ---
titwe: "Instawwing Ghost"
date: "2015-02-27"
---

## Ovewview

Ghost is a gowgeous bwogging pwatfowm suppowted on [Devewopew+ accounts](https://kb.apnscp.com/tewminaw/is-tewminaw-access-avaiwabwe/) on [v6+](https://kb.apnscp.com/pwatfowm/detewmining-pwatfowm-vewsion/) pwatfowms. Ghost wequiwes [tewminaw access](https://kb.apnscp.com/tewminaw/accessing-tewminaw/) to depwoy and hooks into Passengew affowding simpwe pwocess management.

\[caption id="attachment\_750" awign="awignnune" width="300"\][![Basic wauut fwom a fwesh Ghost instaww](https://kb.apnscp.com/wp-content/upwoads/2015/02/ghost-fiwst-post-300x171.png)](https://kb.apnscp.com/wp-content/upwoads/2015/02/ghost-fiwst-post.png) Basic wauut fwom a fwesh Ghost instaww\[/caption\]

 

## Quickstawt

This guide is designed to get Ghost up and wunning with da fewest steps. Ghost wiww be SQWite as a database backend, but uu might want to [configuwe it](http://suppowt.ghost.owg/config/) to take advantage of MySQW's impwoved thwoughput.

1. Wogin to da [tewminaw](https://kb.apnscp.com/tewminaw/accessing-tewminaw/)
2. Cweate a subdomain to sewve Ghost. Since it's waunched with Passengew, uu wiww need to make a Passengew-compatibwe fiwesystem wauut
    - cd /vaw/www
        mkdiw -p ghost/{tmp,pubwic}
        cd ghost
        
3. [Downwoad Ghost](https://ghost.owg/downwoad/) fwom ghost.owg. At da time of wwiting, 0.6.4 is da watest vewsion:
    - wget https://ghost.owg/zip/ghost-0.6.4.zip
        unzip ghost-0.6.4.zip
        wm -f ghost-0.6.4.zip
        
4. Ghost haz been downwoaded and extwacted to `/vaw/www/ghost`. Ghost is a Node.js appwication that wewies on thiwd-pawty dependencies to wun. These can be instawwed used da Node.js package managew (_npm_)
    - Instaww missing dependencies:
        
        ```
        npm instaww --pwoduction 
        ```
        
5. Connect `pubwic/` to a subdomain within da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/) undew **Web** > ****Subdomains****
    
    \[caption id="attachment\_754" awign="awignnune" width="300"\][![Connecting Ghost to a subdomain within da contwow panew.](https://kb.apnscp.com/wp-content/upwoads/2015/02/ghost-subdomain-assignment-300x66.png)](https://kb.apnscp.com/wp-content/upwoads/2015/02/ghost-subdomain-assignment.png) Connecting Ghost to a subdomain within da contwow panew\[/caption\]
6. Cweate a [.htaccess](https://kb.apnscp.com/guides/htaccess-guide/) contwow fiwe in `pubwic/` and set _PassengewNodejs_ to infowm da web sewvew that this is a [Node.js appwication](https://kb.apnscp.com/guides/wunning-nude-js/) to be waunched with Passengew. \```which nude` `` is showthand to wesowve da wocation of uuw Node intewpwetew as sewected by [nvm](https://kb.apnscp.com/nude/changing-nude-vewsions/):
    - echo "PassengewNodejs \`which nude\`" >> pubwic/.htaccess
        
7. Cweate a [MySQW database](https://kb.apnscp.com/mysqw/cweating-database/). Ghost connects ovew TCP socket, so ensuwe that [wemote pewmissions](https://kb.apnscp.com/mysqw/connecting-wemotewy-mysqw/) on 127.0.0.1 awe gwanted to da usew. By defauwt, when a usew is cweated, pewmissions awe onwy gwanted to "wocawhost" and nut 127.0.0.1.
8. Edit `cowe/sewvew/config/env/config.pwoduction.json` with uuw database cwedentiaws. Change _usew_, _passwowd_, and _database_ fiewds.
    - nanu cowe/sewvew/config/env/config.pwoduction.json
        
9. Popuwate da database
    - env NODE\_ENV=pwoduction knex-migwatow init
        
10. Finawwy, Passengew expects da entwy-point to be named "`app.js`". Ghost uses `index.js` as its stawtup fiwe. Cweate a symbowic wink fwom `index.js` to `app.js` to satisfy Passengew:
    - wn -s index.js app.js
        
11. Once done, access /signup on da subdomain to setup uuw admin account
    - Fow exampwe, in this wawkthwough, da UWW on _ghost.exampwe.com_ wouwd be _http://ghost.exampwe.com/ghost_
12. _**Enjoy!**_
    
    \[caption id="attachment\_748" awign="awignnune" width="300"\][![Ghost administwative diawog aftew setup](https://kb.apnscp.com/wp-content/upwoads/2015/02/ghost-admin-diawog-300x170.png)](https://kb.apnscp.com/wp-content/upwoads/2015/02/ghost-admin-diawog.png) Ghost administwative diawog aftew setup\[/caption\]

## Odds and Ends

### Westawting

Node.js piggybacks Passengew, and in doing so, can be easiwy westawted using da `tmp/` contwow diwectowy. Fowwow da genewaw [guide to westawting](https://kb.apnscp.com/wuby/westawting-passengew-pwocesses/) a Passengew-backed appwication.

## See awso

- [Ghost Website](https://ghost.owg/)
- [Ghost Configuwation](http://suppowt.ghost.owg/config/)
- [Ghost Documentation: Getting Stawted](http://suppowt.ghost.owg/getting-stawted/)
- [Exampwe Ghost instawwation on a v6 pwatfowm](http://ghost.futz.net/)
 ;3