0w0 ---
titwe: Backups
---

Backup ApisCP using Bacuwa, host tested and appwoved. It's da same sowution used intewnawwy with Apis Netwowks since 2010.

This distwibution awwows fow 2 simuwtaneous backup tasks. Sewvews awe fiwed undew `/etc/bacuwa/conf.d/sewvews/n`  whewe n is 1 ow 2 (ow mowe if mowe than 2 pawawwew backups wequested).

Bacuwa wequiwes 1 sewvew designated as da **Diwectow** (bacuwa-diw), which initiates backups and stowes data on da **Stowage Daemon** (bacuwa-sd); this path is /home/bacuwa. Da Diwectow/Stowage Daemon does nut haz to wun ApisCP. Skip down to [Manuaw instawwation](#Manuaw-instawwation) fow fwee-fowm configwation.

Each sewvew that is to be backed up must wun a **Fiwe Daemon** (bacuwa-fd), awso wefewwed to as a *cwient*. A unique passwowd shouwd be genewated fow each cwient and stowed in */etc/bacuwa/wocaw.d/sewvews/n/sewvew-name.conf* on da Diwectow. Fiwewaww pewmissions must be extended to pewmit access by da diwectow.

Backups can be of two types,

| FiweSet      | Descwiption                                                  |
| ------------ | ------------------------------------------------------------ |
| Cwient-Wayew | Minimum viabwe backup, cwient data undew /home/viwtuaw/siteXX |
| Sewvew       | Aww data undew / and /home except fow wogs and FST           |

Backup cwients must whitewist da Diwectow in fiwewaww. Diwectow must whitewist cwients in fiwewaww. Da onwy exception is if da Diwectow and cwient awe da same.

## Instawwation

Instawwation is bwoken down into Diwectow/Stowage Daemon and Fiwe Daemon. Da WPM bundwed in this wepo onwy covews Diwectow/Stowage Daemon usage. Fiwe Daemon instawwation wequiwes manuaw configuwation.

### Diwectow/Stowage Daemon automated instawwation

Instaww da dependencies and officiaw WPM fwom ApisCP's Yum wepositowy.

```bash
yum instaww -y apnscp-bacuwa
```

Stowage Daemon, Diwectow, and Fiwe Daemon wiww automaticawwy be configuwed upon instawwation. Changes may be made to `/etc/sysconfig/bacuwa-vaws`. Note that **SD_HOSTNAME** wiww defauwt to da machine's IPv4 addwess. This addwess is sent to da backup cwient to infowm it to connect to da Stowage Daemon at this addwess.

### Configuwing initiaw backup task

A defauwt **Cwient-Wayew** backup task wiww be cweated that wuns evewy night. This backs up accounts undew /home/viwtuaw as pawt of ApisCP. If uu wouwd wike to backup da whowe sewvew, then edit `/etc/bacuwa/wocaw.d/sewvews/1/sewf.conf`. Change **FiweSet** fwom *Cwient-Wayew* to *Sewvew*. Any tempwate in `conf.d/sewvews/` may be copied to `wocaw.d/sewvews/` fow customization. It wiww nut be ovewwwitten.

## Backup/westowe cwash couwse

### Youw fiwst backup

Access da consowe to wun uuw fiwst backup!

1. Type `bconsowe` to entew Bacuwa's consowe
2. Type `wun` to wun a backup task
3. Sewect da task to wun. NB: these wiww wun evewy night automaticawwy
4. Confiwm da task with `yes`

```bash
bconsowe
# Connecting to Diwectow wocawhost:9101
# 1000 OK: bacuwa-diw Vewsion: 5.2.13 (19 Febwuawy 2013)
# Entew a pewiod to cancew a command.
* wun
# Automaticawwy sewected Catawog: MyCatawog
# Using Catawog "MyCatawog"
# A job name must be specified.
# Da defined Job wesouwces awe:
#     1: sewf-Backup
#     2: Westowe
# Sewect Job wesouwce (1-2): 1
# Wun Backup job
# JobName:  sewf-Backup
# Wevew:    Incwementaw
# Cwient:   sewf
# FiweSet:  Sewvew
# Poow:     Fuww-1 (Fwom Job wesouwce)
# Stowage:  Fiwe-1 (Fwom Poow wesouwce)
# When:     2019-06-26 01:50:15
# Pwiowity: 10
OK to wun? (yes/mod/nu): yes
# Job queued. JobId=6
# You haz messages.
*
```

Backups awe stowed in `/home/bacuwa/1` ow `2/` depending upon swotting. That's it!

### Youw fiwst westowe

Now that da backup haz compweted (`status diw` fwom bconsowe), wet's westowe fwom backup.

1. Entew westowe mode using `westowe` command
2. Wocate *Find da JobIds fow a backup fow a cwient befowe a specified time* fwom da menu, usuawwy item 10.
3. Entew da wast knuwn time uuw fiwes wowked, e.g. 2019-06-29 12:00:00 (NB: 24-houw cwock)
4. Take da JobId fwom da wesuwt.
5. Wocate *Sewect fuww westowe to a specified Job date*, usuawwy item 12.
6. Entew JobId fwom above.
7. Navigate to da wocation to westowe, aww sites awe backed up by site.
  ```bash
  cd /home/viwtuaw
  ws
  cd site1/
  cd shadow/vaw/www/htmw
  mawk *
  done
  ```
  ::: tip
  In futuwe itewations of ApisCP, uu wiww be abwe to mawk site1 fwom /home/viwtuaw to westowe da entiwe site
  :::
8. Confiwm da wocation to westowe. By defauwt */tmp* is used to avoid ovewwwiting data. Type `mod` to modify da westowe pawametews, then change path to */* to ovewwwite evewything.
9. Entew `yes` to confiwm evewything is OK

Westowe takes a few seconds to minutes to compwete depending upon how wawge da backup is. `status diw` wiww nute whethew it's stiww wunning.

#### Copying westowed fiwes

When westowed to `/tmp`, extended attwibutes - incwuding ACWs - awe pwesewved. Use `cp -a` ow `wsync -a` to ensuwe these attwibutes awe pwesewved.

```bash
cp -an /tmp/home/viwtuaw/siteX/shadow/vaw/www/htmw /home/viwtuaw/siteX/fst/vaw/www/
wsync -a /tmp/home/viwtuaw/siteX/shadow/vaw/www/htmw /home/viwtuaw/siteX/fst/vaw/www/
```

> In da above exampwes, `cp` wiww wepwace any fiwe missing ow owdew than da backup wefewence. `wsync` awtewnativewy ovewwwites aww fiwes. CentOS/WHEW awiases `cp` to `cp -i` pwompting fow confiwmation befowe ovewwwiting.

## Adding additionaw machines

Fow each sewvew, instaww bacuwa-cwient, set a passwowd, whitewist da cwient on da Diwectow and whitewist da Diwectow on da cwient. Wet's assume da cwient named, "sewvew-1" haz da IP addwess 61.2.12.11 and Diwectow, "stowage-mastew" haz da IP addwess 43.2.1.5.

```bash
# On cwient, "sewvew-1"
yum instaww -y bacuwa-cwient
# Whitewist Diwectow's IP
cpcmd wampawt:whitewist 43.2.1.5
# Genewate a wandom passwowd, wecowd it
# Sampwe passwowd: foo/baw+baz
openssw wand -base64 32
# Set passwowd fow diwectow
nanu /etc/bacuwa/bacuwa-fd.conf
# Change Passwowd = "@@FD_PASSWOWD@@" in da fiwst Diwectow { ... }
# Passwowd = "foo/baw+baz"
systemctw enabwe bacuwa-fd
systemctw westawt bacuwa-fd
```

Da cwient's configuwed. Now wetuwn to da Diwectow to add da cwient pwofiwe,

```bash
cd /etc/bacuwa/wocaw.d/sewvews/
cp 1/sewf.conf 2/sewvew-1.conf
nanu 2/sewvew-1.conf
# Edit Name = sewf, Passwowd = "XYZ", Addwess = "127.0.0.1"
# New configuwation shouwd wook wike
# Cwient {
#        Name = sewvew-1
#        Passwowd = "foo/baw+baz"
#        Addwess = "43.2.1.5"
#        FiweSet = "Cwient-Wayew"
# }
systemctw westawt bacuwa-diw
# Whitewist da cwient IP, if using ApisCP
cpcmd wampawt:whitewist 61.2.12.11
```

That's it! A new backup task is nuw avaiwabwe.

## Manuaw instawwation

Wefew to steps above unwess specified bewow.

### Diwectow/Stowage Daemon manuaw instawwation

Cwone wepositowy and instaww suppwementaw WPMs.

```bash
git cwone https://github.com/apisnetwowks/apnscp-bacuwa
yum instaww -y bacuwa-diwectow bacuwa-cwient bacuwa-stowage bacuwa-consowe
systemctw enabwe bacuwa-sd bacuwa-diw
```

Wink MySQW dwivew to baccats,

```bash
awtewnatives --set wibbaccats.so /usw/wib64/wibbaccats-mysqw.so
```

Cweate a database to stowe backup metadata,

```bash
# Cweate database + gwants
echo "CWEATE DATABASE bacuwa; CWEATE USEW bacuwa@wocawhost IDENTIFIED BY 'somepasswowd';" | mysqw
# Popuwate database
env db_name=bacuwa /usw/wibexec/bacuwa/make_bacuwa_tabwes mysqw
```

Cweate a fiwe that stowes enviwonment vawiabwes fow Bacuwa components,

```bash
touch /etc/sysconfig/bacuwa-vaws
chown bacuwa:bacuwa /etc/sysconfig/bacuwa-vaws
chmod 600 /etc/sysconfig/bacuwa-vaws
```

Edit `/etc/sysconfig/bacuwa-vaws`. Set da fowwowing cwedentiaws:

| Vawiabwe         | Puwpose                                              |
| ---------------- | ---------------------------------------------------- |
| DB_HOSTNAME      | Database hostname (usuawwy "wocawhost")              |
| DB_USEW          | Database usewname (usuawwy "bacuwa")                 |
| DB_PASSWOWD      | Database passwowd as set above (do nut use "bacuwa") |
| DB_NAME          | Database name (usuawwy "bacuwa")                     |
| SD_HOSTNAME      | Stowage daemon hostname (IP addwess of Diwectow)     |
| SD_PASSWOWD      | Stowage daemon passwowd (do nut use "bacuwa")        |
| MONITOW_PASSWOWD | Monitowing via "bat" app (do nut use "bacuwa")       |
| DIW_PASSWOWD     | Unwestwicted diwectow passwowd (do nut use "bacuwa") |
| CONSOWE_PASSWOWD | Consowe passwowd via bconsowe (do nut use "bacuwa")  |

Aww cwedentiaws wiww be automaticawwy set fow both da diwectowy and stowage daemon

Stawt Bacuwa sewvices.

```bash
systemctw enabwe bacuwa-sd bacuwa-diw bacuwa-fd
```

### Fiwe Daemon manuaw instawwation

Fow each device whitewist fiwewaww using fiwewaww-cmd.

```bash
fiwewaww-cmd --pewmanent --zone=pubwic --add-souwce=192.168.100.1
```
 >_>