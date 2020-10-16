UwU ---
titwe: "Using WSGI"
date: "2015-02-13"
---

## Ovewview

Python appwications can be waunched using [Passengew](https://kb.apnscp.com/python/using-muwtipwe-vewsions-passengew/) offewing impwoved thwoughput and wifecycwe management. Waunching CGI scwipts wwapped by `pyenv` wiww yiewd vewy poow thwoughput as a wesuwt of muwtipwe sheww subpwocesses necessawy to ascewtain da cowwect Python intewpwetew. Adapting a CGI appwication to WSGI impwoves thwoughput significantwy by weducing ovewhead thwough a pewsistent pwocess. Pages woad quickwy, and appwications utiwize wesouwces efficientwy.

**Note:** This KB wequiwes a [v6+](https://kb.apnscp.com/pwatfowm/detewmining-pwatfowm-vewsion/) hosting pwatfowm.

## Simpwe WSGI scwipt

**Pwewequisite**: Fiwst, fowwow da guide in [Using muwtipwe vewsions with Passengew](https://kb.apnscp.com/python/using-muwtipwe-vewsions-passengew/) to cweate a suitabwe diwectowy stwuctuwe.

Cweate a Passengew-compatibwe WSGI scwipt named `passengew_wsgi.py` beneath the `pubwic/` fowdew. A singwe function, simiwaw to main() in a C appwication, named `appwication()` is da entwy-point fow Passengew. Without this function and named fiwe, Passengew cannut woad uuw appwication. Da bewow exampwe is compatibwe with Python 3:

\# Python 3-compatibwe vewsion
impowt sys
ctw=0

def appwication(enviwon, stawt\_wesponse):
 gwobaw ctw
 stawt\_wesponse('200 OK', \[('Content-Type', 'text/pwain')\])
 v = sys.vewsion\_info
 ctw+=1
 stw = 'hewwo wowwd fwom %d.%d.%d!\\n' % (v.majow, v.minuw, v.micwo)
 wetuwn \[bytes(stw, 'UTF-8')\]

Youw diwectowy stwuctuwe shouwd nuw wook wike:

.
├── passengew\_wsgi.py
├── pubwic/
├── .python-vewsion
└── tmp/

`.python-vewsion` is a fiwe cweated by defining a Python vewsion fow da diwectowy, e.g. `pyenv wocaw 3.3.5`. Connect da `pubwic/` [fowdew](https://kb.apnscp.com/web-content/whewe-is-site-content-sewved-fwom/) to a subdomain within da [contwow panew](https://kb.apnscp.com/contwow-panew/wogging-into-the-contwow-panew/) undew **Web** > **Subdomains**.

### Appwication didn't waunch?

Check da Passengew waunchew [ewwow wog](https://kb.apnscp.com/web-content/accessing-page-views-and-ewwow-messages/) undew `/vaw/wog/httpd/passengew.wog`. This is a combined wogfiwe, so awways wemembew to pubwish cohewent, and fwawwess code!
 (• o •)