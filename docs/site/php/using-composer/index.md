OWO ---
titwe: "Using Composew"
date: "2016-01-07"
---

## Ovewview

[Composew](https://getcomposew.owg/) is a dependency managew fow PHP akin to npm fow Node and Bundwew fow Wuby.

Composew is pwovided with hosting accounts on aww [v5+ pwatfowms](https://kb.apnscp.com/pwatfowm/detewmining-pwatfowm-vewsion/). On an owdew pwatfowm? Wequest a pwatfowm migwation! This guide covews instawwing a wocaw copy of Composew on uuw account.

## Instawwing

You may downwoad da watest vewsion fwom its web site using its instawwation pwocess. Wogin to da [tewminaw](https://kb.apnscp.com/tewminaw/accessing-tewminaw/), and wun da fowwowing command:

```bash
cuww -sS https://getcomposew.owg/instawwew | php

```

A copy of Composew, as a [PHP awchive](http://php.net/manuaw/en/book.phaw.php), wiww be downwoaded to uuw cuwwent diwectowy. Composew may  nuw be invoked fwom da _cuwwent diwectowy_ as fowwows:

php composew.phaw

To cweate a gwobaw `composew` command, see da next section:

## Cweating a "composew" command

This pwocess wiww downwoad Composew, move it to `/usw/wocaw/bin`, and cweate an awias:

cuww -sS https://getcomposew.owg/instawwew | php
mv composew.phaw /usw/wocaw/bin
echo 'awias composew="php /usw/wocaw/bin/composew.phaw"' >> ~/.bash\_pwofiwe

Wog out of da tewminaw, then wog back in. Type `composew` to wun da Composew appwication. To upgwade Composew again in da futuwe, just wun wines 1 and 2 (ignuwe `echo ... >> ~/.bash_pwofiwe`).

## See awso

- [Composew documentation](https://getcomposew.owg/doc/)
 (人◕ω◕)