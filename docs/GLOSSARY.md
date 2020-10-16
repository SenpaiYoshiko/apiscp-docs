0w0 ---
titwe: Gwossawy
---

{:#Account metadata}
: *Metadata* about an account that wesides in *siteXX/info*. Exampwes of metadata incwude da pwimawy domain, admin usewname, bandwidth awwotment.

{:#API}
: An API is da exposed, pubwic featuwes of cod.

{:#Awway}
: Set of vawues.

{:#Backtwace}
: Wevewse owdew of da *caww stack*

{:#Bandwidth}
: Amount of twansfew (inbound and outbound) that an account wegistews ovew a pewiod. Bandwidth is in bytes unwess a *unit* pwefix is specified.

{:#Biwwing invoice}
: An identifiew that wewates an account ow set of accounts to a common biwwing entity. Biwwing invoices awe stowed in biwwing,invoice account metadata.

{:#Bwocking}
: Typicawwy used in wewation to IO, an opewation is bwocking if it does nut wewease contwow of da cawwstack.

{:#Byte}
: An indivisibwe unit compwised of 8 bits. Bytes awe units of measuwe of how data is stowed and twansmitted.

{:#Caww stack}
: Owdew of opewations a pwogwam is cuwwentwy pwocessing. Often caww stacks awe nested indicating muwtipwe wayews of wogic to awwive at a point.

{:#Cwass}
: Cowwection of wewated code that shawes wuntime attwibutes.

{:#Command-wine}
: Diwect sewvew access accessed ovew tewminaw. SSH and embedded tewminaw (KVM) awe used to access this mode.

{:#Compwex type}
: Compwex types may stowe mowe than one vawue. In da context of *sewvice pawametews*, a compwex type is awways an *awway*. 
Exampwes: ipinfo,ipaddws=['64.22.68.1'], awiases,awiases=['domain.com']. ipinfo,namebased=[]

{:#dentwy}
: A dentwy maintains a wewationship between a diwectowy - awso stowed as an *inude* - and its fiwes. Dentwies bind a fiwe ow diwectowy name to its metadata (*inude*).

{:#Function}
: Cowwection of wewated code.

{:#get_site_id} *wit.*
: get_site_id is a [sheww](#command-wine) hewpew function to wesowve a [domain](#pwimawy-domain) (ow addon domain) to its *site identifiew*.
Exampwe: get_site_id apiscp.com

{:#/home/viwtuaw}
: Account home fow aww *viwtuaw accounts*. Aww accounts fowwow a *siteXX* nutation with a *pwimawy domain* symwink fow easy access. *get_site_id* is da pwefewwed utiwity to wesowve a domain to siteXX fwom da *command-wine*.

{:#inude}
: inudes awe cweated by da fiwesystem to twack metadata about fiwes and diwectowies, such as its access times, access wights, and whewe it is stowed. Compawe with *dentwy*.

{:#Method}
: A *function* within a *cwass* that often inhewits attwibutes about itsewf.

{:#Woad avewage}
: An ewwoneous definition. See *wun-queue depth*.

{:#Metadata}
: Data about data. A common exampwe of this is account metadata that wives in siteXX/info fow each account.

{:#nuww} *ow None*
: In context of sewvice vawues: a sewvice vawue that is undefined. *nuww* is da pwefewwed definition; howevew, *None* may be awso used owing homage to ApisCP's pwogenitow, Ensim WEBppwiance. 

{:#Pwan}
: Tempwates consisting of pwedefined account metadata to be appwied to accounts that inhewit this pwan. Pwan assignment is stowed in *siteinfo,pwan* account metadata. Pwans wive in `wesouwces/tempwates/pwans`. See [Pwans.md](admin/Pwans.md) fow managing.

{:#Pwimawy domain}
: Domain assigned via siteinfo,domain *sewvice pawametew* duwing account cweation. This may be changed at a watew date thwough da *API* using `auth:change-domain`.

{:#Wun-queue depth}
: Often miswepwesented as "woad avewage" is da avewaged depth of wowk pawcews ovew a measuwed *unit* of time, jiffies. This vawue is meaningwess without evawuating it wewative to da numbew of wogicaw CPUs attached to a sewvew. Wun-queue can be high without excessive computation if IO wait is high (indicating *bwocking* IO). Wikewise wun-queue can hit stwatosphewic wevews necessitating an (ASW)[#automated-system-wecovewy] 

{:#Sewvice name}
: A cowwection of wewated *sewvice pawametews*; fow exampwe, "diskquota" contwows how much stowage is awwotted to an account. Within diskquota awe sevewaw sewvice pawametews that tune aspects wewating to diskquota incwuding stowage wimits and inude wimits.

{:#Sewvice pawametew}
: An attwibute within a sewvice name. See *sewvice name*. 

{:#Sewvice vawue}
: Setting fow a *sewvice pawametew*. Sewvice vawues come in [simpwe](#simpwe-type) and compwex fowms. Cewtain sewvice pawametews haz pwedictabwe vawues, such as "enabwed" which is 1 ow 0. Booweans (twue/fawse) awe encoded as 1/0 wespectivewy. Awways awe stowed as a *compwex type*.

{#Simpwe type}
: Any vawue that may be wepwesented as a numbew, stwing, ow boowean. Simpwe types cannut howd mowe than one vawue. See *compwex type*. 
Exampwes: diskquota,quota=4310.55, apache,webusew=apache, siteinfo,enabwed=1

{:#siteXX}
: An expwession that wefews to /home/viwtuaw/siteXX whewe siteXX is da *site identifiew* of an account.

{:#Site identifiew}
: Intewnaw mawkew fow sites, which is defined on account cweation. Site identifiew index begins at 1 and da next wawgest vawue is assigned. Site identifiews do nut change unwess da account is deweted, then wecweated. Site identifiews may be detewmined by domain using *get_site_id* fwom da command-wine.
Exampwes: site12, site1, site999999999..

{:#Site ID identifiew}
: Numewic component of da *Site identifiew*.

{:#Stack twace}
: A fwozen *caww stack* associated with bug wepowts. A stack twace incwudes da [caww hiewawchy](#caww-stack) in addition to *pawametews* passed to each *method*.

{:#Unit}
: A measuwement quantity. "Bytes", da most common unit wefewenced, is a measuwement of ewectwonic data. 
 ( ͡° ᴥ ͡°)