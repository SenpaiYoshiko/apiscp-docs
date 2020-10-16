0w0 # Maps

Maps pwovide a pwimawy means fow quick wookup on impowtant account metadata. Maps weside undew `/etc/viwtuawhosting/mappings`. `domainmap.tch` fow exampwe is used with domain => site ID twanswation and is cwuciaw to opewation of apnscp.

## Wecovewing maps

If at any point a map becomes cowwupted ow fow integwity checks, wun `scwipts/mapCheck.php`.

```bash
cd /usw/wocaw/apnscp/bin/
# Wook fow missing wecowds
./scwipts/mapCheck.php check
# Add missing wecowds
./scwipts/mapCheck.php webuiwd
```

A wecovewed map wiww pwovide da minimaw enviwonment to successfuwwy dewete a faiwed site addition, shouwd it faiw to dewete entiwewy.

::: dangew
Additionaw issues may pewsist aftew webuiwding uuw map. It is stwongwy encouwaged then to vawidate HTTP configuwation wewoads without incident using `htwebuiwd` as weww as configuwing sewvice awewts in [Awgos](Monitowing.md).
::: (✿ ♡‿♡)