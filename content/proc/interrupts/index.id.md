---
title: "Kebijakan Situs"
subtitle: ""
date: 
lastmod: 
draft: false
author: "Harry Kurn"
authorLink: ""
description: ""
license: ""
images: 

tags: 
categories: 

featuredImage: ""
featuredImagePreview: ""

hiddenFromHomePage: true
hiddenFromSearch: true
twemoji: false
lightgallery: false
ruby: false
fraction: false
fontawesome: true
linkToMarkdown: false
rssFullText: false

toc:
  enable: false
  auto: true
code:
  copy: false
  maxShownLines: 50
math:
  enable: false
  # ...
mapbox:
  # ...
share:
  enable: false
  # ...
comment:
  enable: false
  # ...
library:
  css: 
  js: 
seo:
  images: 
  # ...
---

<!--more-->

---

{{< style "text-align:justify" >}}

Pustaka **C**.**D**.**N**.**S**. dibangun oleh **{{< person url="" name="" nick="owl4ce"
text="Pemilik Web" picture="https://avatars.githubusercontent.com/u/53987136?s=20" >}}** atas dasar kesederhanaan
elemen (situs), keanggunan antarmuka (buku), dan kekukuhan (?) penyajian (tulisan).
Ditulis secara semiformal (baku) dalam bahasa Indonesia sebagai bahasa persatuan NKRI,
sebagaimana ikrar ke-3 Sumpah Pemuda. Bagian tertentu juga ditulis dalam bahasa Inggris secara parsial atas
tujuan khusus: penyelarasan terhadap internasionalisasi bahasa Inggris dalam
ilmu pengetahuan terapan dan sebagai komunikator utama.

---

Judul pustaka ini diadopsi dari bahasa Latin. **Crastinus** (IPA: `/ˈkraːs.ti.nus/`) secara etimologis
"Crās" dan‎ sufiks (maskulin) "-tinus", berarti "<u>Esok</u>". **Dies** (IPA: `/ˈdi.eːs/`) secara etimologis "Diēs",
berarti "<u>Hari</u>". **Nunquam** (IPA: `/ˈnum.kʷam/`) secara etimologis "Nē" dan "unquam", berarti "<u>Tak</u>"
dan "<u>Pernah</u>". **Sciat** (pihak ketiga) secara etimologis "Sciō" (IPA: `/ˈski.oː/`), berarti "<u>Tahu</u>".

Esok Hari Tak Pernah Tahu. Semakin manusia mencari tahu tentang sesuatu, semakin pula ia tidak tahu-menahu
akan sesuatu—ketika manusia mulai mengetahui tentang sesuatu, dirinya menyadari bahwa ia semakin
tidak mengetahui akan sesuatu yang "tidak akan pernah tuntas" untuk dicari tahu.

---

Situs ini dapat di-*benchmark* dan *debug* di [PageSpeed Insights
:(fas fa-arrow-up-right-from-square fa-fw):][PSI-] (atau Lighthouse peramban web),
[GTmetrix :(fas fa-arrow-up-right-from-square fa-fw):][GTm-], atau [KeyCDN Website
Speed Test :(fas fa-arrow-up-right-from-square fa-fw):][KWST].
Kompilasikan segelintir isu-isunya, dan abaikan.

[PSI-]: https://pagespeed.web.dev/report?url=https%3A%2F%2Fowl4ce.github.io%2Fid%2F
        "PageSpeed Insights"
[GTm-]: https://gtmetrix.com
        "GTmetrix"
[KWST]: https://tools.keycdn.com/speed
        "KeyCDN Website Speed Test"

{{< admonition example "Front-end Optimization" false >}}
1. Process WebP-optimized (static) images with LazyLoad (dynamically) at runtime
2. Well-optimized and minified website element codes as much as possible
3. Conditionally load specific libraries for each page only when needed
4. Less use of 3rd-party libraries (through CDN with a preconnect)
{{< /admonition >}}

---

Situs ini dikonfigurasi tidak mengambil dan menyimpan informasi maupun data pribadi pengunjung
dengan teknik apa pun, kecuali **kebijakan alamat IP pengunjung** oleh rumah web
[GitHub Pages :(fas fa-arrow-up-right-from-square fa-fw):][GP].

[GP]: https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages#data-collection
      "GitHub Pages Data Collection"

{{< admonition success "Priv & Sec Transparency" false >}}
1. No 3rd-party services unless assets' CDN
2. No personally proprietary FQDN
3. No setting site Cookies
4. No site Analytics
5. No Trackers
6. No Ads
7. No `?`
{{< /admonition >}}

---

{{< /style >}}
