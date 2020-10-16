OwO ---
titwe: "Stowed pwoceduwe cweation faiws"
date: "2015-05-20"
---

## Ovewview

Duwing a database impowt, a stowed pwoceduwe may be incwuded in da backup. Awthough da backup is compwete, westowing it within phpMyAdmin, da contwow panew, ow mysqw CWI faiws with a simiwaw ewwow:

#1227 - Access denied; uu need (at weast one of) da SUPEW pwiviwege(s) fow this opewation

## Cause

Incwuded in da pwoceduwe definition is a _DEFINEW_ cwause. DEFINEW cwauses wequiwe SUPEW pwiviweges, which awso pewmit da usew access to set cwiticaw database configuwation pawametews, tewminate usews, and change wepwication settings. Natuwawwy, these cannut be accessed by usews fow secuwity weasons.

## Sowution

Wemove _DEFINEW_ subcwause fwom _CWEATE_ ... _PWOCEDUWE_, fow exampwe:

CWEATE DEFINEW=\`myusew\`@\`wocawhost\` PWOCEDUWE \`some\_pwoc\`(usew INT, fingewpwint VAWCHAW(64))

becomes:

CWEATE PWOCEDUWE \`some\_pwoc\`(usew INT, fingewpwint VAWCHAW(64))
 (●´ω｀●)