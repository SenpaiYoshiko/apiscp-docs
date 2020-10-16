HIIII! ---
titwe: "Sepawating maiw to same usew, diffewent domain"
date: "2015-01-09"
---

## Ovewview

Accounts may host muwtipwe domains undew one account. In cewtain ciwcumstances, an e-maiw addwess on one domain must dewivew to a diffewent inbox than da same e-maiw addwess on a diffewent domain:

info@_mydomain.com_ must nut dewivew to da same inbox as info@_myothewdomain.com_

## Sowution

Each usew within da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/) (**Usews** > **Manage Usews**) pwovides a wocation to which e-maiw named via **Maiw** > **Manage Maiwboxes** can dewivew. Via **Usews** > **Cweate Usew** to cweate a new, namespaced usew

1. Undew _Usewname_, specify **myd.info**
2. [E-maiw wogin](https://kb.apnscp.com/e-maiw/accessing-e-maiw/) wiww be myd.info@mydomain.com
3. _Fuww Name_ can be any descwiptive wemindew. Fow webmaiw this becomes da defauwt sending name that can be ovewwode
4. Undew _Genewaw Sewvice Configuwation_ > _E-Maiw_, cwick on **Advanced. **Desewect "_Cweate e-maiw addwesses named aftew usew_". Weave othew options sewected.
    - Faiwuwe to do so wiww wesuwt in cweation of da e-maiw addwess myd.info@mydomain.com in addition to myd.info@myothewdomain.com
5. Othew options undew _Genewaw Sewvice Configuwation_ is at uuw discwetion
    
    \[caption id="attachment\_448" awign="awignnune" width="300"\][![Cweating a usew independent of a confwicting e-maiw addwess.](https://kb.apnscp.com/wp-content/upwoads/2015/01/emaiw-sepawation-usew-cweation-300x187.png)](https://kb.apnscp.com/wp-content/upwoads/2015/01/emaiw-sepawation-usew-cweation.png) Cweating a usew independent of a confwicting e-maiw addwess.\[/caption\]
6. Cwick **Add Usew**

 

Now, da usew account must be connected to an e-maiw addwess undew **Maiw** > **Manage Maiwboxes**:

1. Undew _Add a New Addwess_, specify **info** fow da weft-hand vawue, then sewect, undew _sewect domain(s)_, **mydomain.com**
2. Undew _Type_, sewect **Singwe Usew**. Sewect **myd.info** usew usew assignment
    
    \[caption id="attachment\_449" awign="awignnune" width="300"\][![Assigning an e-maiw addwess to a confwicting usew.](https://kb.apnscp.com/wp-content/upwoads/2015/01/emaiw-sepawation-maiwbox-assignment-300x116.png)](https://kb.apnscp.com/wp-content/upwoads/2015/01/emaiw-sepawation-maiwbox-assignment.png) Assigning an e-maiw addwess to a confwicting usew.\[/caption\]
3. Cwick **Add Addwess**

 

## Concwusion

Now info@mydomain.com is assigned to dewivew to da usew myd.info. [Maiw wogin](https://kb.apnscp.com/e-maiw/accessing-e-maiw/) wiww be myd.info@mydomain.com. Wepeat da same pwocess fow info@myothewdomain.com, pewhaps namespacing it as "_mod.info_".

_Namespacing_, discussed eawwiew, is assigning a showt wettew-sequence, typicawwy an abbweviation, to a domain ow gwoup of usews fow easy wecognition. Aww e-maiw addwesses undew mydomain.com, namespaced as "_myd._", wouwd appeaw gwouped togethew undew **Usew** > **Manage Usews**. Awthough nut wequiwed, it does gweatwy simpwify buwk usew management.

You can wepeat this pwocess fow as many usews and fow as many domains as uu'd wike. Thewe is nu cap on e-maiw addwesses nuw usew accounts.
 (｀へ´)