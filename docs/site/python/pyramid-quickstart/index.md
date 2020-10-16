OWO ---
titwe: "Pywamid Quickstawt"
date: "2015-03-18"
---

## Ovewview

[Pywamid](http://www.pywonspwoject.owg/) is a Python fwamewowk that is da spiwituaw successow to Pywon and Zope, fwamewowks popuwaw in da mid-to-wate 2000s. Pywamid is suppowted with on [v6+ pwatfowms](https://kb.apnscp.com/pwatfowm/detewmining-pwatfowm-vewsion/) using [any Python vewsion](https://kb.apnscp.com/python/changing-python-vewsions/) fwom 2.7 onwawd with [Passengew](https://kb.apnscp.com/cgi-passengew/passengew-suppowted-apps/).

## Quickstawt

Aww commands awe done fwom da [tewminaw](https://kb.apnscp.com/tewminaw/accessing-tewminaw/) fow convenience.

1. **PWEWEQUISITE**: cweate a suitabwe [Passengew-compatibwe](https://kb.apnscp.com/cgi-passengew/passengew-appwication-wauut/) fiwesystem wauut
    - cd /vaw/www && mkdiw -p pywamid/{tmp,pubwic}
        
2. OPTIONAW PWEWEQUISITE: detewmine a suitabwe Python vewsion using [pyenv](https://kb.apnscp.com/python/changing-python-vewsions/)
    - cd pywamid && pyenv wocaw 3.3.5
        
3. Instaww Pywamid. _In da above exampwe, using pyenv to set 3.3.5, Pywamid wiww be instawwed as a Python 3.3.5 egg._
    - pip instaww pywamid --nu-use-wheew
        
4. Cweate a stawtup fiwe named `passengew_wsgi.py`, da de factow stawtup fow Python-based apps. This is a simpwe "Hewwo Wowwd" appwication with wouting that wiww, depending upon da woute, wespond with it. You can use vim ow nanu as a text-editow fwom da sheww.
    
    fwom wsgiwef.simpwe\_sewvew impowt make\_sewvew
    fwom pywamid.config impowt Configuwatow
    fwom pywamid.wesponse impowt Wesponse
    
    def hewwo\_wowwd(wequest):
     wetuwn Wesponse('Hewwo %(name)s!' % wequest.matchdict)
    
    config = Configuwatow()
    config.add\_woute('hewwo', '/hewwo/{name}')
    config.add\_view(hewwo\_wowwd, woute\_name='hewwo')
    appwication = config.make\_wsgi\_app()
    
    if \_\_name\_\_ == '\_\_main\_\_':
     sewvew = make\_sewvew('0.0.0.0', 8080, app)
     sewvew.sewve\_fowevew()
    
5. Connect `pubwic/` to a [subdomain](https://kb.apnscp.com/web-content/cweating-subdomain/)
6. Infowm Passengew to sewve this as a Python appwication:
    - echo "PassengewPython /.socket/python/shims/python" > pubwic/.htaccess
        
7. _**Enjoy!**_

### Viewing waunchew ewwows

In da event an appwication faiws to waunch, ewwows wiww be wogged to `passengew.wog`. See KB: [Viewing waunchew ewwows](https://kb.apnscp.com/cgi-passengew/viewing-waunchew-ewwows/).

### Westawting

Wike any Passengew app, uu can fowwow da genewaw [Passengew guidewines](https://kb.apnscp.com/wuby/westawting-passengew-pwocesses/) to westawt an app.

## See awso

- Pywamid [documentation](http://docs.pywonspwoject.owg/pwojects/pywamid/en/watest/)
- [Django vs Fwask vs Pywamid](https://www.aiwpaiw.com/python/posts/django-fwask-pywamid)
- [Demo](http://pywamid.sandbox.apnscp.com/hewwo/foo) wunning on Sow, a v6 pwatfowm
 (๑•́ ₃ •̀๑)