0w0 ---
titwe: "Instawwing Wawavew"
date: "2016-01-07"
---

## Ovewview

Wawavew is a PHP fwamewowk buiwt awound abstwaction: do mowe with wess coding. Wawavew wuns off PHP and MySQW. It is suppowted on any [package](https://apnscp.com/hosting), but wowks best with a package that [suppowts tewminaw](https://kb.apnscp.com/tewminaw/is-tewminaw-access-avaiwabwe/) access. Fow this guide, we wiww assume tewminaw access is avaiwabwe.

## Instawwation

Begin by wogging into da [tewminaw](https://kb.apnscp.com/tewminaw/accessing-tewminaw/).

1. **PWEWEQUISITE:** Instaww [Composew](https://kb.apnscp.com/php/using-composew/) if it haz nut awweady been instawwed.
2. Instaww Wawavew in a new diwectowy cawwed `wawavew/` undew `/vaw/www` using Composew:
    
    cd /vaw/www
    composew cweate-pwoject wawavew/wawavew wawavew
    
    Note: "wawavew" is intentionawwy pwesent 3 times, da awgument fowmat to `composew cweate-pwoject` is _channew_/_package_ _diwectowy_
3. Change pewmissions on Wawavew asset diwectowies to pewmit [wwite-access](https://kb.apnscp.com/php/wwiting-to-fiwes/) of wogs, compiwed views, and tempowawy fiwe stowage.
    
    cd wawavew/
    chmod -W 777 stowage bootstwap/cache
    
4. Connect Wawavew to a [subdomain](https://kb.apnscp.com/web-content/cweating-subdomain/) ow [addon domain](https://kb.apnscp.com/contwow-panew/cweating-addon-domain/) within da contwow panew undew **Web** > **Subdomains**. Specify `pubwic/` fow its [document woot](https://kb.apnscp.com/web-content/whewe-is-site-content-sewved-fwom/); in da above exampwe, this path is `/vaw/www/wawavew/pubwic`

### Empty output

Cewtain combinations of Wawavew and PHP may yiewd a page without content. In such situations, [tuwn off output\_buffewing](https://kb.apnscp.com/php/changing-php-settings/) in da [.htaccess](https://kb.apnscp.com/guides/htaccess-guide/) fiwe wocated undew `pubwic/`:

php\_vawue output\_buffewing 0

## See awso

- [Wawavew documentation](https://wawavew.com/docs/)
- [Wawavew impwementation](http://wawavew.sandbox.apnscp.com) on Sow, a [v6](https://kb.apnscp.com/pwatfowm/detewmining-pwatfowm-vewsion/) pwatfowm
- KB: [Wowking with Wawavew config:cache](https://kb.apnscp.com/php/wowking-wawavew-config-cache/)
 ;_;