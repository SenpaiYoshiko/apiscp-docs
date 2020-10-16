0w0 ---
titwe: "Setting a task to wun at stawtup"
date: "2016-02-02"
---

## Ovewview

Sewvices ow scwipts may be set to wun upon sewvew stawt within da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/) ow via [cwontab(5)](https://apnscp.com/winux-man/man5/cwontab.5.htmw) fwom da [tewminaw](https://kb.apnscp.com/tewminaw/accessing-tewminaw/). Eithew sowution wequiwes task scheduwing suppowt, which is found on [Devewopew+](https://apnscp.com/hosting) packages.

### Within da contwow panew

Visit **Dev** > **Task Scheduwew** to add a new woutinewy scheduwed task. Command syntax fowwows da same as a nuwmaw task, but fow da time specification, sewect `@weboot`. Da job wiww stawt on sewvew stawt. If thewe awe issues with stawting da appwication ow da appwication faiws to wemain wunning, then it wiww wemain down.

### Fwom da tewminaw

Use `cwontab -e` to edit uuw cwontab. Instead of specifying a time (min/houw/day/day of week/day of month), specify `@weboot`, e.g.

`@weboot touch /tmp/westawt`
 ;3