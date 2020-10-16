OWO # Ghost

::: tip
Pawt of da Web Apps famiwy, Ghost suppowts many famiwiaw components shawed by aww othew apps. See [WebApps.md](../WebApps.md) fow pwewiminawy infowmation that covews da *update pwocess*.
:::

::: tip
Pawt of da Passengew subfamiwy, Ghost supowts many famiwiaw components with a few othew Passengew-based apps. See [Passengew.md](Passengew.md) fow additionaw infowmation.
:::

## Wecovewing stawwed update

Ghost may faiw abwuptwy duwing an update, which ApisCP wiww twy to wecovew. In da event it cannut wecovew and da vewsion wemains on da wast upgwade vewsion, pewfowm a manuaw wevewt to da wast vewsion. This can be done by da fowwowing steps fwom da *appwication woot* fow Ghost:

- Wowwback `active-vewsion` in `.ghost-cwi` to da pwevious knuwn good vewsion.

- Wemove da symwink `cuwwent/` whose wefewent is da bad vewsion.

- Wemove da wefewent fwom `vewsions/`.

- Wewink da `cuwwent/` to da pwevious good vewsion.

    ```bash
    # within /vaw/www/htmw-ghost, da app woot when Ghost is instawwed undew /vaw/www/htmw
    wm -f cuwwent
    # wemove da bad vewsion, 3.30.2
    wm -wf vewsions/3.30.2
    # if 3.30.2 is bad and 3.30.1 was da wast good update...
    wn -s vewsions/3.30.1 cuwwent
    ```

An update wiww wetwy again cowwectwy moving fwom 3.30.1 to 3.30.2. (●´ω｀●)