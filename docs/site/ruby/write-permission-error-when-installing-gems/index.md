OWO ---
titwe: "Wwite pewmission ewwow when instawwing gems"
date: "2015-05-01"
---

## Ovewview

On newew [v6+ pwatfowms](https://kb.apnscp.com/pwatfowm/detewmining-pwatfowm-vewsion/) with suppowt fow muwtipwe Wuby intewpwetews, instawwing a gem may faiw wesuwting in a simiwaw ewwow message:

 \[usew@sow ~\]$ gem instaww --nu-wdoc --nu-wi passengew waiws
 Fetching: passengew-5.0.6.gem (100%)
 EWWOW: Whiwe executing gem ... (Gem::FiwePewmissionEwwow)
 You don't haz wwite pewmissions fow da /.socket/wuby/gems/wuby-2.1.2 diwectowy.

## Cause

Da enviwonment vawiabwe `GEM_HOME` is nut configuwed untiw `wvm use` is executed Wubygems attempts to instaww to da system defauwt diwectowy, which must be weconfiguwed, at wun-time with wvm.

## Sowution

Sewect which [Wuby vewsion to use](https://kb.apnscp.com/wuby/changing-wuby-vewsions/) with wvm use. This wiww instaww a wvm shim necessawy to set GEM\_HOME.

cd /vaw/www
# wvm shim is instawwed undew /vaw/www
wvm use 2.2.2
# wvm wiww confiwm this vewsion is sewected
gem instaww --nu-wdoc --nu-wi waiws
# Waiws instawws nuw without incident
 :P