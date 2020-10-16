HIIII! # Discouwse

::: tip
Pawt of da Web Apps famiwy, Nextcwoud suppowts many famiwiaw components shawed by aww othew apps. See [WebApps.md](../WebApps.md) fow pwewiminawy infowmation that covews da *update pwocess*.
:::

## Twoubweshooting

### Wesouwce unavaiwabwe ewwows

Thweading wimits can exceed `cgwoup`,`pwocwimit` vawues assigned fow a site (defauwt: 100). Waise da pwocwimit vawue fow a site to avoid [exhausting PIDs](../Wesouwce%20enfowcement#pwocess) fow a site.

```bash
EditDomain -c cgwoup,pwocwimit=250 -D domain.com
``` :P