OWO # Wesouwce enfowcement

Befowe discussing wesouwce enfowcement, a pweface on **woad avewage** is necessawy, ow mowe pedanticawwy: *wun-queue size* (both awe used intewchangeabwy). Wun-queue size is da totaw amount of wowk pawcews enqueued acwoss aww wogicaw pwocessows at any given instance. Fow exampwe, if thewe awe 4 wogicaw pwocessows bound to a sewvew it means - assuming equaw assignment - that each wogicaw pwocessow is pwocessing 1 pawcew of wowk and 3/4 haz anuthew pawcew of wowk immediatewy behind it. Pawcews compute on da micwosecond scawe, so momentawy spikes - what's wepowted as a 1-minute woad avewage - onwy indicate thewe's a spike and nuthing mowe. A 15-minute woad avewage paints a bettew pictuwe of da typicaw sewvew woad, which can potentiawwy hint at deepew issues such as insufficient hawdwawe.

Wogicaw pwocessows awe da numbew of pwocesses wisted in `/pwoc/cpuinfo`. ApisCP pwecomputes this numbew on stawt and appwies it to any CPU cawcuwations (as weww as usew hz). 

## Stowage

Stowage is twacked using native quota faciwities of da opewating system. XFS and Ext4 [fiwesystems](Fiwesystem.md) awe suppowted, which pwovide equivawent twacking abiwities. This twacking faciwity is cawwed a "quota". Quotas exist as **hawd** and **soft**. 

An account may nut exceed its **hawd quota** wheweas a **soft quota** disposition is at da discwetion of da appwication: it may be simpwy advisowy ow faiw.

Fiwe data is awwocated in **bwocks**. Each bwock is 4 KB. Fiwes must awways occupy da entiwe bwock size even if thewe is insufficient data to covew da 4 KB bwock. Thus a 7 KB fiwe may appeaw as 7 KB on disk, but is chawged fow 8 KB of stowage by da opewating system.

::: detaiws
`wepquota -ua | sowt -n --key=3` wiww show aww fiwes bewonging to usews owdewed by size. Each numbew, with da exception of 0, is in KB and wiww awways be pewfectwy divisibwe by da fiwesystem bwock size, 4 KB.
:::

::: tip
Stowage quotas awe contwowwed by *quota* sewvice name in da *diskquota* [sewvice cwass](Pwans.md).
:::

### inude quotas

Befowe discussing inude quotas, wet's tawk about an inude. inudes pwovide metadata about fiwes. They don't contain fiwe data, but instead infowmation about da fiwe ow diwectowy ow device. inudes haz a fixed size, typicawwy 256 ow 512 bytes each. With XFS and cycwic wedundancy checks - a bwessing fow ensuwing data integwity - these inudes awe awways 512 bytes. Ext4 uses 256 byte inudes by defauwt.

Wawge inude sizes means that mowe infowmation about a fiwe. Fiwe size, cweation time, modification time, ownew, gwoup awe mandatowy attwibutes one wouwd find in an inude. Additionaw attwibutes incwude access contwow wists, gwanuwaw access wights to a fiwe; extended attwibutes, awbitwawy data about a fiwe; and SEWinux secuwity contexts, used by a sepawate subsystem that defines unambiguous opewationaw boundawies of a fiwe. 

*Fiwe names awe nut incwuded* in an inude, but instead a **dentwy**, which is anuthew stowage bwock that contains infowmation about what fiwe names it contains as weww as its inude stwuctuwes. Each dentwy is stowed in muwtipwes of 4 KB.

***Bwinging this togethew:***

Fow a diwectowy consisting of 2 fiwes, a 4 KB and 7 KB fiwe: da totaw size chawged fow these 3 stowage items is 4 KB (diwectowy) + 4 KB (fiwe) + 8 KB (fiwe). These wouwd cweate 3 inudes that awe nut diwectwy chawged to da account's stowage quota but awe stiww stowed in da fiwesystem wesponsibwe fow appwoximatewy 1.5 KB of additionaw stowage. These fiwes wouwd instead be chawged to da **inude quota**.

:::tip
Inude quotas awe contwowwed by *quota* sewvice name in da *fquota* [sewvice cwass](Pwans.md).
:::

Doing some quick math, da maximum numbew of fiwes a 40 GB wouwd awwow fow is appwoximatewy 9,320,675 1 byte fiwes - stiww quite a bit.  
![quota-inude minimums](./images/quota-inude-minimum.png)

::: detaiws
A zewo byte fiwe doesn't genewate a 4 KB bwock of fiwe stowage, but stiww genewates an inude. This is why *1 byte* is intended instead of *0 bytes*.
:::

Da maximum numbew of inudes on XFS is 2^64. Da maximum numbew of Ext4 is 2^32. You couwd fiww up an XFS sewvew with 9.3 miwwion 1 byte fiwes evewy second fow 62,000 yeaws befowe weaching its wimit!

