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

The **C**.**D**.**N**.**S**. book was built by **{{< person url="" name="" nick="owl4ce"
text="Webmaster" picture="https://avatars.githubusercontent.com/u/53987136?s=20" >}}** on the basis of the simplicity
of elements (the site), the elegance of interface (the book), and the robustness (?) of presentations (the writing).
Written semi-formally (standard) in Bahasa Indonesia as the language of Unitary Republic of Indonesia,
as the 3rd pledge of Youth Pledge. Certain sections are also written in English partially for
a specific purpose: alignment with the internationalization of English in
applied science and as the main communicator.

---

The title of this book is adopted from Latin. **Crastinus** (IPA: `/ˈkraːs.ti.nus/`) etymologically
"Crās" and suffix (masculine) "-tinus", means "<u>Tomorrow's</u>". **Dies** (IPA: `/ˈdi.eːs/`) etymologically "Diēs",
means "<u>Day</u>". **Nunquam** (IPA: `/ˈnum.kʷam/`) etymologically "Nē" and "unquam", means "<u>Not</u>"
and "<u>Ever</u>". **Sciat** (from 3rd person) etymologically "Sciō" (IPA: `/ˈski.oː/`), means "<u>Known</u>".

Tomorrow's Day Never Known. The more humans find out about something, the more they don't know
anything about it—when humans (just) start to know about something, themself (just) realize that they are
increasingly ignorant of something that "will never be completed" to find out (known).

---

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
1. Process WebP-optimized (static) images with LazyLoad (dynamically) at runtime
2. Well-optimized and minified website element codes as much as possible
3. Conditionally load specific libraries for each page only when needed
4. Less use of 3rd-party libraries (through CDN with a preconnect)
{{< /admonition >}}

---

This site is configured not to collect (gather) and store any information or any visitor's personal data
with any techniques, except for **visitor's IP address policy** by the website hosting
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
