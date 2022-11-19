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
  copy: true
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

## Pengantar Pustaka

{{< style "text-align:justify" >}}

Pustaka [**C**.**D**.**N**.**S**.][CDNS] dibangun oleh {{< person url="#pemilik-web" name=""
nick="owl4ce" text="Pemilik Web" picture="https://github.com/owl4ce.png" >}} atas dasar kesederhanaan
elemen ([situs](#informasi-situs)), keanggunan antarmuka (buku), dan kekukuhan (?) penyajian (tulisan).
Ditulis secara semiformal (baku) dalam bahasa Indonesia sebagai bahasa persatuan NKRI, sebagaimana
ikrar ke-3 Sumpah Pemuda. Bagian tertentu juga ditulis dalam bahasa Inggris secara parsial atas
tujuan khusus: penyelarasan terhadap internasionalisasi bahasa Inggris dalam
ilmu pengetahuan terapan dan sebagai komunikator utama.

[CDNS]: /humans.txt "Crastinus Dies Nunquam Sciat"

---

{{< /style >}}

### **:(fas fa-dove fa-fw):** <sub>Definisi dan Filosofi</sub>

{{< style "text-align:justify" >}}

Judul pustaka ini diadopsi dari bahasa Latin. **Crastinus** (IPA: `/ˈkraːs.ti.nus/`) secara etimologis
"Crās" dan‎ sufiks (maskulin) "-tinus", berarti "<u>Esok</u>". **Dies** (IPA: `/ˈdi.eːs/`) secara etimologis "Diēs",
berarti "<u>Hari</u>". **Nunquam** (IPA: `/ˈnum.kʷam/`) secara etimologis "Nē" dan "unquam", berarti "<u>Tak</u>"
dan "<u>Pernah</u>". **Sciat** (pihak ketiga) secara etimologis "Sciō" (IPA: `/ˈski.oː/`), berarti "<u>Tahu</u>".

Esok Hari Tak Pernah Tahu. Semakin manusia mencari tahu tentang sesuatu, semakin pula ia tidak tahu-menahu
akan sesuatu—ketika manusia mulai mengetahui tentang sesuatu, dirinya menyadari bahwa ia semakin
tidak mengetahui akan sesuatu yang "tidak akan pernah tuntas" untuk dicari tahu.

---

{{< /style >}}

## Informasi Situs

### **:(fas fa-rocket fa-fw):** <sub>99+ Performa</sub>

{{< style "text-align:justify" >}}

Situs ini dapat di-*benchmark* dan *debug* di [PageSpeed Insights
:(fas fa-arrow-up-right-from-square fa-fw):][ps-i] (atau Lighthouse peramban web),
[GTmetrix :(fas fa-arrow-up-right-from-square fa-fw):][gt-m], atau [KeyCDN Website
Speed Test :(fas fa-arrow-up-right-from-square fa-fw):][kC-s].
Kompilasikan segelintir isu-isunya, dan abaikan.

[ps-i]: https://pagespeed.web.dev/report?url=https%3A%2F%2Fowl4ce.github.io%2Fid%2F "PageSpeed Insights"
[gt-m]: https://gtmetrix.com "GTmetrix"
[kC-s]: https://tools.keycdn.com/speed "KeyCDN Website Speed Test"

{{< admonition abstract "Question and Answer" false >}}
- [Cache Control for GitHub Pages :(fas fa-arrow-up-right-from-square fa-fw):][ccf]
- [Just How Fast Are GitHub Pages? :(fas fa-arrow-up-right-from-square fa-fw):][jhf]
- [Lighthouse score of 100: not always for the better :(fas fa-arrow-up-right-from-square fa-fw):][lso]
- [Google's Lighthouse Accessibility Tests Are Helpful, But Not Perfect :(fas fa-arrow-up-right-from-square fa-fw):][gla]

[ccf]: https://retirednotout.uk/blog/2021/05/cache-control-for-github-pages
       "Cache Control for GitHub Pages"
[jhf]: https://www.jeremymorgan.com/blog/programming/how-fast-are-github-pages
       "Just How Fast Are GitHub Pages?"
[lso]: https://nooshu.com/blog/2019/08/18/lighthouse-score-100-not-always-for-the-better
       "Lighthouse score of 100: not always for the better"
[gla]: https://www.boia.org/blog/googles-lighthouse-accessibility-tests-are-helpful-but-not-perfect
       "Google's Lighthouse Accessibility Tests Are Helpful, But Not Perfect"
{{< /admonition >}}

{{< admonition example "Front-end Optimization" true >}}
1. Process WebP-optimized (static) images with Lazy Load (dynamically) at runtime
2. Well-optimized and minified website element codes as much as possible
3. Conditionally load specific libraries for each page only when needed
4. Less use of 3rd-party libraries (through CDN without preconnect)
{{< /admonition >}}

---

{{< /style >}}

### **:(fas fa-shield-heart fa-fw):** <sub>99% Privasi</sub>

{{< style "text-align:justify" >}}

Situs ini dikonfigurasi tidak mengambil dan menyimpan informasi maupun data pribadi pengunjung
dengan teknik apa pun, kecuali **kebijakan alamat IP pengunjung** oleh rumah web
[GitHub Pages :(fas fa-arrow-up-right-from-square fa-fw):][gh-p].

[gh-p]: https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages#data-collection
        "GitHub Pages Data Collection"

{{< admonition danger "Seven Implemented Things to Avoid" true >}}
1. Avoid 3rd-party services unless assets' CDN
2. Avoid personally proprietary FQDN
3. Avoid setting site Cookies
4. Avoid any Analytics
5. Avoid Trackers
6. Avoid Ads
7. Avoid ?
{{< /admonition >}}

---

{{< /style >}}

## Pemilik Web

{{< style "text-align:justify" >}}

Apabila memiliki pertanyaan (atau kritik dan saran) yang relevan,
[[e-mail][e-mail]] pemilik web atau [[matrix][matrix]].

[e-mail]: ../../index.xml "Tulis E-Mail kepada Webmaster"
[matrix]: https://matrix.to/#/@owl4ce:matrix.org "Diskusikan!"

---

{{< /style >}}

### **:(fas fa-key fa-fw):** <sub>Kunci PGP</sub>

{{< style "text-align:justify" >}}

```shell
curl -sL https://git.io/JKsMD | gpg --import
```

{{< admonition type=info title="Fingerprint" open=false >}}
B9BD C551 5AF4 9F42 CBC8 CF39 7D03 DB4D 862E A826
{{< /admonition >}}

---

{{< /style >}}
