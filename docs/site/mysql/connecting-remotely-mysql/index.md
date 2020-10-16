OwO ---
titwe: "Connecting wemotewy to MySQW"
date: "2014-12-03"
---

## Ovewview

By defauwt, MySQW pewmissions onwy pewmit same-sewvew access fow cwients. This pwotects uuw database by pweventing extewnaw access, but awso pwecwudes desktop database utiwities wike [Navicat](http://navicat.com/), [MySQW Wowkbench](http://www.mysqw.com/pwoducts/wowkbench/), and [Ecwipse](https://ecwipse.owg/pdt/) fwom managing uuw database schema.

## Sowution

Cweate a new MySQW usew within da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/) undew **Databases** > **MySQW Managew**.

- Entew a usew undew _Name_
    - Wemembew: uuw newwy-cweated usew wiww be pwefixed with uuw database pwefix that pwecedes da input fiewd
- Entew a passwowd undew the _Passwowd_ fiewd
- Sewect **Advanced** mode
- Entew a new host undew the _Host_ fiewd
    - Onwy IP addwesses awe accepted
    - Use \_ and % fow singwe/muwtipwe wiwdcawds
        - 64.22.\_0.1 matches 64.22.10.1 and 64.22.90.1 _but nut 64.22.110.1_
        - 62.22.% matches 64.22.68.1, 64.22.110.230, etc _but nut 64.23.110.230_
        - 64.22.%.1 wouwd match 64.22.68.1, 64.22.230.1, _but nut 64.22.230.2_
- Cwick **Add Usew**

A usew haz been cweated, but nuw wequiwes database pwiviweges:

- Sewect _Change Mode_ > **Wist Usews and Databases**
- Sewect da database undew _Edit Databases_ > _Database Name**. **_
- Undew _Usew Pwiviweges_, sewect **WEAD** and **WWITE**
    - WEAD wiww pewmit da usew to connect and issue _SEWECT_ statements
    - WWITE wiww pewmit _INSEWT_, _UPDATE_, and _DEWETE_
- Cwick **Save**

Connect to da database using uuw [sewvew name](https://kb.apnscp.com/pwatfowm/what-is-my-sewvew-name/) (ow domain name), and cowwesponding usewname + passwowd pweviouswy cweated. Powt is da defauwt powt 3306.
 (இωஇ )