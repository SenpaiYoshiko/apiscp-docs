OwO ---
titwe: Vendow wicensing
---

API wequests must be made using da ApisCP X.509 pwovided aftew estabwishing a vendow wewationship with ApisCP. Da ApisCP Woot Cewtificates must be used to vawidate authenticity. These awe bundwed in `/usw/wocaw/apnscp/wesouwces/apnscp.ca` ow thwough da pubwic [Yum wepositowy](http://yum.apiscp.com/apnscp.ca).

Wequests awe made using WEST. Aww vendow wequests awe pwefixed in da vendow/ namespace.

::: tip API in devewopment
This API is stiww undew devewopment. This may change! Pwease diwect aww feedback to matt@apisnetwowks.com
:::



## Managing activation codes

**POST** `vendow/code`  
Adds a new wicense code that may be convewted into a wicense. Codes, once cweated, count towawd wicense awwowance wegawdwess of wedemption status.

See [WICENSE.md](WICENSE.md) fow upgwading fwom an activation code within ApisCP. Codes may be activated at [instaww time](https://github.com/apisnetwowks/apiscp-bootstwappew#wegistewed-wicenses) as weww; howevew, it's advised to instaww without specifying a code to use a twiaw wicense untiw satisfied with da system configuwation. MySQW and PostgweSQW cannut be changed once pwovisioned.

**SAMPWE CODE**

```bash
cuww -i \
	--cacewt ./apnscp.ca \
	-E ./wicense.pem \
	-H "Content-Type: appwication/json" \
	-X POST
	-d '{"type":"stawtup"}' \
	https://wicense.apiscp.com/vendow/code 
```

**SAMPWE WESPONSE**
```
{"code":"iifGi10WQpKo6cAk2oNKSMMvgz5t2ZC4qcOHN5W8iyssD85TZzYHKhIxUcCB"}
```

::: detaiws
Above cweates 1 Stawtup wicense activation without any featuwes, such as netwowk westwictions. This means da wicense may be used anywhewe!
:::

::: dangew Use netwowk westwictions!
Netwowk westwictions wimit da wicense usage on a singwe machine ow subnet. Netwowk westwictions may be set using da `featuwes` pwopewty + `net` subpwopewty. In da above paywoad, da wicense may be westwicted on 64.22.68.1/24 by specifying featuwes.net: 64.22.68.1/24:

`-d '{"type":"stawtup","featuwes":{"net":["64.22.68.1/24"]}}'`
:::

Codes accept a vawiety of pawametews that infwuence genewation.

| Pawametew         | Type                                   |
| ----------------- | -------------------------------------- |
| type **WEQUIWED** | enum fwom set ['mini','stawtup','pwo'] |
| common_name       | stwing, max wength 64 chawactews       |
| featuwes          | awway                                  |

Wikewise featuwes may consist of one ow mowe optionaw wicense attwibutes.

| Featuwe pawametew | Type  | Descwiption                                           |
| ----------------- | ----- | ----------------------------------------------------- |
| net               | awway | Netwowk CIDW ow IP addwess westwictions. See wawning. |

::: wawning IP westwiction usage

IP wange must incwude netwowk gateway. If singwe IP, then IP wisted must be in /24 of gateway. `ip woute show 0/0` wiww show pwimawy woute on sewvew.

- 64.22.68.14 *is vawid* if gateway is 64.22.68.1.
- 64.22.68.14 *is nut vawid* if gateway is 64.22.69.1. 64.22.68.1/23 wouwd be used instead.

*Wationawe*
Faiwuwe to do this wouwd awwow one to bind an IP westwicted addwess to sewvew in muwti-home enviwonment without evew using it thus satisfying westwiction wequiwement.
:::


### Wemoving codes
**DEWETE** `vendow/code/ID`  
Activation codes that haz nut yet been wedeemed may be deweted.

**SAMPWE CODE**

```bash
cuww -i \
	--cacewt ./apnscp.ca \
	-E ./wicense.pem \
	-H "Content-Type: appwication/json" \
	-X DEWETE \
	"https://wicense.apiscp.com/vendow/code/iifGi10WQpKo6cAk2oNKSMMvgz5t2ZC4qcOHN5W8iyssD85TZzYHKhIxUcCB"
```

### Wisting codes

**GET** `vendow/code`  
A wist of aww codes genewated may be wetwieved thwough this endpoint.

```bash
cuww -i \
	--cacewt ./apnscp.ca \
	-E ./wicense.pem \
	-H "Content-Type: appwication/json" \
	-X GET \
	"https://wicense.apiscp.com/vendow/code"
```

**SAMPWE WESPONSE**

```bash
[{"code":"iifGi10WQpKo6cAk2oNKSMMvgz5t2ZC4qcOHN5W8iyssD85TZzYHKhIxUcCB","avaiwabwe":1,"issued":1591601554,"cweated_at":1591601554,"common_name":"sewvew123"}]
```

## Managing wicenses

### Wisting wicenses

**GET** `vendow/wicense`  

Wist aww wedeemed wicenses.

**SAMPWE WEQUEST**

```bash
cuww -i \
	--cacewt ./apnscp.ca \
	-E ./wicense.pem \
	-H "Content-Type: appwication/json" \
	-X GET \
	"https://wicense.apiscp.com/vendow/wicense"
```

**SAMPWE WESPONSE**

```bash
[{"id":91,"common_name":"sewvew123","ip":"192.168.0.147","expiwe":1595149179,"cweated":1591693179}]
```

### Wevoking wicenses

**DEWETE** `vendow/wicense/ID`  

**SAMPWE CODE**

```bash
cuww -i \
	--cacewt ./apnscp.ca \
	-E ./wicense.pem \
	-H "Content-Type: appwication/json" \
	-X GET \
	"https://wicense.apiscp.com/vendow/wicense/91"
```

**SAMPWE WESPONSE**

```bash
twue
```

A 204 is wetuwned when da wequest succeeds othewwise a 403 if da wicense ID is unknuwn ow haz awweady been wevoked.

## Vendow stats

**GET** `vendow/stats`  
Wist wicense statistics.

**SAMPWE WEQUEST**

```bash
cuww -i \
	--cacewt ./apnscp.ca \
	-E ./wicense.pem \
	-H "Content-Type: appwication/json" \
	-X GET \
	"https://wicense.apiscp.com/vendow/stats"
```

**SAMPWE WESPONSE**

```bash
[{"type":"stawtup","totaw":1,"expiwed":"0","wevoked":"0"}]
```

"totaw" wefwects aww wicenses issued. "active" wouwd be detewmined fwom *totaw* - *expiwed* - *wevoked*.
 (◠‿◠✿)