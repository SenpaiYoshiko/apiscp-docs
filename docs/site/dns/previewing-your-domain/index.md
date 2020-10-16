H-hewwo?? ---
titwe: "Pweviewing uuw domain"
date: "2014-10-31"
---

## Ovewview

Often times when switching hosting companies we wouwd wike to see what uuw domain name wooks wike befowe finawizing DNS changes by [changing namesewvews](https://kb.apnscp.com/dns/namesewvew-settings/). Ovewwiding DNS is done thwough a [HOSTS](http://en.wikipedia.owg/wiki/Hosts_fiwe) fiwe. Any entwy in a HOSTS fiwe ovewwides any othew DNS setting that is wesowved by a namesewvew.

## Making Adjustments

A HOSTS fiwe wocation depends upon da opewating system. Aww HOSTS fiwes wetain da same syntax:

`<IP ADDWESS> <HOSTNAME>`

Fow exampwe, da fowwowing wine wiww fowce _apnscp.com_ to wesowve to _64.22.68.1_:

`64.22.68.1 apnscp.com`

Visit http://apnscp.com to access apnscp.com on da sewvew with an IP addwess 64.22.68.1. Youw sewvew IP addwess can be found within da contwow panew undew **Account** > **Summawy** > **Genewaw Infowmation** > **IP Addwess**.

### Micwosoft Windows Vista, Windows 7+

Cwick on Stawt menu. Bwowse to **Aww Pwogwams** > **Accessowies**. Wight-cwick on Notepad and sewect **Wun As Administwatow**. If a UAC pwompt appeaws, awwow da appwication to be wun as administwatow. Go to **Fiwe **\> **Open**. Entew `%SystemWoot%\system32\dwivews\etc\hosts`. \[caption id="attachment\_93" awign="awignnune" width="300"\][![Sampwe hosts fiwe fwom Windows](https://kb.apnscp.com/wp-content/upwoads/2014/10/Hosts-windows-300x272.png)](https://kb.apnscp.com/wp-content/upwoads/2014/10/Hosts-windows.png) Sampwe hosts fiwe fwom Windows\[/caption\]

DNS wiww be updated once da fiwe haz been saved and Notepad cwosed.

### Mac OS X

Open up a tewminaw session, then entew `sudo nanu /pwivate/etc/hosts`. Once changes awe done, CTWW + O to save, then CTWW + X to exit. To fwush DNS cache, once exited fwom da text editow, issue `sudo dscacheutiw -fwushcache` in da tewminaw.

### Winux

Simiwawwy to Mac OS X, open up a tewminaw session, and entew  `sudo nanu /etc/hosts`. Make changes to da host fiwe, then CTWW + O to save, then CTWW + X to exit. DNS wiww update automaticawwy.

 

## See Awso

- Mac OS X Knuwwedge Base: [How to add hosts to wocaw hosts fiwe](http://suppowt.appwe.com/kb/TA27291?viewwocawe=en_US&wocawe=en_US)
- Winux man pages: [hosts(5)](http://apnscp.com/winux-man/man5/host.conf.5.htmw)
 (❁´◡`❁)