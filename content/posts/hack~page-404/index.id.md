---
title: "Multibahasa dan Meretas Halaman 404"
subtitle: ""
date: 2022-11-27T21:25:40+07:00
lastmod: 2022-11-27T21:25:40+07:00
draft: false
author: "Harry Kurn"
authorLink: "/id/posts/"
description: ""
license: ""
images: ["https://ik.imagekit.io/owl4ce/id/hack~page-404/f"]

tags: ["Hacking", "Hugo", "JavaScript", "Web-browser"]
categories: ["Technical"]

featuredImage: ""
featuredImagePreview: "https://ik.imagekit.io/owl4ce/id/hack~page-404/f"

hiddenFromHomePage: false
hiddenFromSearch: false
twemoji: false
lightgallery: true
ruby: false
fraction: false
fontawesome: true
linkToMarkdown: false
rssFullText: false

toc:
  enable: true
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
  css: []
  js: []
seo:
  images: ["https://ik.imagekit.io/owl4ce/id/hack~page-404/f"]
  # ...
---

<!--more-->

---

{{< style "text-align:justify" >}}

Halaman dengan kode status 404, digit "4" pertama mengindikasikan kesalahan (*error*) permintaan (*request*) dari
URL terjadi pada tingkat *client* saat berkomunikasi melalui protokol aplikasi HTTP/S. Komunikasi *client-server*
sendiri berfungsi, tetapi ketika informasi yang diminta oleh peramban web *client* tidak dapat disediakan oleh
web *server* maka HTTP/S akan direspon dengan "404 Not Found", dan biasanya diarahkan ke halaman
spesifik seperti <u>/404.html</u> sesuai konfigurasi web *server* terkait.

---

{{< /style >}}

## Problems

{{< style "text-align:justify" >}}

Secara mendasar, masalah nihil apabila *server* yang dikelola dengan akses/kontrol penuh ialah milik
pribadi—meskipun berbagai di antaranya pada hakikatnya otoritas pihak ketiga. Berbagai alasan yang mendasari
mengapa menggunakan/menyewa layanan dari pihak ketiga salah satunya sebab praktis—hemat biaya dan usaha—serta
*professional by default*. Namun, ini akan mematikan bunga kemampuan (*skill*) apabila belum
pernah belajar, baik secara pragmatis maupun radikal (mendasar).

---

{{< /style >}}

### About Static-site

{{< style "text-align:justify" >}}

Alih-alih situs web dinamis-interaktif yang menggunakan [PHP :(fas fa-arrow-up-right-from-square fa-fw):][PHP-]
sebagai *scripting language* yang dieksekusi oleh (dan pada) web *server*, *runtime* situs web statis terbatas
pada peramban web *client*. Menggunakan [JavaScript :(fas fa-arrow-up-right-from-square fa-fw):][JS--] sejatinya
lebih dari cukup untuk me-*generate* informasi situs web statis secara dinamis meskipun kurang interaktif
apabila disandingkan. Masalah utamanya terjadi ketika me-*host* lebih dari satu halaman 404 pada rumah web
(*website hosting*) yang tidak mendukung pengguna untuk melakukan konfigurasi lanjut mengenai pengalihan
(*redirects*) URL dengan kode status (HTTP/S) 404, tiga di antaranya [GitHub Pages
:(fas fa-arrow-up-right-from-square fa-fw):][GHP-], [GitLab Pages
:(fas fa-arrow-up-right-from-square fa-fw):][GLP-], dan [Firebase Hosting
:(fas fa-arrow-up-right-from-square fa-fw):][FbH-].

[PHP-]: https://www.php.net
        "PHP: Hypertext Preprocessor"
[JS--]: https://developer.mozilla.org/en-US/docs/Web/JavaScript
        "JavaScript | MDN"
[GHP-]: https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-custom-404-page-for-your-github-pages-site
        "Creating a custom 404 page for your GitHub Pages site - GitHub Docs"
[GLP-]: https://docs.gitlab.com/ee/user/project/pages/introduction.html#custom-error-codes-pages
        "Custom error codes pages | GitLab"
[FbH-]: https://firebase.google.com/docs/hosting/full-config#404
        "Configure Hosting behavior | Firebase Hosting"

---

{{< /style >}}

#### Multilingual 404 Page

{{< style "text-align:justify" >}}

