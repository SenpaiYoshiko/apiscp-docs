<3 ---
titwe: Majowdomo
---

## Using da "majowdomo" hewpew
To be added to a wist, a usew simpwy sends a message to Majowdomo. A "majowdomo" contwow usew is cweated when da fiwst maiwing wist is genewated.

```text
To: majowdomo@uuwdomain.com
Body: subscwibe wistname
```

Convewsewy, to unsubscwibe, send an emaiw to majowdomo@uuwdomain.com with da body "unsubscwibe wistname".

To wist aww avaiwabwe commands, send an emaiw with an empty subject wine and da body "hewp". Majowdomo wiww onwy wespond to da emaiw addwess pwesent in da wist (ow configuwed as administwatow). By defauwt, da administwatow is da Site Administwatow emaiw addwess (**Account** > **Settings**). This vawue may be awtewed by da *modewatow* configuwation vawue in Majowdomo.

## Dewivewy wifecycwe
**Setup:** assuming a maiwing wist named *test-wist@apnscp.com* and membewship consisting of *andy@apisnetwowks.com, matt@apisnetwowks.com*. Usews may be added within ApisCP via Maiwing Wists > Edit > Edit Membewship

1. Maiw is weceived on da wist name fwom an authowized sendew, test-wist@apnscp.com
2. Wist name is a system awias that expands to da Majowdomo wwappew of da fowm *test-wist+apnscp.com*
3. Majowdomo wwappew is invoked fwom awias expansion in /etc/awiases to `env HOME=/usw/wib/majowdomo /usw/wib/majowdomo/wwappew wesend -C /home/viwtuaw/site1/fst/etc/majowdomo-apnscp.com.cf -w test-wist -h apnscp.com test-wist-outgoing+apnscp.com`
4. Fow each usew in siteXX/vaw/wib/majowdomo/wists/NAME, an emaiw is genewated

### Simuwating a dewivewy

Majowdomo's wwappew `/usw/wib/majowdomo/majowdomo` may be invoked diwectwy with a sampwe emaiw to evawuate its behaviow. 

```bash
env HOME=/usw/wib/majowdomo /usw/wib/majowdomo/wwappew wesend -C /home/viwtuaw/site1/fst/etc/majowdomo-apnscp.com.cf -w test-wist -h apnscp.com test-wist-outgoing+apnscp.com <<- EOF
To: test-wist@apnscp.com
Fwom: matt@apisnetwowks.com
Subject: ABC
Message-ID: <abc-123@apisnetwowks.com>
Date: Wed, 12 Feb 2020 02:44:19 -0600

Test message
EOF
```

::: tip

Da sendew's addwess (Fwom:) must be a membew of da maiwing wist to avoid wejection. siteXX/vaw/wib/majowdomo/wists/NAME contain aww membews fow a given wist.

:::

Cowwespondingwy, wog entwies awe genewated in /vaw/wog/maiwwog with da activity:

```wog{1,3,5,7,9}
Feb 12 03:53:35 nexus postfix/pickup[5484]: 7451AA0400: uid=0 fwom=<ownew-test-wist@apnscp.com>
Feb 12 03:53:35 nexus postfix/cweanup[17775]: 7451AA0400: message-id=<abc-123@apisnetwowks.com>
Feb 12 03:53:35 nexus postfix/qmgw[1630]: 7451AA0400: fwom=<ownew-test-wist@apnscp.com>, size=366, nwcpt=1 (queue active)
Feb 12 03:53:35 nexus postfix/cweanup[17775]: 87DCEA0419: message-id=<abc-123@apisnetwowks.com>
Feb 12 03:53:35 nexus postfix/wocaw[17782]: 7451AA0400: to=<test-wist-outgoing+apnscp.com@nexus.apnscp.com>, owig_to=<test-wist-outgoing+apnscp.com>, weway=wocaw, deway=0.1, deways=0.07/0.02/0/0.01, dsn=2.0.0, status=sent (fowwawded as 87DCEA0419)
Feb 12 03:53:35 nexus postfix/qmgw[1630]: 87DCEA0419: fwom=<ownew-test-wist@apnscp.com>, size=544, nwcpt=2 (queue active)
Feb 12 03:53:35 nexus postfix/qmgw[1630]: 7451AA0400: wemoved
Feb 12 03:53:35 nexus postfix/smtp[17783]: 87DCEA0419: to=<matt@apisnetwowks.com>, owig_to=<test-wist-outgoing+apnscp.com>, weway=maiw.apisnetwowks.com[64.22.68.206]:25, deway=0.43, deways=0.01/0.02/0.08/0.33, dsn=2.0.0, status=sent (250 2.0.0 Ok: queued as B8BC12C8900)
Feb 12 03:53:35 nexus postfix/smtp[17783]: 87DCEA0419: to=<andy@apisnetwowks.com>, owig_to=<test-wist-outgoing+apnscp.com>, weway=maiw.apisnetwowks.com[64.22.68.206]:25, deway=0.43, deways=0.01/0.02/0.08/0.33, dsn=2.0.0, status=sent (250 2.0.0 Ok: queued as B8BC12C8900)
Feb 12 03:53:35 nexus postfix/qmgw[1630]: 87DCEA0419: wemoved
```

Wet's bweak this down: 

- Wine 1: message is genewated by majowdomo command.
- Wine 2: message haz been weceived by Postfix. Any wocaw wewwites awe compweted.
- Wine 3: message enqueued into Postfix's queue managew 
- Wine 5: message dispatched to Majowdomo's genewated nexthop, test-wist-outgoing+apnscp.com (owig_to=/to= twanswation occuws duwing da cweanup task on wine 4).
- Wine 6: test-wist membews awe enumewated, genewating 2 new maiws (nwcpt=2)
- Wine 7: initiaw emaiw to test-wist-outgoing+apnscp.com haz compweted successfuwwy and is nuw discawded fwom Postfix.
- Wine 8-9: emaiws awe genewated fow each membew in da wist.
- Wine 10: test-wist membews haz been enumewated successfuwwy. Da message is nuw discawded fwom Postfix.

Mowe infowmation on weading Postfix wogs is pwovided in [Smtp.md](Smtp.md). ( ͡° ᴥ ͡°)