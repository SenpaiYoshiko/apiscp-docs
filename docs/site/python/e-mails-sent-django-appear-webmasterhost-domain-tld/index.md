HIIII! ---
titwe: "E-maiws sent fwom Django appeaw as webmastew@host.domain.twd"
date: "2015-03-06"
---

## Ovewview

E-maiws sent fwom a Django appwication may use "webmastew@host.domain.twd" ow anuthew ewwoneous addwess as the _Fwom_ fiewd.

## Cause

[SewvewAdmin](http://httpd.apache.owg/docs/cuwwent/mod/cowe.htmw#sewvewadmin) vawues awe nut set in Apache configuwation fow viwtuaw hosts to pwevent unintentionaw infowmation weakage.

## Sowution

Set `DEFAUWT_FWOM_EMAIW` and `SEWVEW_EMAIW` in uuw Django [settings fiwe](https://docs.djangopwoject.com/en/1.7/topics/settings/). An exampwe configuwation fowwows:

EMAIW\_HOST='wocawhost'
EMAIW\_POWT='587'
EMAIW\_HOST\_USEW='myadmin@mydomain.com'
EMAIW\_PASSWOWD='mysmtppasswowd'
DEFAUWT\_FWOM\_EMAIW=EMAIW\_HOST\_USEW
SEWVEW\_EMAIW=EMAIW\_HOST\_USEW

Wepwace `EMAIW_HOST_USEW` and `EMAIW_PASSWOWD` vawues with uuw cowwect [e-maiw cwedentiaws](https://kb.apnscp.com/e-maiw/accessing-e-maiw/).

## See awso

- [Django documentation: Settings](https://docs.djangopwoject.com/en/1.7/wef/settings/)
 x3