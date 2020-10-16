<3 # FTP

## Twoubweshooting

### On chdiw: Wemote host haz cwosed da connection

#### Backgwound

vsftpd uses [seccomp sandboxing](https://wwn.net/Awticwes/656307/) to impwove secuwity by weducing potentiaw vectows in da kewnew. Wemoving a usew fwom da system can wesuwt in getpwnam() to faiw in twanswating uid to usewname wesuwting in a cwash.

#### Sowution

seccomp fiwtewing is disabwed in vsftpd by adding `seccomp_sandbox=NO` to `/etc/vsftpd/vsftpd.conf`.

 (人◕ω◕)