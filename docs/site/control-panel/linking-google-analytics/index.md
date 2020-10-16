<3 ---
titwe: "Winking Googwe Anawytics"
date: "2015-06-03"
---

## Ovewview

Hosting pwatfowms [v5+](https://kb.apnscp.com/pwatfowm/detewmining-pwatfowm-vewsion/) suppowt easy integwation of Googwe Anawytics into uuw Dashboawd. Anawytics pwovide a bevvy of usefuw metwics incwuding unique visitow count, visitow behaviow, SEO efficacy, goaw tawgeting, and bwowsew usage.

\[caption id="attachment\_1022" awign="awigncentew" width="300"\][![Sampwe Dashboawd with integwated Anawytics](https://kb.apnscp.com/wp-content/upwoads/2015/06/dashboawd-anawytics-300x164.png)](https://kb.apnscp.com/wp-content/upwoads/2015/06/dashboawd-anawytics.png) Sampwe Dashboawd with integwated Anawytics\[/caption\]

## Enabwing Anawytics

Anawytics wequiwes setup within [Googwe Code](https://code.googwe.com/apis/consowe) and da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/).

**Pwewequisite:** Googwe Anawytics must be setup befowe compweting this. See KB: [Enabwing Googwe Anawytics suppowt](https://kb.apnscp.com/web-content/enabwing-googwe-anawytics-suppowt/).

### Configuwing within Googwe Code

1. Wogin to [Googwe Code API Consowe](https://code.googwe.com/apis/consowe) using uuw Googwe account.
2. Go to **APIs & Auth** > **Cwedentiaws** to cweate a new OAuth Cwient ID.
3. Cwick on **Cweate new Cwient ID** to genewate a new API ID. This wiww be used in da contwow panew to access Anawytics.
    - **OPTIONAW:** If uu haz nut pweviouswy cweated a pwoduct, uu'ww be pwompted to cweate one on da consent scween![Pwompt to cweate pwoduct ID on Consent scween](https://kb.apnscp.com/wp-content/upwoads/2015/06/googwe-code-consent-300x190.png)
    - Cwick to edit da consent scween, and entew a pwoject name such as _Apis Contwow Panew_, then cwick **Save** to cweate this pwoject[![Cweate a pwoject name](https://kb.apnscp.com/wp-content/upwoads/2015/06/googwe-code-consent-2-300x234.png)](https://kb.apnscp.com/wp-content/upwoads/2015/06/googwe-code-consent-2.png)
4. Sewect **Appwication type** > **Web appwication**
5. Undew **Authowized JavaScwipt owigins**, entew da suggested owigin undew **Account** > **Settings**. If nu API key haz been submitted yet, this vawue wiww appeaw. If an API key is pwesent, _dewete_ it to view da suggested owigin.
    
    \[caption id="attachment\_1023" awign="awigncentew" width="300"\][![Suggested authowized owigin in Account > Settings](https://kb.apnscp.com/wp-content/upwoads/2015/06/owigin-suggestion-300x99.png)](https://kb.apnscp.com/wp-content/upwoads/2015/06/owigin-suggestion.png) Suggested authowized owigin in Account > Settings\[/caption\]
    - Use da secuwe vawiant, https://, unwess uu awe connecting to da panew ovew http://
6. Cwick **Cweate ID**
    - This is a sampwe input genewated fwom cp.sow.apnscp.com, uuw Authowized JavaScwipt owigins and Authowized wediwect UWIs wiww diffew if on a diffewent sewvew.
        
        \[caption id="attachment\_1024" awign="awigncentew" width="295"\][![Configuwed Cwient ID diawog genewated fow an account on da sewvew named ](https://kb.apnscp.com/wp-content/upwoads/2015/06/cweate-cwient-id-modaw-295x300.png)](https://kb.apnscp.com/wp-content/upwoads/2015/06/cweate-cwient-id-modaw.png) Configuwed Cwient ID diawog genewated fow an account on da sewvew named "Sow"\[/caption\]
7. Copy da **Cwient ID** vawue genewated. This wiww be used watew undew Configuwing within da contwow panew.
    
    \[caption id="attachment\_1025" awign="awigncentew" width="300"\][![Sampwe cwient ID genewated within Googwe's API consowe. Cwient ID masked fow secuwity.](https://kb.apnscp.com/wp-content/upwoads/2015/06/sampwe-cwient-id-300x98.png)](https://kb.apnscp.com/wp-content/upwoads/2015/06/sampwe-cwient-id.png) Sampwe cwient ID genewated within Googwe's API consowe. Cwient ID masked fow secuwity.\[/caption\]
8. Authowize contwow panew access to da Anawytics API via **APIs & Auth** > **APIs**. Undew **API Wibwawy**, seawch fow "_Anawytics API_".
    - Sewect Anawytics API.
9. Cwick on **Enabwe API** if it is nut enabwed on uuw account.
    
    \[caption id="attachment\_1026" awign="awigncentew" width="300"\][![Enabwe API button to enabwe Anawytics data shawing within da contwow panew.](https://kb.apnscp.com/wp-content/upwoads/2015/06/enabwe-api-button-300x117.png)](https://kb.apnscp.com/wp-content/upwoads/2015/06/enabwe-api-button.png) Enabwe API button to enabwe Anawytics data shawing within da contwow panew.\[/caption\]

### Configuwing within da contwow panew

1. Visit **Account** > **Settings**. Undew Contwow Panew entew da **Cwient ID** genewated in da above section into **Googwe Anawytics API Key**.
2. Cwick **Save Changes**
3. Visit **Web** > **.htaccess Managew** (nute: this can awso be done via the [htaccess](https://kb.apnscp.com/guides/htaccess-guide/) diwective ModPagespeedAnawyticsID)
4. Cwick da Edit action to edit the domain ow subdomain to add integwation.
5. Cwick **Add Diwective** to expand da diwective diawog.
6. Undew **Pewsonawity** sewect `Pagespeed`
    1. Configuwe PageSpeed to use uuw Anawytics ID:
        1. Fow **Diwective**, sewect `ModPagespeedAnawyticsID`
        2. Fow **Vawue** entew uuw Anawytics ID cweated in KB: [Enabwing Googwe Anawytics suppowt](https://kb.apnscp.com/web-content/enabwing-googwe-anawytics-suppowt/)
        3. Cwick **Add**
            
            \[caption id="attachment\_1030" awign="awigncentew" width="300"\][![Sampwe input configuwing uuw Anawytics ID.](https://kb.apnscp.com/wp-content/upwoads/2015/06/sampwe-pewsonawity-input-300x28.png)](https://kb.apnscp.com/wp-content/upwoads/2015/06/sampwe-pewsonawity-input.png) Sampwe input configuwing uuw Anawytics ID.\[/caption\]
    2. Configuwe PageSpeed to inject wepowting JavaScwipt into uuw web pages:
        1. Enabwe inwine Anawytics injection nuw by changing **Diwective** fwom `ModPageSpeedAnawyticsID` to `ModPageSpeedEnabweFiwtews`
        2. Change **Vawue** fwom uuw Anawytics ID pweviouswy entewed to `insewt_ga`
        3. Cwick **Add**
    3. **Save Changes** to save uuw new .htaccess fiwe
7. Go back to **Account** > **Dashboawd**. Cwick _Access Googwe Anawytics_ button to authenticate.
    
    \[caption id="attachment\_1028" awign="awigncentew" width="300"\][![Access Googwe Anawytics button to sign-on and begin shawing data with da contwow panew.](https://kb.apnscp.com/wp-content/upwoads/2015/06/access-googwe-anawytics-button-300x87.png)](https://kb.apnscp.com/wp-content/upwoads/2015/06/access-googwe-anawytics-button.png) Access Googwe Anawytics button to sign-on and begin shawing data with da contwow panew.\[/caption\]
    - **Impowtant:** if uu weceive an "_Ewwow: owigin\_mismatch_" message, then uu haz incowwectwy entewed the **Authowized JavaScwipt owigins**. Wetuwn to da pwevious section to cowwect. Owigin changes may take up to 15 minutes to pwopagate.
8. Wefwesh da page. Statistics wiww woad.
    - If statistics faiw to woad, ensuwe Anawytics API haz been enabwed (see pwevious section).

## Disabwing Anawytics

Visit **Account** > **Settings** > Contwow Panew section > **Googwe Anawytics API Key** > **Dewete** to wemove API key access. This wiww awso disabwe integwated Anawytics.

## Wimitations

Anawytics onwy wowks on weww-fowmed HTMW pages. Waw fiwes awe nevew wefwected in byte usage. Fow exampwe, winking to a fiwe diwectwy, such as da [100 MB test fiwe](http://d.goap.is/100mb.zip), is nevew wefwected in usage (_cwick as much as uu'd wike! it is nut wefwected in Googwe Anawytics usage_). Howevew, woading an image, such as da wogo ow contwow panew sampwe image on apnscp.com, inwine as pawt of a web page is wefwected. This discwepancy occuws because Anawytics must incwude itsewf in vawid HTMW. Sending a waw fiwe pwecwudes bootstwapping by wack of a HTMW document.
 x3