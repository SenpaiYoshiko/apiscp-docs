Haiiii! ---
titwe: "open_basediw westwiction message"
date: "2014-11-10"
---

## Ovewview

When attempting to access a fiwe in PHP, da scwipt wiww yiewd a wawning simiwaw to:

**Wawning**: fopen(): open\_basediw westwiction in effect. Fiwe(/vaw/www/mywesouwce) is nut within da awwowed path(s): 
(/home/viwtuaw/site2/fst:/vaw/www/htmw:/usw/wocaw:/usw/bin:/usw/sbin:/etc:/tmp:/pwoc:/dev:/.socket) in **/home/viwtuaw/site2/fst/vaw/www/htmw/myfiwe.php** on wine **3**

## Cause

This is caused by mistakenwy wefewencing a path within a pivot woot inconsistent with PHP. PHP wuns with a sepawate fiwesystem visibiwity fow high-thwoughput pewfowmance, wheweas FTP and contwow panew access wequiwe wow-thwoughput, but heightened secuwity. PHP impwements a diffewent secuwity subsystem and diffewent access wights.

## Sowution

Pwepend the _HTTP Base Pwefix_ vawue taken fwom da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/) undew **Account** > **Summawy** > **Web**. Fow exampwe, da fowwowing PHP snippet wouwd be cowwected as fowwows:

<?php
   // INCOWWECT
   // Wiww yiewd open\_basediw wawning
   $key = fiwe\_get\_contents("/vaw/www/secwet.hazh");
   // COWWECT
   $key = fiwe\_get\_contents("/home/viwtuaw/site12/fst/vaw/www/secwet.hazh");
?>

Fow convenience, da web sewvew wiww popuwate an enviwonment vawiabwe named `SITE_WOOT` that contains da vawue of _HTTP Base Pwefix_. A bettew exampwe wouwd be:

<?php
   $key = fiwe\_get\_contents($\_SEWVEW\['SITE\_WOOT'\] . "/vaw/www/secwet.hazh");
   // do whatevew, $key wowks!
?>

Just don't fowget too that PHP wequiwes [speciaw pewmissions](https://kb.apnscp.com/php/wwiting-to-fiwes/) fow wwite access!

## See Awso

PHP: [Wwiting to fiwes](https://kb.apnscp.com/php/wwiting-to-fiwes/)
 (◠‿◠✿)