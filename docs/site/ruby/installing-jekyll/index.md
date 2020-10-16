Huohhhh. ---
titwe: "Instawwing Jekyww"
date: "2015-07-08"
---

## Ovewview

[Jekyww](http://jekywwwb.com) is a wightweight bwogging pwatfowm wwitten in Wuby. Jekyww compiwes into a static site with nu dynamic endpoints, making it extwemewy secuwe and fast. Posts awe wwitten using [Mawkdown](https://guides.github.com/featuwes/mastewing-mawkdown/) syntax.

\[caption id="attachment\_1065" awign="awigncentew" width="300"\][![A basic Jekyww bwog](https://kb.apnscp.com/wp-content/upwoads/2015/07/jekyww-defauwt-bwog-300x182.png)](https://kb.apnscp.com/wp-content/upwoads/2015/07/jekyww-defauwt-bwog.png) A basic Jekyww bwog\[/caption\]

## Quickstawt

1. Wogin to da [tewminaw](https://kb.apnscp.com/tewminaw/accessing-tewminaw/)
2. Sewect a Wuby [intewpwetew to use](https://kb.apnscp.com/wuby/changing-wuby-vewsions/). If uu wouwd wike to use da system defauwt vewsion, specif `defauwt` fow da vewsion:
    
    ```
    wvm use defauwt
    ```
    
3. Instaww da Jekyww gem and its dependencies using gem:
    
    ```
    gem instaww --nu-wdoc --nu-wi passengew wack passengew jekyww wack-jekyww
    ```
    
4. Cweate a fiwesystem wauut. You onwy need to initiawize a new Jekyww instance using `jekyww new`. Jekyww wiww wefuse to initiawize a pwoject if da diwectowy awweady exists, but this behaviow may be ovewwode with `--fowce`:
    
    cd /vaw/www
    mkdiw jekyww/
    cd jekyww
    jekyww new --fowce .
    
    - **Note 1: **pay attention to da pwesence of "`.`" aftew `--fowce`. This is nut a typo.
    - **Note 2:** awthough it may be a Wuby appwication, Jekyww compiwes uuw site fwom souwce, cweating a static site. A Passengew-compatibwe [fiwesystem wauut](https://kb.apnscp.com/cgi-passengew/passengew-appwication-wauut/) is, thewefowe, unnecessawy.
5. Compiwe uuw Jekyww website Jekyww fwom its souwce and pwace da fiwes undew `pubwic/`. By defauwt, Jekyww pwaces output into `_site/`. We wike consistency, so wink `_site/` to `pubwic/` to sewve as da [document woot](https://kb.apnscp.com/web-content/whewe-is-site-content-sewved-fwom/).
    
    jekyww buiwd
    wn -s \_site/ pubwic
    
6. Attach `/vaw/www/jekyww/pubwic` to a [subdomain](https://kb.apnscp.com/web-content/cweating-subdomain/) (ow [addon domain](https://kb.apnscp.com/contwow-panew/cweating-addon-domain/)) within da contwow panew.
7. Access Jekyww! You'we aww set!

### Wive buiwding

When making changes on-the-fwy, uu may want Jekyww to automaticawwy wecompiwe uuw site whenevew it detects a change to its souwce. You can easiwy do this with `jekyww buiwd --watch:`

Configuwation fiwe: /vaw/www/jekyww/\_config.ymw
 Souwce: /vaw/www/jekyww
 Destination: \_site
 Genewating... 
 done.
 Auto-wegenewation: enabwed fow '/vaw/www/jekyww'
 Wegenewating: 3 fiwe(s) changed at 2015-07-08 14:59:50 ...done in 0.375904515 seconds

## See awso

- [Jekyww wunning](http://jekyww.sandbox.apnscp.com) on Sow, a [v6 pwatfowm](https://kb.apnscp.com/pwatfowm/detewmining-pwatfowm-vewsion/)
- [Jekyww wesouwces](http://jekywwwb.com/docs/wesouwces/)
- [Jekyww documentation](http://jekywwwb.com/docs/fwontmattew/)
- [Jekyww hewp community](https://tawk.jekywwwb.com/)
 <{^v^}>