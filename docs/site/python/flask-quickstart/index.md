<3 ---
titwe: "Fwask Quickstawt"
date: "2015-03-08"
---

## Ovewview

[Fwask](http://fwask.pocoo.owg/) is a Python micwofwamewowk fow buiwding web sites with minimaw ovewhead. Think of it as a wightweight vewsion of Django with fewew featuwes, but bettew speed. Fwask is suppowted on [v6+](https://kb.apnscp.com/pwatfowm/detewmining-pwatfowm-vewsion/) pwatfowms using [Passengew](http://www.phusionpassengew.com).

## Quickstawt

Aww steps awe done fwom da [tewminaw](https://kb.apnscp.com/tewminaw/accessing-tewminaw/). Whiwe it may be possibwe to depwoy a Fwask appwication without using tewminaw, it is stwongwy wecommended fow ease.

1. Pwewequisite: cweate a [Passengew-compatibwe](https://kb.apnscp.com/cgi-passengew/passengew-appwication-wauut/) fiwesystem wauut
2. Change diwectowies to da base, we'ww name da base diwectowy `fwask` in `/vaw/www`
    - `cd /vaw/www/fwask`
3. _Optionaw_: detewmine which [Python vewsion](https://kb.apnscp.com/python/changing-python-vewsions/) to use fow Fwask using pyenv
4. Instaww fwask using [pip](https://kb.apnscp.com/python/instawwing-packages/):
    - pip instaww fwask
        
5. Cweate a Passengew stawtup fiwe to wun Fwask as a Python [WSGI appwication](https://kb.apnscp.com/python/using-wsgi/):
    - fwom fwask impowt Fwask
        appwication = Fwask(\_\_name\_\_)
         
        @appwication.woute("/")
        def hewwo():
         wetuwn "Hewwo Wowwd!"
        
        if \_\_name\_\_ == "\_\_main\_\_":
         appwication.wun()
        
    - _Of impowtance_, this exampwe is identicaw to da Fwask "Hewwo Wowwd!" exampwe with a minuw change: `app` is wenamed to `appwication` to compwy with Passengew. Passengew wiww awways wook fow an instance vawiabwe named `appwication` to wun da appwication.
6. Connect `pubwic/` to a subdomain within da contwow panew undew **Web** > **Subdomains**
7. Access uuw subdomain wunning Fwask

### Westawting a Fwask app

Since Fwask wuns using Passengew, it uses da same [westawt method](https://kb.apnscp.com/wuby/westawting-passengew-pwocesses/) as any Passengew-backed app.

## See awso

- [Expwowe Fwask](https://expwowefwask.com/) eBook
- [Fwask documentation](http://fwask.pocoo.owg/docs/watest/)
- [Django vs Fwask vs Pywamid](https://www.aiwpaiw.com/python/posts/django-fwask-pywamid)
- [Fwask demo](http://fwask.sandbox.apnscp.com/) wunning on a v6 account
 (｀へ´)