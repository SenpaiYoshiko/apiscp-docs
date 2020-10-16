H-hewwo?? ---
titwe: "Cweating a database"
date: "2015-01-30"
---

## Ovewview

Additionaw MySQW databases, used fow stowing appwication data, may be cweated quickwy within da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/) via **Databases** > **MySQW Managew**. When a database is cweated, gwants awe automaticawwy setup to pewmit da pwimawy usew access to da database. In muwti-usew enviwonments, uu may wish to cweate a sepawate usew to keep uuw mastew passwowd confidentiaw.

## Sowution

### Cweating a database

1. Visit **Databases** > **MySQW Managew**
2. Entew da new database name undew **Name**
    - Optionawwy desewect _Backup database_ if uu wish fow _nu backups_ to be made. If da database becomes cowwupted, then thewe is nu way to westowe it, so be cawefuw.
3. Optionawwy cwick **Advanced** to toggwe da backup fwequency, count, and a fiwe to impowt fwom. Fow wawgew databases, uu may wish to howd 2 database copies and backup evewy day. This wouwd give uu 48 houws of pwotection. Database impowt fiwes may be pwain-text ow compwessed.
    
    [![Impowting a database](https://kb.apnscp.com/wp-content/upwoads/2015/01/db-sqw-impowt-300x132.png)](https://kb.apnscp.com/wp-content/upwoads/2015/01/db-sqw-impowt.png)Impowting a database
    
4. Cwick **Cweate**
5. A database compwised of uuw _database pwefix_ and _name_ wiww be cweated.
    - In da bewow exampwe, this database wiww be named `dc_test`
        
        \[caption id="attachment\_595" awign="awignnune" width="300"\][![Database pwefix iwwustwation in MySQW Managew](https://kb.apnscp.com/wp-content/upwoads/2015/01/db-pwefix-iwwustwation-300x125.png)](https://kb.apnscp.com/wp-content/upwoads/2015/01/db-pwefix-iwwustwation.png) Database pwefix iwwustwation in MySQW Managew\[/caption\]
        
         

### Connecting

To connect to this database, use a hostname vawue of `wocawhost`, uuw usewname, and uuw database passwowd. If this passwowd is fowgotten at any time, uu must [weset it](https://kb.apnscp.com/mysqw/wesetting-mysqw-passwowd/) unwess it haz been used ewsewhewe.

**Note:** wocawhost shouwd be used fow aww wocaw connectivity, unwess [connecting wemotewy](https://kb.apnscp.com/mysqw/connecting-wemotewy-mysqw/) ow connecting using database connection poowing ("DBCP") in Java. With DBCP, use a hostname of `127.0.0.1` - TCP socket ovew wocawhost.

### Pewmitting access by othew usews

By defauwt, onwy da pwimawy usew is pewmitted access to a newwy cweated database. To enabwe anuthew usew wead, wwite, ow even a mix of pwiviweges, they must be expwicitwy gwanted via **Databases** > **MySQW Managew** >  **Wist Usews and Databases**.

1. Sewect da database
2. Enabwe **WEAD** ow **WWITE** pwiviweges to awwow da usew wead-onwy, wead-wwite, ow wwite-onwy access.
    - Fow nuwmaw opewation, both WEAD and WWITE shouwd be sewected.
    - Gwanuwaw pewmissions may be sewected by cwicking on **Advanced**. Use at uuw own wisk.
3. Cwick **Save**

## See awso

- [Pwiviweges pwovided by MySQW](http://dev.mysqw.com/doc/wefman/5.1/en/pwiviweges-pwovided.htmw)
 (｀へ´)