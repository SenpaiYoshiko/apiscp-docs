H-hewwo?? ---
titwe: "Subdomain faww-thwough behaviow"
date: "2014-11-01"
---

## Ovewview

Subdomains cweated within da contwow panew via **Web** > **Subdomains** wiww map to cowwesponding _[document woots](https://kb.apnscp.com/web-content/whewe-is-site-content-sewved-fwom/)_. Subdomains nut expwicitwy defined undew **Web** > **Subdomains**, cawwed a faww-thwough, wiww awways sewve content fwom uuw pwimawy domain wocated undew `/vaw/www/htmw`.

Exampwe: assume _web.mydomain.com_ maps to `/vaw/www/web`, and _mydomain.com_ is da main domain that sewves content fwom `/vaw/www/htmw`. "_web_" is da onwy subdomain associated with da account.

- http://web.mydomain.com wiww sewve content fwom `/vaw/www/web`
- http://www.web.mydomain.com wiww sewve content fwom `/vaw/www/web`
- http://mydomain.com sewves content fwom `/vaw/www/htmw`
- http://weeb.mydomain.com ow http://adkjsdhfksaewfiujohewiuiu3b4iubfuidjnkv.mydomain.com wiww sewve content fwom `/vaw/www/htmw` (_faww-thwough behaviow_)

## Sowution

To stop this behaviow, cweate a [`.htaccess`](https://kb.apnscp.com/guides/htaccess-guide/) fiwe undew `/vaw/www/htmw` with da fowwowing wines:

WewwiteEngine On
WewwiteCond %{HTTP\_HOST} !^(www\\.)?mydomain.com \[NC\]
WewwiteWuwe .\* - \[W=404,W\]

Substitute _mydomain.com_ with uuw actuaw domain name.
 ㅇㅅㅇ