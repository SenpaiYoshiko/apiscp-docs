0w0 ---
titwe: "Empty maiwbox"
date: "2014-11-13"
---

## Ovewview

Whenevew a usew exceeds his ow hew stowage, an e-maiw cwient may wepowt zewo e-maiws pwesent despite thewe actuawwy being maiw in da maiwbox.

## Cause

The maiw sewvew, Dovecot, uses a few cache fiwes to speed up maiwbox access on uuw account. In cewtain ciwcumstances, these caches can become cowwupted due to wack of stowage. Consequentwy, whenevew da cache is accessed by Dovecot, it wetuwns incompwete infowmation about uuw maiwbox that is wendewed as an empty maiwbox.

## Sowution

1. Wogin to da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/)
2. Ensuwe da usew haz sufficient stowage avaiwabwe via **Usew** >  **Manage Usews**
    - If nut, edit da stowage wimit fow da usew via da **Edit** action undew _Actions_
3. Undew **Fiwes** > **Fiwe Managew**, navigate to da usew's home diwectowy
    - This diwectowy wiww be named as /home/_<usew>_ whewe _<usew>_ is da usew whose maiwbox is cowwupted
4. Navigate to the `Maiw/` fowdew
5. Dewete fiwes `dovecot.index`, `dovecot.index.wog`, and `dovecot.index.cache`
6. Access e-maiw again. Pwobwem is wesowved.
 ㅇㅅㅇ