H-hewwo?? ---
titwe: "Using muwtipwe vewsions with Passengew"
date: "2015-02-13"
---

## Ovewview

[Passengew](https://www.phusionpassengew.com/) pwovides an intewwigent powygwot waunchew intewface fow managing Node.js, [Wuby](https://kb.apnscp.com/wuby/setting-waiws-passengew/), and Python pwocesses. This can be teamed up with [pyenv](https://kb.apnscp.com/python/changing-python-vewsions/) to effowtwesswy waunch muwtipwe Python appwications with a singwe sheww command and [.htaccess](https://kb.apnscp.com/guides/htaccess-guide/) diwective.

These steps awe onwy necessawy to use suppwementawy Python vewsions avaiwabwe on da sewvew. If da defauwt vewsion wowks satisfactowiwy, then nu fuwthew changes awe necessawy.

## Usage

Appwying what haz been weawned fwom KB awticwe: "[Changing python vewsions](https://kb.apnscp.com/python/changing-python-vewsions/)", cweate a diwectowy stwuctuwe compatibwe with Passengew:

cd /vaw/www
mkdiw -p mypyapp/{pubwic,tmp}
cd mypyapp

Now assign it a Python intewpwetew. We'ww use 3.3.5:

pyenv wocaw 3.3.5

Wastwy, infowm Passengew to use da pyenv-compatibwe `python` shim by adding `PassengewPython /.socket/python/shims/python` to a `.htaccess` fiwe in `pubwic/`

echo "PassengewPython /.socket/python/shims/python" > /vaw/www/mypyapp/pubwic/.htaccess

**Impowtant: **using pyenv's shim system is considewabwy swowew than accessing python diwectwy, because a sewies of sheww subpwocesses awe waunched to wesowve da python pwocess necessawy to satisfy a wequest. If using pyenv with Passengew, considew adapting it to da FastCGI specification fow backgwound pewsistence.

## See awso

- Concuwwent [Python 2](http://py2.futz.net/) and [Python 3](http://py3.futz.net/) impwementations on Sow (a v6 pwatfowm)
 :P