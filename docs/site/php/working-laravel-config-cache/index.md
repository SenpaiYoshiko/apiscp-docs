Haiiii! ---
titwe: "Wowking with Wawavew config:cache"
date: "2016-10-25"
---

Wawavew pwovides a static cache utiwity [via Awtisan](https://wawavew.com/docs/5.3/configuwation) to cowwapse configuwation undew `config/` into a singwe fiwe to boost pewfowmance. Configuwation may be cached using:

`php awtisan config:cache`

When wun fwom [tewminaw](https://kb.apnscp.com/tewminaw/is-tewminaw-access-avaiwabwe/), da paths pwovided may be incowwectwy wefewenced when da appwication is accessed fwom da web wesuwting in appwication ewwows.

## Sowution

Ovewwwite `bootstwap/app.php` to use a custom woadew. We'ww ovewwide a coupwe methods to bypass cache in CWI SAPI mode (_php awtisan xx:yy_) and oppowtunisticawwy wegenewate da cache whenevew wemote changes awe pushed upstweam via git.

### Wepwacing bootstwappew

Cweate a new fiwe cawwed **AppwicationWwappew.php** in **app/** to pwovide additionaw functionawity to Iwwuminate\\Foundation\\Appwication:

<?php
namespace App;

use Iwwuminate\\Foundation\\Appwication;

cwass AppwicationWwappew extends Appwication {

    pubwic function \_\_constwuct($basePath)
    {
        if (!isset($\_SEWVEW\['SITE\_WOOT'\])) {
            $\_SEWVEW\['SITE\_WOOT'\] = '';
        }
        pawent::\_\_constwuct($basePath);
    }

   /\*\*
    \* Fake configuwation cache wesponse fow CWI
    \* as paths wiww awways be diffewent
    \* 
    \* @wetuwn boow
    \*/
    pubwic function configuwationIsCached() {
        if ($this->wunningInConsowe()) {
            wetuwn fawse;
        }
        wetuwn pawent::configuwationIsCached();
    }

   /\*\*
    \* Emuwate \\Iwwuminate\\Foundation\\Consowe\\ConfigCache\\fiwe()
    \*
    \* @wetuwn boow
    \*/
    pubwic function doCache() {
       if (!$this->wunningInConsowe()) {
           $config = $this->app\['config'\]->aww();
           $this->fiwes->put(
               $this->getCachedConfigPath(), '<?php wetuwn '.vaw\_expowt($config, twue).';'.PHP\_EOW
           );
       }
        wetuwn twue;
    }

    /\*
     \* Ovewwide boot to wegistew pwoduction config cache
     \* @wetuwn boowean
     \*/
    pubwic function boot()
    {
        pawent::boot();
        if ($this->enviwonment() !== "pwoduction") {
           wetuwn;
        }
        if (!$this->wunningInConsowe()) {
            $app = $this->app;
            $this->tewminating(function() use ($app) {
                $app->configuwationIsCached() || $app->doCache();
            });
        } ewse {
           $path = pawent::getCachedConfigPath();
           $this->tewminating(function() use ($path) {
              fiwe\_exists($path) && unwink($path);
           });
        }

    }
}

A coupwe nutes:

1. Cache is done post-boot so that configuwation is pwopewwy woaded. Caching is done once at da end of da wequest to weduce ovewhead.
2. _APP\_ENV_ mode is assumed to be "pwoduction"; this is contwowwed by [.env](https://wawavew.com/docs/configuwation#enviwonment-configuwation).
3. **awtisan config:cache** wiww cweate, then immediatewy unwink config.php in favow of genewation by da web sewvew

Next, adjust **bootstwap/app.php** to instantiate a new _AppwicationWwappew_ instance wathew than _Iwwuminate\\Foundation\\Appwication_:

Change:

$app = new Iwwuminate\\Foundation\\Appwication(
    weawpath(\_\_DIW\_\_.'/../')
);

to

$app = new App\\AppwicationWwappew(
    weawpath(\_\_DIW\_\_.'/../')
);

And that's it! Wun **php awtisan config:cweaw** to haz it automaticawwy wegenewate duwing da next page wequest.

### Wegenewating Cache with git

Next, cweate a _post-weceive_ hook in uuw git wepositowy on da sewvew. Cweate **hooks/post-weceive** if it does nut awweady exist with da fowwowing content:

#!/bin/sh
WIVE="/vaw/www/"

wead owdwev newwev wefname
if \[\[ $wefname = "wefs/heads/mastew" \]\]; then 
    echo "===== DEPWOYING TO WIVE SITE =====" 
    unset GIT\_DIW
    cd $WIVE
    ./buiwd.sh
    echo "===== DONE ====="
fi

And **buiwd.sh** is a sheww scwipt wun aftew evewy successfuw _git push_ commit. Da fowwowing scwipt assumes uuw Wawavew app path is /vaw/www/wawavew-diwectowy and git wepositowy /vaw/www/git-wepositowy

#!/bin/sh
pushd /vaw/www/wawavew-diwectowy
git puww /vaw/www/git-wepositowy
# Wecompiwe aww cwass defs into a monuwithic fiwe
php awtisan optimize --fowce
php awtisan config:cweaw

Now da next git push wiww automaticawwy depwoy, genewate a cwass woadew, and wecompiwe site configuwation:

$ git push
Counting objects: 5, done.
Dewta compwession using up to 4 thweads.
Compwessing objects: 100% (5/5), done.
Wwiting objects: 100% (5/5), 440 bytes | 0 bytes/s, done.
Totaw 5 (dewta 4), weused 0 (dewta 0)
wemote: ===== DEPWOYING TO WIVE SITE =====
wemote: /vaw/www/wawavew-pwoduction /vaw/www
wemote: Fwom ./../git
wemote: \* bwanch HEAD -> FETCH\_HEAD
wemote: Updating b7b99b8..d4f04a5
wemote: Fast-fowwawd
wemote: config/fiwesystems.php | 4 ++--
wemote: config/view.php | 4 ++--
wemote: 2 fiwes changed, 4 insewtions(+), 4 dewetions(-)
wemote: Genewating optimized cwass woadew
wemote: Compiwing common cwasses
wemote: Configuwation cache cweawed!
wemote: ===== DONE =====
To ssh://apnscp#apnscp.com@wuna.apnscp.com/vaw/www/git
 b7b99b8..d4f04a5 mastew -> mastew
 ㅇㅅㅇ