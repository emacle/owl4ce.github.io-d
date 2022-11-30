---
title: "Site Policy"
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

## Introduction to Book

{{< style "text-align:justify" >}}

The [**C**.**D**.**N**.**S**.][CDNS] book was built by {{< person url="#webmaster" name=""
nick="owl4ce" text="Webmaster" picture="https://github.com/owl4ce.png" >}} on the basis of the simplicity of
elements ([the site](#site-information)), the elegance of interface (the book), and the robustness (?) of presentations
(the writing). Written semi-formally (standard) in Bahasa Indonesia as the language of Unitary Republic of Indonesia,
as the 3rd pledge of Youth Pledge. Certain sections are also written in English partially for a
specific purpose: alignment with the internationalization of English in
applied science and as the main communicator.

[CDNS]: /humans.txt
        "Crastinus Dies Nunquam Sciat"

---

{{< /style >}}

### **:(fas fa-dove fa-fw):** <sub>Definition and Philosophy</sub>

{{< style "text-align:justify" >}}

The title of this book is adopted from Latin. **Crastinus** (IPA: `/ˈkraːs.ti.nus/`) etymologically
"Crās" and suffix (masculine) "-tinus", means "<u>Tomorrow's</u>". **Dies** (IPA: `/ˈdi.eːs/`) etymologically "Diēs",
means "<u>Day</u>". **Nunquam** (IPA: `/ˈnum.kʷam/`) etymologically "Nē" and "unquam", means "<u>Not</u>"
and "<u>Ever</u>". **Sciat** (from 3rd person) etymologically "Sciō" (IPA: `/ˈski.oː/`), means "<u>Knows</u>".

Tomorrow's Day Never Knows. The more humans find out about something, the more they don't knows
anything about it—when humans (just) start to know about something, themself (just) realize that they are
increasingly ignorant of something that "will not ever complete" to find out (to knows).

---

{{< /style >}}

## Site Information

### **:(fas fa-rocket fa-fw):** <sub>99+ Performance</sub>

{{< style "text-align:justify" >}}

This site can be benchmarked and debug on [PageSpeed Insights
:(fas fa-arrow-up-right-from-square fa-fw):][PSI-] (or web-browser's Lighthouse),
[GTmetrix :(fas fa-arrow-up-right-from-square fa-fw):][GTm-], or [KeyCDN Website
Speed Test :(fas fa-arrow-up-right-from-square fa-fw):][KWST].
Compile a handful of the issues, and ignore them.

[PSI-]: https://pagespeed.web.dev/report?url=https%3A%2F%2Fowl4ce.github.io%2Fid%2F
        "PageSpeed Insights"
[GTm-]: https://gtmetrix.com
        "GTmetrix"
[KWST]: https://tools.keycdn.com/speed
        "KeyCDN Website Speed Test"

{{< admonition abstract "Question and Answer" false >}}
- [Cache Control for GitHub Pages :(fas fa-arrow-up-right-from-square fa-fw):][CCfGP----]
- [Just How Fast Are GitHub Pages? :(fas fa-arrow-up-right-from-square fa-fw):][JHFAGP---]
- [Lighthouse score of 100: not always for the better :(fas fa-arrow-up-right-from-square fa-fw):][Lso1naftb]
- [Google's Lighthouse Accessibility Tests Are Helpful, But Not Perfect :(fas fa-arrow-up-right-from-square fa-fw):][GLATAHBNP]

[CCfGP----]: https://retirednotout.uk/blog/2021/05/cache-control-for-github-pages
             "Cache Control for GitHub Pages"
[JHFAGP---]: https://www.jeremymorgan.com/blog/programming/how-fast-are-github-pages
             "Just How Fast Are GitHub Pages?"
[Lso1naftb]: https://nooshu.com/blog/2019/08/18/lighthouse-score-100-not-always-for-the-better
             "Lighthouse score of 100: not always for the better"
[GLATAHBNP]: https://www.boia.org/blog/googles-lighthouse-accessibility-tests-are-helpful-but-not-perfect
             "Google's Lighthouse Accessibility Tests Are Helpful, But Not Perfect"
{{< /admonition >}}

{{< admonition example "Front-end Optimization" true >}}
1. Process WebP-optimized (static) images with Lazy Load (dynamically) at runtime
2. Well-optimized and minified website element codes as much as possible
3. Conditionally load specific libraries for each page only when needed
4. Less use of 3rd-party libraries (through CDN with a preconnect)
{{< /admonition >}}

---

{{< /style >}}

### **:(fas fa-shield-heart fa-fw):** <sub>99% Privacy</sub>

{{< style "text-align:justify" >}}

This site is configured not to collect (gather) and store any information or any visitor's personal data
with any techniques, except for **visitor's IP address policy** by the website hosting
[GitHub Pages :(fas fa-arrow-up-right-from-square fa-fw):][GP].

[GP]: https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages#data-collection
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

## Webmaster

{{< style "text-align:justify" >}}

If (readers) have relevant questions (or criticisms and suggestions),
[[e-mail][e-mail]] webmaster or [[matrix][matrix]].

[e-mail]: ../../index.xml
          "Write E-Mail to Webmaster"
[matrix]: https://matrix.to/#/@owl4ce:matrix.org
          "Discuss!"

---

{{< /style >}}

### **:(fas fa-key fa-fw):** <sub>PGP Key</sub>

{{< style "text-align:justify" >}}

```shell
curl -sL https://git.io/JKsMD | gpg --import
```

{{< admonition info "Fingerprint" false >}}
B9BD C551 5AF4 9F42 CBC8 CF39 7D03 DB4D 862E A826
{{< /admonition >}}

---

{{< /style >}}