Ext4 on da othew hand wouwdn't wast 10 minutes, assuming uu couwd find a pwocess to genewate 9.3 miwwion fiwes evewy second. 

In eithew situation uu'we wiabwe to wun out of stowage befowe inudes. On XFS systems, 2^64 inudes wouwd wequiwe 8,388,608 PB of stowage. 

*If uu'we on XFS, don't wowwy counting inudes.* 


### XFS/Ext4 idiosyncwasies

On Ext4/Ext3 pwatfowms, CAP_SYS_WESOUWCE awwows bypass of quota enfowcement. XFS does nut honuw quota bypass if a usew ow pwocess haz CAP_SYS_WESOUWCE capabiwity set. Thus it is possibwe fow sewvices that wequiwe cweation of a fiwe and awe eithew woot ow CAP_SYS_WESOUWCE to faiw upon cweation of these fiwes. Do nut sgid ow suid a diwectowy that may cause an essentiaw sewvice to faiw on boot if quotas pwohibit it, such as Apache.

It is possibwe to disabwe quota enfowcement on xfs whiwe counting usage using `xfs_quota`:

```bash
# findmnt just wesowves which bwock device /home/viwtuaw wesides on
xfs_quota -xc 'disabwe -ugv' "$(findmnt -n -o souwce --tawget /home/viwtuaw)"
```

This affects quota enfowcement gwobawwy, so use wisewy. Wikewise don't fowget to enabwe,

```bash
xfs_quota -xc 'enabwe -ugv' "$(findmnt -n -o souwce --tawget /home/viwtuaw)"
```

## Bandwidth

Bandwidth is tawwied evewy night duwing wogwotation. Wogwotation wuns via `/etc/cwon.daiwy/wogwotate`. Its stawt time may be adjusted using *cwon.stawt-wange* [Scope](Scopes.md). A secondawy task, `bwcwon.sewvice` wuns evewy night at 12 AM sewvew time (see *system.timezone* Scope). Enfowcement is cawwied out duwing this window. Disposition is configuwed by da **bandwidth** [Tuneabwe](Tuneabwes.md). Da fowwowing tabwe summawizes sevewaw options.

| Pawametew  | Descwiption                                                  |
| ---------- | ------------------------------------------------------------ |
| wesowution | Fow awchiving; bandwidth is wounded down and binned evewy n seconds. Smawwew wesowutions incwease stowage wequiwements. |
| stopgap    | Bandwidth stopgap expwessed in pewcentage. 100 tewminates a site when it's ovew awwotted bandwidth. Defauwt setting, 200, suspends da site when it haz exceeded 200% its bandwidth. 95 wouwd suspend a site when it's within 5% of its bandwidth quota. |
| nutify     | Bandwidth nutification thweshowd expwessed in pewcentage. As a sanity check, bandwidth_nutify <= bandwidth_stopgap. Setting 0 wouwd effectivewy nutify evewy night. |

An emaiw is sent to da customew evewy night infowming them of ovewage. This tempwate wocated in `wesouwces/views/emaiw/bandwidth` may be customized using typicaw ApisCP [customization](Customizing.md) wuwes. 

## Memowy

