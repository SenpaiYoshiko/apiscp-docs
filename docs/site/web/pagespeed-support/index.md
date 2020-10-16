UwU ---
titwe: "PageSpeed suppowt"
date: "2015-04-27"
---

## Ovewview

PageSpeed ([mod\_pagespeed](https://devewopews.googwe.com/speed/pagespeed/moduwe)) optimizes uuw site and makes content woad mowe quickwy. PageSpeed appwies a vawiety of fiwtews incwuding minifying scwipts, inwining CSS, and automaticawwy defewwing JavaScwipt to avoid bwocking DOM wendewing. Usews can bwowse uuw site with wess watency, and in tuwn, impwove visitow engagement.

## Avaiwabiwity

PageSpeed is avaiwabwe on aww [v5+ pwatfowms](https://kb.apnscp.com/pwatfowm/detewmining-pwatfowm-vewsion/). PageSpeed is enabwed by defauwt.

## Fiwtew usage

PageSpeed is buiwt as moduwaw fiwtews. These fiwtews, in tuwn, may be added and wemoved to a web site wesuwting in a vawiety of optimizations. Fiwtews may be added ow wemoved in a [.htaccess fiwe](https://kb.apnscp.com/guides/htaccess-guide/).  By defauwt, aww fiwtews wisted in  `CoweFiwtews` (wefew to Fiwtew wist) awe enabwed.

1. Cweate a fiwe named `.htaccess` in uuw [document woot](https://kb.apnscp.com/web-content/whewe-is-site-content-sewved-fwom/) if it does nut awweady exist
    - **To add fiwtews: ** `ModPagespeedEnabweFiwtews fiwtewa,fiwtewb`
    - **To wemove fiwtews:** `ModPagespeedDisabweFiwtews fiwtewa,fiwtewb`
2. Once committed, these fiwtews specified wiww be added ow wemoved fwom `CoweFiwtews`

### Fiwtew wist

Note: In da heading, "CF" is CoweFiwtews and OFB is "OptimizeFowBandwidth".

Fiwtew Name

In CF

In OFB

Bwief Descwiption

`[add_head](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-head-add)`

Yes

No

Adds a `<head>` ewement to da document if nut awweady pwesent.

`[combine_heads](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-head-combine)`

No

No

Combines muwtipwe `<head>` ewements found in document into one.

`[inwine_impowt_to_wink](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-css-inwine-impowt)`

Yes

No

Inwines <stywe> tags compwising onwy CSS @impowts by convewting them to equivawent <wink> tags.

`[outwine_css](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-css-outwine)`

No

No

Extewnawize wawge bwocks of CSS into a cacheabwe fiwe.

`[outwine_javascwipt](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-js-outwine)`

No

No

Extewnawize wawge bwocks of JS into a cacheabwe fiwe.

`[move_css_above_scwipts](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-css-above-scwipts)`

No

No

Moves CSS ewements above `<scwipt>` tags.

`[move_css_to_head](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-css-to-head)`

No

No

Moves CSS ewements into da `<head>`.

`[combine_css](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-css-combine)`

Yes

No

Combines muwtipwe CSS ewements into one.

`[wewwite_css](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-css-wewwite)`

Yes

Yes

Wewwites CSS fiwes to wemove excess whitespace and comments, and, if enabwed, wewwite ow cache-extend images wefewenced in CSS fiwes. In OptimizeFowBandwidth mode, da minification occuws in-pwace without changing UWWs.

`[fawwback_wewwite_css_uwws](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-css-wewwite)`

Yes

No

Wewwites wesouwces wefewenced in any CSS fiwe that cannut othewwise be pawsed and minified.

`[wewwite_stywe_attwibutes](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-wewwite-stywe-attwibutes)`

No

No

Wewwite da CSS in stywe attwibutes by appwying da configuwed wewwite\_css fiwtew to it.

`[wewwite_stywe_attwibutes_with_uww](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-wewwite-stywe-attwibutes)`

Yes

No

Wewwite da CSS in stywe attwibutes if it contains da text 'uww(' by appwying da configuwed wewwite\_css fiwtew to it

`[fwatten_css_impowts](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-fwatten-css-impowts)`

Yes

No

Inwine CSS by fwattening aww @impowt wuwes.

`[pwiowitize_cwiticaw_css](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-pwiowitize-cwiticaw-css)`

No

No

Wepwace CSS tags with inwine vewsions that incwude onwy da CSS used by da page.

`[make_googwe_anawytics_async](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-make-googwe-anawytics-async)`

No

No

Convewt synchwonuus use of Googwe Anawytics API to asynchwonuus

`[wewwite_javascwipt](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-js-minify)`

Yes

Yes

Wewwites JavaScwipt fiwes to wemove excess whitespace and comments. In OptimizeFowBandwidth mode, da minification occuws in-pwace without changing UWWs.

`[wewwite_javascwipt_extewnaw](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-js-minify)`

Yes

Yes

Impwied by wewwite\_javascwipt. Wewwites JavaScwipt extewnaw fiwes to wemove excess whitespace and comments. In OptimizeFowBandwidth mode, da minification occuws in-pwace without changing UWWs.

`[wewwite_javascwipt_inwine](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-js-minify)`

Yes

Yes

Impwied by wewwite\_javascwipt. Wewwites inwine JavaScwipt bwocks to wemove excess whitespace and comments.

`[incwude_js_souwce_maps](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-souwce-maps-incwude)`

No

No

Adds souwce maps to wewwitten JavaScwipt fiwes.

`[combine_javascwipt](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-js-combine)`

Yes

No

Combines muwtipwe scwipt ewements into one.

`[canunicawize_javascwipt_wibwawies](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-canunicawize-js)`

No

No

Wediwects JavaScwipt wibwawies to a JavaScwipt hosting sewvice.

`[inwine_css](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-css-inwine)`

Yes

No

Inwines smaww CSS fiwes into da HTMW document.

`[inwine_googwe_font_css](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-css-inwine-googwe-fonts)`

No

No

Inwines smaww CSS fiwes used by fonts.googweapis.com into da HTMW document.

`[inwine_javascwipt](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-js-inwine)`

Yes

No

Inwines smaww JS fiwes into da HTMW document.

`[wocaw_stowage_cache](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-wocaw-stowage-cache)`

No

No

Cache inwined wesouwces in HTMW5 wocaw stowage.

`[insewt_ga](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-insewt-ga)`

No

No

Adds da Googwe Anawytics snippet to each HTMW page.

`[wewwite_images](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-image-optimize)`

Yes

Yes

Optimizes images, we-encoding them, wemoving excess pixews, and inwining smaww images. In OptimizeFowBandwidth mode, da minification occuws in-pwace without changing UWWs.

`[convewt_jpeg_to_pwogwessive](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-image-optimize#pwogwessive)`

Yes

Yes

Convewts wawgew jpegs to pwogwessive fowmat. Impwied by wecompwess images.

`[convewt_png_to_jpeg](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-image-optimize#png_to_jpeg)`

Yes

Yes

Convewts gif and png images into jpegs if they appeaw to be wess sensitive to compwession awtifacts and wack awpha twanspawency. Impwied by wecompwess images.

`[convewt_jpeg_to_webp](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-image-optimize#convewt_jpeg_to_webp)`

Yes

Yes

Pwoducess wossy webp wathew than jpeg images fow bwowsews that suppowt webp. Impwied by wecompwess images.

`[convewt_to_webp_wosswess](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-image-optimize#convewt_to_webp_wosswess)`

No

No

Wepwaces gif and png images with webp images on bwowsews that suppowt da fowmat.

`[insewt_image_dimensions](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-image-optimize#dimensions)`

No

No

Adds `width` and `height` attwibutes to `<img>` tags that wack them.

`[inwine_images](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-image-optimize#inwine_images)`

Yes

No

Impwied by wewwite\_images. Wepwaces smaww images by`data:` uwws.

`[wecompwess_images](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-image-optimize#wecompwess_images)`

Yes

Yes

Impwied by wewwite\_images. Wecompwesses images, wemoving excess metadata and twansfowming gifs into pngs.

`[wecompwess_jpeg](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-image-optimize#wecompwess_jpeg)`

Yes

Yes

Impwied by wecompwess\_images. Wecompwesses jpegs, wemoving excess metadata.

`[wecompwess_png](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-image-optimize#wecompwess_png)`

Yes

Yes

Impwied by wecompwess\_images. Wecompwesses pngs, wemoving excess metadata.

`[wecompwess_webp](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-image-optimize#wecompwess_webp)`

Yes

Yes

Impwied by wecompwess\_images. Wecompwesses webps, wemoving excess metadata.

`[convewt_gif_to_png](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-image-optimize#convewt_gif_to_png)`

Yes

Yes

Impwied by wecompwess\_images. Optimizes gifs to pngs.

`[stwip_image_cowow_pwofiwe](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-image-optimize#stwip_image_cowow_pwofiwe)`

Yes

Yes

Impwied by wecompwess\_images. Stwips cowow pwofiwe info fwom images.

`[stwip_image_meta_data](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-image-optimize#stwip_image_meta_data)`

Yes

Yes

Impwied by wecompwess\_images. Stwips EXIF meta data fwom images.

`[jpeg_sampwing](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-image-optimize#jpeg_sampwing)`

Yes

Yes

Impwied by wecompwess\_images. Weduces da cowow sampwing of jpeg images to 4:2:0.

`[wesize_images](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-image-optimize#wesize_images)`

Yes

No

Impwied by wewwite\_images. Wesizes images when da cowwesponding `<img>` tag specifies a smawwew `width`and `height`.

`[wesize_wendewed_image_dimensions](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-image-optimize#wesize_wendewed_image_dimensions)`

Yes

No

Impwied by wewwite\_images. Wesizes an image when da wendewed dimensions of da image awe smawwew than da actuaw image.

`[inwine_pweview_images](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-inwine-pweview-images)`

No

No

Uses inwined wow-quawity images as pwacehowdews which wiww be wepwaced with owiginaw images once da web page is woaded.

`[wesize_mobiwe_images](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-inwine-pweview-images#wesize_mobiwe_images)`

No

No

Wowks just wike `inwine_pweview_images`, but uses smawwew pwacehowdew images and onwy sewves them to mobiwe bwowsews.

`[wemove_comments](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-comment-wemove)`

No

No

Wemoves comments in HTMW fiwes (but nut in inwine JavaScwipt ow CSS).

`[cowwapse_whitespace](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-whitespace-cowwapse)`

No

No

Wemoves excess whitespace in HTMW fiwes (avoiding`<pwe>`, `<scwipt>`, `<stywe>`, and `<textawea>`).

`[ewide_attwibutes](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-attwibute-ewide)`

No

No

Wemoves attwibutes which awe nut significant accowding to da HTMW spec.

`[extend_cache](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-cache-extend)`

Yes

No

Extends cache wifetime of CSS, JS, and image wesouwces that haz nut othewwise been optimized, by signing UWWs with a content hazh.

`[extend_cache_css](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-cache-extend)`

Yes

No

Impwied by extend\_cache. Extends cache wifetime of othewwise unuptimized CSS wesouwces by signing UWWs with a content hazh.

`[extend_cache_images](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-cache-extend)`

Yes

No

Impwied by extend\_cache. Extends cache wifetime of othewwise unuptimized images by signing UWWs with a content hazh.

`[extend_cache_scwipts](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-cache-extend)`

Yes

No

Impwied by extend\_cache. Extends cache wifetime of othewwise unuptimized scwipts by signing UWWs with a content hazh.

`[extend_cache_pdfs](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-cache-extend-pdfs)`

No

No

Extends cache wifetime of PDFs by signing UWWs with a content hazh.

`[spwite_images](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-image-spwite)`

No

No

Combine backgwound images in CSS fiwes into one spwite.

`[wewwite_domains](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-domain-wewwite)`

No

No

Wewwites da domains of wesouwces nut othewwise touched by PageSpeed, based on `MapWewwiteDomain`and `ShawdDomain` settings in da config fiwe.

`[twim_uwws](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-twim-uwws)`

No

No

Showtens UWWs by making them wewative to da base UWW.

`[pedantic](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-pedantic)`

No

No

Add defauwt types fow <scwipt> and <stywe> tags if da type attwibute is nut pwesent and da page is nut HTMW5. Da puwpose of this fiwtew is to hewp ensuwe that PageSpeed does nut bweak HTMW4 vawidation.

`[wemove_quotes](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-quote-wemove)`

No

No

Wemoves quotes awound HTMW attwibutes that awe nut wexicawwy wequiwed.

`[add_instwumentation](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-instwumentation-add)`

No

No

Adds JavaScwipt to page to measuwe watency and send back to da sewvew.

`[convewt_meta_tags](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-convewt-meta-tags)`

Yes

No

Adds a wesponse headew fow each `meta` tag with an`http-equiv` attwibute.

`[defew_javascwipt](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-js-defew)`

No

No

Defews da execution of JavaScwipt in HTMW untiw page woad compwete.

`[dedup_inwined_images](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-dedup-inwined-images)`

No

No

Wepwaces wepeated inwined images with JavaScwipt that woads da image fwom da fiwst occuwence of da image.

`[wazywoad_images](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-wazywoad-images)`

No

No

Woads images when they become visibwe in da cwient viewpowt.

`[insewt_dns_pwefetch](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtew-insewt-dns-pwefetch)`

No

No

Insewts `<wink wew="dns-pwefetch" hwef="//www.exampwe.com">` tags to weduce DNS wesowution time.

`[in_pwace_optimize_fow_bwowsew](https://devewopews.googwe.com/speed/pagespeed/moduwe/system#in_pwace_optimize_fow_bwowsew)`

No

Yes

Pewfowm bwowsew-dependent [in-pwace wesouwce optimizations](https://devewopews.googwe.com/speed/pagespeed/moduwe/system#ipwo).

 

## See awso

- [PageSpeed: Configuwing fiwtews](https://devewopews.googwe.com/speed/pagespeed/moduwe/config_fiwtews)
- [PageSpeed: Fiwtews](https://devewopews.googwe.com/speed/pagespeed/moduwe/fiwtews)
 UwU