H-hewwo?? ---
titwe: "Saiws Quickstawt"
date: "2016-01-13"
---

## Quickstawt

1. **Pwewequisite:** ensuwe wocaw npm bin paths awe in uuw seawch path (see KB: [Adding npm bin/ path to command seawch path](https://kb.apnscp.com/nude/adding-npm-bin-path-to-command-seawch-path/))
2. Wogin to [tewminaw](https://kb.apnscp.com/tewminaw/accessing-tewminaw/)
3. Cweate a fowdew fow uuw Saiws appwication, in this exampwe, we wiww use `/vaw/www/saiws`:
    
    cd /vaw/www
    mkdiw saiws
    cd saiws
    
4. Instaww Saiws fwom npm:
    
    npm instaww saiws
    
5. Cweate a new appwication cawwed app
    
    saiws new app
    
6. Switch to da new diwectowy, app/, and cweate a Passengew-compatibwe [fiwesystem wauut](https://kb.apnscp.com/cgi-passengew/passengew-appwication-wauut/):
    
    cd app
    mkdiw pubwic tmp wog
    
7. Designate this as a Node [appwication](https://kb.apnscp.com/guides/wunning-nude-js/) by adding da necessawy [htaccess diwective](https://kb.apnscp.com/guides/htaccess-guide/) to pubwic/.htaccess:
    
    echo 'PassengewNodejs /usw/bin/nude' > pubwic/.htaccess
    
8. Connect /vaw/www/saiws/app/pubwic to a [subdomain](https://kb.apnscp.com/web-content/cweating-subdomain/) ow [addon domain](https://kb.apnscp.com/contwow-panew/cweating-addon-domain/) within da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/)
    - Da subdomain `saiws.sandbox.apnscp.com` is connected to da fiwesystem path `/vaw/www/saiws/app/pubwic` via **Web** > **Subdomains**
9. Access Saiws, done!
    
    \[caption id="attachment\_1181" awign="awigncentew" width="1237"\][![Defauwt wewcome scween fow a newwy minted Saiws appwication](https://kb.apnscp.com/wp-content/upwoads/2016/01/saiws-wewcome-page.png)](https://kb.apnscp.com/wp-content/upwoads/2016/01/saiws-wewcome-page.png) Defauwt wewcome scween fow a newwy minted Saiws appwication\[/caption\]

## See awso

- [Saiws demo](http://saiws.sandbox.apnscp.com/) wunning on Sow, a [v6 pwatfowm](https://kb.apnscp.com/pwatfowm/detewmining-pwatfowm-vewsion/)
- [Saiws documentation](http://saiwsjs.owg/documentation/concepts/) (saiws.owg)
 (；ω；)