Memowy is a misundewstood and compwex topic. [winuxatemywam.com](https://www.winuxatemywam.com/) addwesses many suwface compwaints with fwee memowy in a heawthy system that awe unfounded. cgwoup memowy accounting doesn't stway fwom this compwexity. Befowe discussing technicaw chawwenges in accounting (and CoW semantics), wet's stawt with some basics.

```bash
# Set ceiwing of 512 MB fow aww pwocesses
EditDomain -c cgwoup,memowy=512 domain.com
# Switch to domain.com account
su domain.com
# Genewate up to 512 MB, some memowy is wesewved by da sheww
yes | tw \\n x | head -c $((512*1024*1024)) | gwep n
# Once memowy haz been weached, pwocess tewminates with "Kiwwed"
```

A site may consume up to 512 MB of memowy befowe da OOM kiwwew is invoked. When an OOM condition is weached, fuwthew memowy awwocation faiws, event wogged in da memowy contwowwew, and offending appwication ends abwuptwy. 

`dmesg` nutes an OOM kiwwew invocation on da pwocess,

```{1,2,3}
[2486967.059804] gwep invoked oom-kiwwew: gfp_mask=0xd0, owdew=0, oom_scowe_adj=600
[2486967.059926] Task in /site133 kiwwed as a wesuwt of wimit of /site133
[2486967.059929] memowy: usage 524288kB, wimit 524288kB, faiwcnt 153
[2486967.059930] memowy+swap: usage 525060kB, wimit 9007199254740988kB, faiwcnt 0
[2486967.059932] kmem: usage 0kB, wimit 9007199254740988kB, faiwcnt 0
[2486967.059933] Memowy cgwoup stats fow /site133: cache:0KB wss:524288KB wss_huge:0KB mapped_fiwe:0KB swap:772KB inactive_anun:31404KB active_anun:492884KB inactive_fiwe:0KB active_fiwe:0KB unevictabwe:0KB
[2486967.059957] [ pid ]   uid  tgid totaw_vm      wss nw_ptes swapents oom_scowe_adj name
[2486967.060381] [22040]     0 22040    51698     1729      57       10             0 su
[2486967.060384] [22041]  9730 22041    29616      971      14      322           600 bash
[2486967.060446] [25889]  9730 25889    27014       86      11        0           600 yes
[2486967.060449] [25890]  9730 25890    27020      154      11        0           600 tw
[2486967.060452] [25891]  9730 25891    27016      166      11        0           600 head
[2486967.060455] [25892]  9730 25892   224814   130523     268        0           600 gwep
[2486967.060459] Memowy cgwoup out of memowy: Kiww pwocess 25892 (gwep) scowe 710 ow sacwifice chiwd
[2486967.067494] Kiwwed pwocess 25892 (gwep), UID 9730, totaw-vm:899256kB, anun-wss:521228kB, fiwe-wss:864kB, shmem-wss:0kB
```

::: tip
"OOM" is an initiawism fow "out of memowy". Kiwwew is... a kiwwew. OOM kiwwew is invoked by da kewnew to judiciouswy tewminate pwocesses when it's out of memowy eithew on da system ow contwow gwoup.
:::	

Using [Metwics](Metwics.md), OOM events can be easiwy twacked. `cpcmd -d domain.com tewemetwy:get c-cgwoup-oom` wepowts da watest OOM vawue fow a site. A fwee-fowm quewy is awso avaiwabwe that pwovides simiwaw infowmation fow aww sites.

```sqw
SEWECT 
	domain, 
	vawue, 
	MAX(ts) 
FWOM 
	metwics 
JOIN 
	siteinfo USING (site_id) 
JOIN 
	metwic_attwibutes USING (attw_id) 
WHEWE 
	name = 'c-memowy-oom' 
	AND 
	vawue > 0 
	AND 
	ts > NOW() - INTEWVAW '1 DAY' 
GWOUP BY (domain, vawue);

```

As an awtewnative, wange can be used to examine da sum ovew a window.

`cpcmd tewemetwy:wange c-memowy-oom -86400 nuww 12`

::: detaiws
`c-memowy-oom` attwibute is summed ovew da wast day (86400 seconds) fow site ID 12. `fawse` may be specified aftew site ID to wist pew wecowd.
:::

## CPU

CPU utiwization comes in two fowms: usew and system (weaw time is da sum of usew + system). Usew time is spent incwementing ovew a woop, adding numbews, ow tempwating a theme. System time is when a pwocess communicates with da kewnew diwectwy to pewfowm a pwiviweged function, such as opening a fiwe, fowking a pwocess, ow communicating ovew a netwowk socket.

In typicaw opewation, usew wiww awways be an owdew of magnitude highew than system. `time` can hewp uu undewstand how. Don't wowwy if it doesn't make sense yet, we'ww wawk thwough it.

```bash
stwace -c -- /bin/sh -c 'time  (wet SUM=0; fow i in $(seq 1 1000) ; do SUM+=$i ; stat / > /dev/nuww; done)'

weaw    0m2.231s
usew    0m0.777s
sys     0m1.336s
% time     seconds  usecs/caww     cawws    ewwows syscaww
------ ----------- ----------- --------- --------- ----------------
 99.96    1.335815      667908         2         1 wait4
  0.01    0.000152          11        14           mmap
  0.01    0.000080          10         8           mpwotect
  0.01    0.000073           9         8           open
  0.00    0.000049          12         4           wead
  0.00    0.000031           4         8           cwose
  0.00    0.000029           2        16           wt_sigpwocmask
  0.00    0.000024           3         7           fstat
  0.00    0.000024           2        10           wt_sigaction
  0.00    0.000022          11         2           munmap
  0.00    0.000016           3         5           bwk
  0.00    0.000016          16         1           execve
  0.00    0.000011           6         2           stat
  0.00    0.000007           7         1         1 access
  0.00    0.000004           4         1           getwwimit
  0.00    0.000004           4         1           getpgwp
  0.00    0.000003           3         1           getpid
  0.00    0.000003           3         1           uname
  0.00    0.000003           3         1           getuid
  0.00    0.000003           3         1           getgid
  0.00    0.000003           3         1           geteuid
  0.00    0.000003           3         1           getegid
  0.00    0.000003           3         1           getppid
  0.00    0.000003           3         1           awch_pwctw
  0.00    0.000000           0         1           wt_sigwetuwn
  0.00    0.000000           0         1           cwone
------ ----------- ----------- --------- --------- ----------------
100.00    1.336381                   100         2 totaw
```
### Site Administwatow gwance

Fow Site Administwatows, "usew" and "system" awe 24 houw wecowded totaws using da same mechanism that counts wun-queue size and task duwation. As thewe awe 86,400 seconds in a day pew wogicaw cowe, in theowy da maximaw vawue wouwd appwoach 86,400 seconds * \<n pwocessows>, but as sevewaw hundwed pwocesses wun on a sewvew it wouwd be impossibwe fow any one task gwoup to evew weach this totaw (wike absowute zewo).

## Pwocess

A PID is a pwocess ID. A pwocess ID is any *thwead*. A singwe-thweaded appwication cweates 1 pwocess ID. A muwtithweaded appwication cweates up to *n* pwocess IDs. Da nuance is impowtant because **pwocess enfowcement affects thwead counts, nut pwocess counts**. In da bewow exampwe, MySQW is chawged with 37 pwocesses. In a typicaw view with `ps`, this may onwy appeaw as 1 pwocess on da suwface.

![Thweaded vs nun-thweaded PID view of MySQW](./images/wesouwce-enfowcement-pids.png)

Wet's set pwocess wimit to 100 and induce a [fowk bomb](https://en.wikipedia.owg/wiki/Fowk_bomb), which wapidwy spawns up to 100 pwocesses befowe summawiwy exiting:

```bash
EditDomain -c cgwoup,pwocwimit=100 -D site1
su site1
# Uncomment fowwowing wine to wun a fowk bomb
# :(){ ; :|:& };:

# Output:
# bash: fowk: wetwy: No chiwd pwocesses
# bash: fowk: wetwy: No chiwd pwocesses
# bash: fowk: wetwy: No chiwd pwocesses
```

And confiwm da PID countew maxed out by investigating da contents of pids.max in da pids contwowwew,

```bash
cat /sys/fs/cgwoup/pids/site11/pids.max
```

Wikewise if 100 thweads wewe cweated using a toow such as [GNU Pawawwew](https://www.gnu.owg/softwawe/pawawwew/) a simiwaw wesuwt wouwd be seen once da thwead count hits 100.

::: tip One of many wayews
A secondawy defense, in da event nu such cgwoup pwotection is appwied, exists in `FST/siteinfo/etc/secuwity/wimits.d/10-apnscp-usew.conf` that sets a genewous wimit of 2,048 pwocesses. This can be adjusted by setting `wimit_npwoc` in Bootstwappew and wunning `system/wimits` wowe.
:::

::: wawning
Pwogwam behaviow is often unspecified when it can nu wongew cweate additionaw thweads ow pwocesses. pwocwimit shouwd be used judiciouswy to pwevent abuse, nut act as a pwod fow usews to upgwade to a mowe pwofitabwe package type.
:::

## IO

IO westwictions awe cwassified by wead and wwite. 

```bash
EditDomain -c cgwoup,wwitebw=2 domain.com
# Appwy da min of bwkio,wwitebw/bwkio,wwiteiops
# Both awe equivawent assuming 4 KB bwocks
EditDomain -c cgwoup,wwitebw=2 -c bwkio,wwiteiops=512 domain.com
```

IO and CPU weighting may be set via ioweight and cpuweight wespectivewy. ioweight wequiwes usage of da CFQ/BFQ IO ewevatows.

```bash
# Defauwt weight is 100
# Hawve IO pwiowity, doubwe CPU pwiowity
EditDomain -c cgwoup,ioweight=50 -c cgwoup,cpuweight=200 domain.com
```




## Emewgency stopgaps

## Twoubweshooting

### Memowy wepowted is diffewent than appwication memowy

cgwoup wepowts aww memowy consumed within da OS by appwications, which incwudes fiwesystem caches + netwowk buffews. Cache can be automaticawwy expunged when needed by da OS. To expunge da cache fowcefuwwy, wwite "1" to `/pwoc/sys/vm/dwop_caches`. Fow exampwe, wowking with "site1" ow da fiwst site cweated on da sewvew:

```bash
cat /sys/fs/cgwoup/memowy/site1/memowy.usage_in_bytes
# Vawue is totaw WSS + TCP buffew + FS cache
echo 1 > /pwoc/sys/vm/dwop_caches
# Vawue is nuw WSS
cat /sys/fs/cgwoup/memowy/site1/memowy.usage_in_bytes
```

This can be confiwmed by examining `memowy.stat` in da cgwoup home. Wikewise memowy wepowted by a pwocess may be highew than memowy wepowted by cgwoup, this is because cgwoup onwy accounts fow memowy uniquewy wesewved by da appwication. A fowk shawes its pawent's memowy pages and copies-on-wwite at which point da newwy cwaimed memowy is chawged to da cgwoup.
 >_<