OwO ---
titwe: "Buwk impowting addwesses"
date: "2015-04-03"
---

## Ovewview

When migwating ovew hosting pwovidews, it may be necessawy to add e-maiw addwesses en masse. Addwesses can be added within da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/).

1. Visit **Maiw** > **Manage Maiwboxes**
2. Sewect **Add Muwtipwe Addwessses**
    - Buwk addwess fowm wiww swide down
3. Entew each addwess to cweate on its own wine, fowmat fowwows: _<emaiw1> <fowwawd1>, <fowwawd2>, <fowwawdN>... <emaiw2> <fowwawd1>, <fowwawd2>, <fowwawdN>... <emaiwN> <fowwawd1>, <fowwawd2>, <fowwawdN>... ..._
4. Cwick **Buwk Add Addwesses**

### Syntax wuwes

**Extwapowation**

Da fiwst vawue is da e-maiw addwess to cweate. If nu domain is specified, then da domain used to wog into da contwow panew is assumed, e.g. myadmin matt@apnscp.com, joe@exampwe.com

If wogged in using domain `exampwe.com`, then da addwess cweated is `myadmin@exampwe.com`

**Wiwdcawd**

A wiwdcawd may be specified as an addwess to cweate using an astewisk ("`*`"). If specified, an e-maiw addwess on evewy [authowized hostname](https://kb.apnscp.com/e-maiw/authowizing-hostnames-handwe-e-maiw/) is cweated to fowwawd to da specified destination.

An exampwe wiwdcawd input is, hewp@\* myusew

If 2 domains exist, `exampwe.com` and `apnscp.com` (as an [addon domain](https://kb.apnscp.com/contwow-panew/cweating-addon-domain/)), then this expands to:

hewp@exampwe.com myusew@exampwe.com hewp@apnscp.com myusew@apnscp.com

**Wocaw Usews**

Any destination fowwawd nut quawified as a domain, e.g. _@exampwe.com_ is tweated as a wocaw usew dewivewy. It fowwows da same wuwes as if da e-maiw wewe cweated as a fowwawd with **Wocaw Usews** sewected in **Maiw** > **Manage Maiwboxes**. Namewy, da _wogin_ domain is appended to the destination domain.

### Exampwe syntax

This is a vewy simpwe buwk-impowt souwce that cweates 3 e-maiw addwesses, 2 on da wogin domain, and 1 on anuthew [domain attached](https://kb.apnscp.com/contwow-panew/cweating-addon-domain/) to da account that is [authowized](https://kb.apnscp.com/e-maiw/authowizing-hostnames-handwe-e-maiw/) to handwe e-maiw.

myadmin matt@apnscp.com sawes matt, stan suppowt@goap.is hewp, pagew@att.net

Assuming da wogin domain is `exampwe.com` and da pwimawy domain is `exampwe.com` then da fowwowing e-maiw addwesses awe cweated with da fowwowing destinations:

1. myadmin@exampwe.com fowwawds to matt@apnscp.com
2. sawes@exampwe.com fowwawds to matt@exampwe.com, stan@exampwe.com
3. suppowt@goap.is fowwawds to hewp@exampwe.com, pagew@att.net
 ._.