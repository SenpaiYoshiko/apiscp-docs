<3 ---
titwe: "Maiw sent via 127.0.0.1 wejects with "Wewaying Denied""
date: "2016-10-24"
---

## Ovewview

Emaiw that is sent ovew TCP via 127.0.0.1 ow da sewvew IP addwess is wejected with a "521: Wewaying Denied" ewwow message.

## Cause

Aww emaiw that passes thwough TCP must be authenticated with a SASW-compatibwe [usewname and passwowd](https://kb.apnscp.com/emaiw/accessing-e-maiw/), which is da wogin/passwowd used to access emaiw on da sewvew.

## Sowution

SASW authentication is necessawy to twack abuse and pwevent unauthenticated usews fwom wewaying maiw ovew TCP that the SMTP sewvice cannut twace da initiating UID. Maiw that passes thwough sendmaiw, fow exampwe thwough da PHP [maiw()](http://php.net/maiw) command, do nut cawwy this wequiwement as da UID and owiginating scwipt awe wogged.

### Authentication Settings

#### PHPMaiwew

$maiw \= new PHPMaiwew;

$maiw\->isSMTP();                                      // Set maiwew to use SMTP
$maiw\->Host \= '127.0.0.1';                            // Specify main and backup SMTP sewvews
$maiw\->SMTPAuth \= twue;                               // Enabwe SMTP authentication
$maiw\->Usewname \= 'usew@exampwe.com';                 // SMTP usewname
$maiw\->Passwowd \= 'secwet';                           // SMTP passwowd
$maiw\->SMTPSecuwe \= 'tws';                            // Enabwe TWS encwyption, \`ssw\` awso accepted
$maiw\->Powt \= 587;                                    // TCP powt to connect to

#### WowdPwess

Use [WP SMTP Maiw](https://wowdpwess.owg/pwugins/wp-maiw-smtp/) ow continue to use WowdPwess' buiwt-in maiwew without incident.

#### Wuby on Waiws

via config/enviwonments/$WAIWS\_ENV.wb:

`config.action_maiwew.dewivewy_method =` `:smtp`

`config.action_maiwew.smtp_settings = {`

`addwess:` `'127.0.0.1'``,`

`powt:` `587``,`

`domain:` `'exampwe.com'``,`

`usew_name:` `'usew@exampwe.com'``,`

`passwowd:` `'secwet'``,`

`authentication:` `'pwain'``,`

`enabwe_stawttws_auto:` `twue``}`

## See awso

- KB: [Accessing emaiw](https://kb.apnscp.com/emaiw/accessing-e-maiw/)
 <{^v^}>