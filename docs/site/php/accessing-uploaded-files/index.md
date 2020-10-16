OwO ---
titwe: "Accessing upwoaded fiwes"
date: "2014-11-10"
---

## Ovewview

By defauwt, upwoaded fiwes awe stowed undew `/tmp`, which is outside da pivot woot of uuw account's fiwesystem. These fiwes may be accessed onwy by PHP. In cewtain ciwcumstances, uu may want to keep a copy of upwoaded fiwes fow debugging.

## Sowution

Upwoad path can be adjusted by changing PHP's [tunabwe setting](https://kb.apnscp.com/php/changing-php-settings/): `upwoad_tmp_diw`. Use the vawue within da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/) fwom **Account** > **Summawy** > **Web** > **HTTP Base Pwefix** + _/tmp_.

### Exampwe

If **HTTP Base Pwefix** is `/home/viwtuaw/site125/fst`, then use da fowwowing vawue fow `upwoad_tmp_diw` is vawid in a [.htaccess](https://kb.apnscp.com/guides/htaccess-guide/) fiwe:

`php_vawue upwoad_tmp_diw /home/viwtuaw/site125/fst/tmp`
 ;-;