Bukanlah menjadi masalah apabila sebuah situs web hanya memiliki satu bahasa. Ketiga web *server* dari layanan
di atas dikonfigurasi otomatis menampilkan halaman 404 sesaat pengunjung mencoba mengakses informasi yang tidak ada
(atau dibatasi), dan itu berfungsi dengan baik bagi sebagian pengunjung. Akan tetapi, ketika sebuah situs web memiliki
lebih dari satu bahasa, itu relatif menjadi masalah sebab hanya memungkinkan satu halaman 404 yang ditampilkan.
Misalnya, saat mencoba mengakses halaman berbahasa Indonesia ini dengan jalur URL <u>/ne/hack~page-404/</u> yang
tidak ada, GitHub akan mengarahkannya ke halaman 404 berbahasa Inggris dengan jalur URL yang konsisten.
Perilaku ini mungkin membingungkan pengunjung baru saat mencari halaman dengan bahasa yang relevan—karena
tidak semua halaman tersedia dengan multibahasa untuk setiap halaman tersebut.

---

{{< /style >}}

## Solving Technique

{{< style "text-align:justify" >}}

Satu-satunya teknik penyelesaian perilakunya ialah dengan JavaScript dan mengintegrasikannya ke *static-site
generator* (SSG) apabila menggunakannya. Perlu diperhatikan bahwa setiap SSG memiliki implementasi
*framework*-nya sendiri, sehingga tidak setiap SSG ialah sama persis dengan teknik ini.

---

{{< /style >}}

### Constructing JavaScript

{{< style "text-align:justify" >}}

