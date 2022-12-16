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

The [**C**.**D**.**N**.**S**.][CDNS] book was built by {{< person url="#leave-a-message" name="" nick="owl4ce"
text="Webmaster" picture="https://avatars.githubusercontent.com/u/53987136?s=20" >}} on the basis of the simplicity of
elements ([the site](#site-information)), the elegance of interface (the book), and the robustness (?) of presentations
(the writing). Written semi-formally (standard) in Bahasa Indonesia as the language of Unitary Republic of Indonesia,
as the 3rd pledge of Youth Pledge. Certain sections are also written in English partially for a
specific purpose: alignment with the internationalization of English in
applied science and as the main communicator.

[CDNS]: /humans.txt
        "Crastinus Dies Nunquam Sciat"

---

{{< /style >}}

### **:(fas fa-dove fa-fw):** <sub><sup>Definition and Philosophy</sup></sub>

{{< style "text-align:justify" >}}

The title of this book is adopted from Latin. **Crastinus** (IPA: `/ˈkraːs.ti.nus/`) etymologically
"Crās" and suffix (masculine) "-tinus", means "<u>Tomorrow's</u>". **Dies** (IPA: `/ˈdi.eːs/`) etymologically "Diēs",
means "<u>Day</u>". **Nunquam** (IPA: `/ˈnum.kʷam/`) etymologically "Nē" and "unquam", means "<u>Not</u>"
and "<u>Ever</u>". **Sciat** (from 3rd person) etymologically "Sciō" (IPA: `/ˈski.oː/`), means "<u>Known</u>".

Tomorrow's Day Never Known. The more humans find out about something, the more they don't know
anything about it—when humans (just) start to know about something, themself (just) realize that they are
increasingly ignorant of something that "will never be completed" to find out (known).

---

{{< /style >}}

## Site Information

### **:(fas fa-rocket fa-fw):** <sub><sup>99+ Performance</sup></sub>

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

{{< admonition example "Front-end Optimization" false >}}
1. Process WebP-optimized (static) images with Lazy Load (dynamically) at runtime
2. Well-optimized and minified website element codes as much as possible
3. Conditionally load specific libraries for each page only when needed
4. Less use of 3rd-party libraries (through CDN with a preconnect)
{{< /admonition >}}

---

{{< /style >}}

### **:(fas fa-shield-heart fa-fw):** <sub><sup>99% Privacy</sup></sub>

{{< style "text-align:justify" >}}

This site is configured not to collect (gather) and store any information or any visitor's personal data
with any techniques, except for **visitor's IP address policy** by the website hosting
[GitHub Pages :(fas fa-arrow-up-right-from-square fa-fw):][GP].

[GP]: https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages#data-collection
      "GitHub Pages Data Collection"

{{< admonition danger "Seven Horrible  ̶I̶n̶s̶e̶c̶u̶r̶e̶ Things" false >}}
1. Avoid 3rd-party services unless assets' CDN
2. Avoid personally proprietary FQDN
3. Avoid setting site Cookies
4. Avoid site Analytics
5. Avoid Trackers
6. Avoid Ads
7. Avoid `?`
{{< /admonition >}}

---

{{< /style >}}

## Leave a Message

{{< style "text-align:justify" >}}

If (readers) have relevant questions (or criticisms and suggestions),
[<a href="mailto&#58;%&#54;1&#108;t%6&#53;%72nate%2&#68;&#115;e%&#51;7e&#37;6E&#64;proton&#46;&#109;e"
    title="Write E-Mail to Webmaster"
    target="_blank"
    rel="external noopener noreferrer">e-mail</a>]
webmaster or [[matrix][matrix]].

[matrix]: https://matrix.to/#/@owl4ce:matrix.org
          "Discuss!"

---

{{< /style >}}

### **:(fas fa-fingerprint fa-fw):** <sub><sup>PGP Key</sup></sub>

{{< style "text-align:justify" >}}

```shell
curl -sL https://git.io/JKsMD | gpg --import
```

{{< admonition info "Fingerprint" false >}}
B9BD C551 5AF4 9F42 CBC8 CF39 7D03 DB4D 862E A826
{{< /admonition >}}

---

{{< /style >}}
