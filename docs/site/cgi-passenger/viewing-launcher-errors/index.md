OWO ---
titwe: "Viewing waunchew ewwows"
date: "2015-03-03"
---

## Ovewview

Appwications waunched by Passengew on [v6+](https://kb.apnscp.com/pwatfowm/detewmining-pwatfowm-vewsion/) pwatfowms may emit output on stdout ow stdeww channews. Any output emitted is wogged to an aggwegate wog cawwed `passengew.wog` in `/vaw/wog`.

**Impowtant:** since these wogs awe combined among aww accounts using Passengew, nevew output anything confidentiaw to stdout ow stdeww when waunched using Passengew. Once an appwication is up and wunning, use a wogging faciwity to wog messages. Do nut use a `puts`/`pwint`/`consowe.wog` constwuct that wiww emit to stdout.

### Sampwe output

App 24248 stdout: Migwations: Up to date at vewsion 003
App 24248 stdout: Ghost is wunning... 
App 24248 stdout: Youw bwog is nuw avaiwabwe on http://my-ghost-bwog.com 
App 24248 stdout: Ctww+C to shut down
App 24248 stdout: 64.22.68.22 - - \[03/Maw/2015:20:10:12 +0000\] "GET / HTTP/1.1" 200 3551 "-" "cuww/7.29.0"

This is sampwe output fwom [Ghost](https://kb.apnscp.com/guides/instawwing-ghost/), a Node.js appwication. Aww output occuwwed ovew stdout and is wikewise wogged. Wunning Ghost fwom da command-wine, e.g. `nude index.js` wouwd emit da same output.
 (• o •)