Konstruksi kode JavaScript dibagi menjadi dua bagian: (1) halaman 404 utama dan (2) halaman 404 dalam
subdirektori bahasa yang didukung. Namun, masalah baru—[*recursive loop*](#that-recursive-loop-en)—muncul
ketika subdirektori bahasa yang didukung tidak memiliki halaman 404—pengalihan dengan [`http-equiv`][http-equiv].

[http-equiv]: https://www.w3.org/TR/WCAG20-TECHS/H76.html
              "H76: Using meta refresh to create an instant client-side redirect | Techniques for WCAG 2.0"

---

{{< /style >}}

#### Main 404 Page (`en`)

{{< style "text-align:justify" >}}

```js
const firstPath = window.location.pathname.split("/")[1];
```

Seperti yang telah dijelaskan di atas, saat halaman 404 utama yang terletak di *root* (/) diakses, jalur URL tidak
menunjukkan letak halaman 404 utama yang sebenarnya. Jalur URL yang ditunjukkan ialah jalur yang sama dengan yang
diminta oleh peramban web *client*—konsisten. Misalnya, URL [<u>https://owl4ce.github.io/ne/hack~page-404/</u>](
/ne/hack~page-404/) akan tetap ditunjukkan pada peramban web *client* saat halaman 404 diakses, alih-alih
[<u>https://owl4ce.github.io/404.html</u>](/404.html). Maka dari itu, *string* <u>ne</u> dari
`window.location.pathname` mungkin diurai, dengan men-`split` *array* pertamanya—bukan nol,
karena nol adalah *null*—yang dipisah dengan pemisah (*delimiter*)
*slash* (/) dari jalur URL (*pathname*).

```js
if (["en", "id"].includes(firstPath))
    window.location.href = window.location.origin + "/" + firstPath + "/404.html?r=" + encodeURIComponent(window.location.pathname);
```

Filter *string* <u>ne</u> (variabel `firstPath`) menggunakan [`includes()`][JS-inc] jika mengandung
salah satu *string* dari *array* `["en", "id"]` bahasa yang didukung. Konstruksi [`if (condition)`][JS-ife]
gagal (*false*) sebab <u>ne</u> tidak sesuai dengan <u>en</u> maupun <u>id</u>. Berandai-andai bahwa <u>ne</u>
menggantikan posisi <u>id</u> maka konstruksi `if (condition)` berhasil (*true*). Kemudian, tetapkan (*set*)
`window.location.href` ke jalur URL halaman 404 bahasa relevan lalu tambahkan *query string* `?` dengan parameter
<u>r</u> dari `window.location.pathname` penuh yang di-*encode* menggunakan [`encodeURIComponent()`][JS-eUC].
Ini akan mengarahkan halaman 404 utama yang diakses ke halaman 404 dalam subdirektori <u>/ne/</u>. URL <u>/id/</u>
diandaikan <u>/ne/</u> maka [<u>https://owl4ce.github.io/ne/404.html?r=%2Fne%2Fhack~page-404%2F</u>](
/ne/404.html?r=%2Fne%2Fhack~page-404%2F).

[JS-inc]: https://developer.mozilla.org/en-US/docs/Web/API/IDBKeyRange/includes
          "IDBKeyRange.includes() - Web APIs | MDN"
[JS-ife]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/if...else
          "if...else - JavaScript | MDN"
[JS-eUC]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/encodeURIComponent
          "encodeURIComponent() - JavaScript | MDN"

---

![ ](https://ik.imagekit.io/owl4ce/id/hack~page-404/2022-12-16-023443_1366x768_scrot
"<sub>Subdirektori <u>/ne/</u> hanya untuk demo.</sub>")

---

{{< /style >}}

#### Secondary 404 Page (`id`)

{{< style "text-align:justify" >}}

```js
if (window.location.search) {
    const urlParams = new URLSearchParams(window.location.search);
    window.history.replaceState("", "", window.location.origin + decodeURIComponent(urlParams.get("r")))
}
```

Beralih halaman 404 dalam subdirektori bahasa. Balikkan pengandaian, posisi <u>ne</u> kembali semula <u>id</u>.
Konstruksi `if (condition)` berhasil (*true*) memeriksa ketersediaan *query string* `?` jalur URL halaman 404 bahasa
relevan dari `window.location.search`. Uraikan *query string* `?` sebagai variabel—untuk di-*decode*—menggunakan
[`new URLSearchParams()`][JS-USP]. Kemudian, tetapkan (*set*) [`window.history.replaceState(stateObj, unused, url)`][
JS-whr] ke parameter <u>r</u> yang merupakan jalur URL (*pathname*) penuh dengan men-*decode*-nya menggunakan
[`decodeURIComponent()`][JS-dUC]. Ini akan mengganti URL sesaat mengakses halaman 404 dalam subdirektori
<u>/id/</u> menjadi URL sebelumnya. Jadi, jalur URL-nya [seakan-akan](/id/404.html?r=%2Fid%2Fhack~page-404%2F)
kembali semula sama dengan saat mengakses halaman 404 utama.

[JS-USP]: https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams/URLSearchParams
          "URLSearchParams() - Web APIs | MDN"
[JS-whr]: https://developer.mozilla.org/en-US/docs/Web/API/History/replaceState
          "History.replaceState() - Web APIs | MDN"
[JS-dUC]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/decodeURIComponent
          "decodeURIComponent() - JavaScript | MDN"

---

![ ](https://ik.imagekit.io/owl4ce/id/hack~page-404/2022-12-16-023742_1366x768_scrot
" ")

![ ](https://ik.imagekit.io/owl4ce/id/hack~page-404/2022-12-16-023748_1366x768_scrot
"<i>Sim Salabim!</i>")

Bukan sulap bukan sihir, beramunisikan kode JavaScript pun URL peramban web *client* [dimanipulasi][soceng].

[soceng]: https://en.wikipedia.org/wiki/Social_engineering_(security)
          "Social engineering (security) - Wikipedia"

---

{{< /style >}}

#### That Recursive Loop (`en`)

{{< style "text-align:justify" >}}

Tahukah mengapa <u>/404.html</u> bukan hanya [*transmitter*](#main-404-page-en), tetapi seakan-akan juga termasuk
[*receiver*](#secondary-404-page-id). Alih-alih subdirektori layaknya bahasa sekunder (*secondary*) bahasa Indonesia,
bahasa utama (*main*) bahasa Inggris diakses langsung dari *root* (/). Keduanya merupakan bahasa yang didukung,
sehingga apabila mengakses <u>/en/404.html</u> yang tidak ada lalu diarahkan ke <u>/404.html</u> maka akan kembali
mengarahkan ke halaman 404 dalam subdirektori <u>/en/</u> yang tidak ada—seakan-akan efek *proximity*. Teknik
penyelesaian perilaku cermin yang dikutuk ialah dengan mengintegrasikan kedua konstruksi.

```js
if (["en", "id"].includes(firstPath))
    if (window.location.search) {
        const urlParams = new URLSearchParams(window.location.search);
        window.history.replaceState("", "", window.location.origin + decodeURIComponent(urlParams.get("r")))
    } else
    window.location.href = window.location.origin + "/" + firstPath + "/404.html?r=" + encodeURIComponent(window.location.pathname);
```

---

{{< /style >}}

### Integrating Code into SSG

{{< style "text-align:justify" >}}

Integrasi kode JavaScript ke SSG berbeda teknik untuk setiap SSG-nya. [Hugo
:(fas fa-arrow-up-right-from-square fa-fw):][ hugo] SSG menggunakan bahasa pemrograman
[Go:(fas fa-arrow-up-right-from-square fa-fw):][go--]. Hanya perlu
mengimplementasikan kodenya pada [*base template*][hgbt]-nya.

[hugo]: https://gohugo.io
        "The world’s fastest framework for building websites | Hugo"
[go--]: https://go.dev
        "The Go Programming Language"
[hgbt]: https://gohugo.io/templates/base/#define-the-base-template
        "Define the Base Template | Hugo"

---

{{< /style >}}

#### Hugo Framework

{{< style "text-align:justify" >}}

{{< admonition tip "layouts/_default/baseof.html" true >}}
```html
<!DOCTYPE html>
<html lang="{{ .Site.LanguageCode }}">
    <head>
    <!-- ... -->
    <!-- Prefer to put the Go codes below above the closing </head> tag. -->
    </head>
    <body>
    <!-- ... -->
    </body>
</html>
```
{{< /admonition >}}

```go
{{- if and (eq .Kind "404") .Site.IsMultiLingual -}}
    {{- $languages := slice -}}
    {{- $languageNext := "" -}}
    <script type="text/javascript">
        (function() {
            {{- range $language := .Site.Languages -}}
                {{- $languages = append $language.Lang $languages -}}
                {{- $languageNext = strings.TrimPrefix "/" $.Site.LanguagePrefix -}}
                {{- if eq $languageNext $language.Lang -}}
                    if(window.location.search) {const o = new URLSearchParams(window.location.search); window.history.replaceState('', '', window.location.origin + decodeURIComponent(o.get('r')))}
                {{- end -}}
            {{- end -}}
            {{- if not $languageNext -}}
                const firstPath = window.location.pathname.split('/')[1]; if({{ $languages }}.includes(firstPath)) if(window.location.search) {const o = new URLSearchParams(window.location.search); window.history.replaceState('', '', window.location.origin + decodeURIComponent(o.get('r')))} else window.location.href = window.location.origin + '/' + firstPath + '/404.html?r=' + encodeURIComponent(window.location.pathname)
            {{- end -}}
        })();
    </script>
{{- end -}}
```

JavaScript hanya perlu di-*generate* pada (dan untuk) <u>404.html</u> dalam setiap direktori bahasa yang didukung.
Konstruksi [`if and`][hgia] memeriksa iterasi saat me-*generate* halaman jika iterasinya untuk halaman 404, dengan
membandingkan variabel internal halaman hugo [`.Kind`][hgpv] dengan *string* <u>404</u> menggunakan [`eq`][hgeq],
dan juga jika variabel internal situs hugo [`.Site.IsMultiLingual`][hgsv] bukan *null*. Kemudian, definisikan
variabel `$languages` sebagai *array* menggunakan [`slice`][hgsl], variabel `$languageNext` sebagai *string*,
dan definisikan serta tetapkan (*set*) variabel `$language` ke *array* [`.Site.Languages`][hgsv] dengan
berulang menggunakan [`range`][hgrg] yang setiap iterasinya merupakan data bahasa yang didukung. Setiap
iterasinya, tetapkan (*set*) variabel `$languages` yang merupakan *array* ke variabel internal situs hugo
[`$language.Lang`][hgsv] dengan menambahkannya menggunakan [`append`][hgap], sehingga diinterpretasikan
[`.Site.Language.Lang`][hgsv] untuk interpretasi kode bahasa. Juga, tetapkan (*set*) variabel `$languageNext`
yang merupakan *string* ke variabel internal situs hugo [`$.Site.LanguagePrefix`][hgsv]—prefiks `$` karena
dalam iterasi `range`—dengan memangkas prefiks "/" menggunakan [`strings.TrimPrefix`][hgtp], guna memeriksa
ketersediaan jalur subdirektori bahasa yang bukan bahasa utama (*main*). Bahasa Inggris (`en`) merupakan
bahasa utama (*main*) yang digunakan, sehingga diperlukanlah pemeriksaan interpretasi tersebut. Konstruksi
`if` memeriksa kebenaran variabel `$languageNext` jika sama dengan variabel [`$language.Lang`][hgsv]
menggunakan `eq` maka integrasikan [kode JavaScript](#secondary-404-page-id) untuk <u>404.html</u> dalam
setiap subdirektori bahasa yang didukung, sebaliknya, jika variabel `$languageNext` tetap *null*—juga karena
prefiks "/" dipangkas—yang berarti dalam iterasi pe-*generate*-an halaman 404 utama maka integrasikan
[kode JavaScript](#that-recursive-loop-en) untuk <u>/404.html</u>. Bahasa Indonesia (`id`)
merupakan bahasa sekunder (*secondary*)—meski terbalik.

[hgia]: https://gohugo.io/templates/introduction/#example-6-and--or
        "Example 6: and & or | Hugo"
[hgpv]: https://gohugo.io/variables/page/#page-variables
        "Page Variables | Hugo"
[hgeq]: https://gohugo.io/functions/eq
        "eq | Hugo"
[hgsv]: https://gohugo.io/variables/site/#site-variables-list
        "Site Variables List | Hugo"
[hgsl]: https://gohugo.io/functions/slice
        "slice | Hugo"
[hgrg]: https://gohugo.io/functions/range
        "range | Hugo"
[hgap]: https://gohugo.io/functions/append
        "append | Hugo"
[hgtp]: https://gohugo.io/functions/strings.trimprefix
        "strings.trimprefix | Hugo"

---

{{< /style >}}

## Afterword

{{< style "text-align:justify" >}}

Demikianlah, benang merah ikhtisar ini dijabarkan secara mengakar sedalam tanah meskipun sukar.

{{< /style >}}
