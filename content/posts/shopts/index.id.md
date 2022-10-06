---
title: "Optimisasi Mikro dan Portabilitas Unix-shell"
subtitle: ""
date: 2022-03-14T22:36:11+07:00
lastmod: 2022-03-14T22:36:11+07:00
draft: false
author: "Harry Kurn"
authorLink: ""
description: "Memperkokoh paradigma seorang administrator dalam menyusun algoritma, praktis komprehensif."
license: ""
images: ["/id/shopts/featured.jpg"]

tags: ["Unix-like"]
categories: ["Technical"]

featuredImage: ""
featuredImagePreview: "/id/shopts/featured.jpg"

hiddenFromHomePage: false
hiddenFromSearch: false
twemoji: false
lightgallery: false
ruby: false
fraction: false
fontawesome: true
linkToMarkdown: true
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
  enable: true
  # ...
comment:
  enable: false
  # ...
library:
  css: []
  js: ["js/shield.js"]
seo:
  images: ["/id/shopts/featured.jpg"]
  # ...
---

<!--more-->

---

{{< style "text-align:justify" >}}

Memahami spesifikasi POSIX maka otomatis menguasai berbagai (Unix) *shell*. Memahami bukanlah hanya
diketahui, tetapi harus mempelajari lingkungan *userspace*. Mempelajari tidak sekedar *trial-error*,
melainkan diaplikasikan, guna memperkokoh paradigma dalam menyusun sebuah algoritma. Demikian,
rangkuman praktis ini didedikasikan bagi para "pragmatis" terhadap segala urusan teknis.

---

{{< /style >}}

## Parameter Expansion

### Type of Shell Parameters

#### Variable

{{< style "text-align:justify" >}}

```shell
name="value"
```

```shell
echo "$name"
```

{{< admonition success "/proc/self/fd/1" true >}}
value
{{< /admonition >}}

---

{{< /style >}}

#### Positional

{{< style "text-align:justify" >}}

```shell
set -- is a shell
```

```shell
echo "$0 $1 $2 $3"
```

{{< admonition success "/proc/self/fd/1" true >}}
dash is a shell
{{< /admonition >}}

---

{{< /style >}}

#### Special

{{< style "text-align:justify" >}}

```shell
man 1 bash | less +/Special\ Parameters +n
```

```shell
echo "$$"
```

{{< admonition success "/proc/self/fd/1" true >}}
1337
{{< /admonition >}}

---

{{< /style >}}

### Expanding Substrings

#### Conditional Test

{{< style "text-align:justify" >}}

```shell
# POSIX.1-2017: ${parameter:-string}
```

```shell
echo "${VARIABLE:-"negative-fallback value to output here"}"
```

{{< admonition success "/proc/self/fd/1" true >}}
negative-fallback value to output here
{{< /admonition >}}

---

```shell
# POSIX.1-2017: ${parameter:?string}
```

```shell
echo "${VARIABLE:?"\$VARIABLE is unset."}"
```

{{< admonition failure "/proc/self/fd/2" true >}}
dash: 4: VARIABLE: $VARIABLE is unset.
{{< /admonition >}}

---

```shell
# POSIX.1-2017: ${parameter:=string}
```

```shell
echo "${VARIABLE:="negative-fallback value to set and output here"}"
```

{{< admonition success "/proc/self/fd/1" true >}}
negative-fallback value to set and output here
{{< /admonition >}}

---

```shell
# POSIX.1-2017: ${parameter:+string}
```

```shell
echo "${VARIABLE:+"positive-fallback value to output here"}"
```

{{< admonition success "/proc/self/fd/1" true >}}
positive-fallback value to output here
{{< /admonition >}}

---

{{< /style >}}

#### Length Counter

{{< style "text-align:justify" >}}

```shell
# POSIX.1-2017: ${#parameter}
```

```shell
echo "Panjang '$VARIABLE' adalah ${#VARIABLE} karakter."
```

{{< admonition success "/proc/self/fd/1" true >}}
Panjang 'negative-fallback value to set and output here' adalah 46 karakter.
{{< /admonition >}}

---

{{< /style >}}

#### Processor (glob)

{{< style "text-align:justify" >}}

```shell
AUDIO_VOLUME="$(amixer sget Master)"
echo "$AUDIO_VOLUME" # Show the value.
```

{{< admonition success "/proc/self/fd/1" true >}}
Simple mixer control 'Master',0  
Capabilities: pvolume pswitch pswitch-joined  
Playback channels: Front Left - Front Right  
Limits: Playback 0 - 65536  
Mono:  
Front Left: Playback 39324 [60%] [on]  
Front Right: Playback 39324 [60%] [on]
{{< /admonition >}}

```shell
# POSIX.1-2017: ${parameter#string}
#               ${parameter##string}
```

```shell
AUDIO_VOLUME="${AUDIO_VOLUME#* \[}" # Remove closest prefix.
```

```shell
# POSIX.1-2017: ${parameter%string}
#               ${parameter%%string}
```

```shell
AUDIO_VOLUME="${AUDIO_VOLUME%%%\] *}" # Remove furthest suffix.
```

```shell
echo "$AUDIO_VOLUME" # Show the final value.
```

{{< admonition success "/proc/self/fd/1" true >}}
60
{{< /admonition >}}

---

```shell
FIRST_SECOND='dua satu'
```

```shell
# ksh93, bash, zsh, mksh, busybox sh: ${parameter:offset}
#                                     ${parameter:offset:length}
```

```bash
printf '%s\n' "${FIRST_SECOND:4}" "${FIRST_SECOND:0:3}"
```

{{< admonition success "/proc/self/fd/1" true >}}
satu  
dua
{{< /admonition >}}

```shell
# Alternative with expr from GNU coreutils.
```

```shell
expr "x${FIRST_SECOND}" : 'x.\{0,4\}\(.\{0,4\}\)'
```

{{< admonition success "/proc/self/fd/1" true >}}
satu
{{< /admonition >}}

```shell
# Alternative with cut from GNU coreutils.
```

```bash
cut -b1-4 <<< "$FIRST_SECOND" # bash herestrings.
```

{{< admonition success "/proc/self/fd/1" true >}}
dua
{{< /admonition >}}

---

```shell
CURRENT_SONG='Polyphia - Ego Death (feat. Steve Vai)'
```

```shell
# ksh93, bash, zsh, mksh: ${parameter/pattern}
#                         ${parameter/pattern/string}
#                         ${parameter//pattern}
#                         ${parameter//pattern/string}
```

```bash
printf '%s\n' "${CURRENT_SONG/\(feat. *)/(feat. Guitar Lord)}" "${CURRENT_SONG//[AaIiUuEeOo]}"
```

{{< admonition success "/proc/self/fd/1" true >}}
Polyphia - Ego Death (feat. Guitar Lord)  
Plyph - g Dth (ft. Stv V)
{{< /admonition >}}

---

```shell
CURRENT_SONG='Avenged Sevenfold - Nightmare'
```

```shell
# bash 4.3+: ${parameter^pattern}
#            ${parameter^^pattern}
#            ${parameter,pattern}
#            ${parameter,,pattern}
#            ${parameter~~pattern}
```

```bash
printf '%s\n' "${CURRENT_SONG^^}" "${CURRENT_SONG,,}" "${CURRENT_SONG~~}"
```

{{< admonition success "/proc/self/fd/1" true >}}
AVENGED SEVENFOLD - NIGHTMARE  
avenged sevenfold - nightmare  
aVENGED sEVENFOLD - nIGHTMARE
{{< /admonition >}}

```shell
# Alternative with (POSIX) tr.
```

```bash
tr '[:lower:]' '[:upper:]' <<< "$CURRENT_SONG" # bash herestrings.
tr '[:upper:]' '[:lower:]' <<< "$CURRENT_SONG"
```

{{< admonition success "/proc/self/fd/1" true >}}
AVENGED SEVENFOLD - NIGHTMARE  
avenged sevenfold - nightmare
{{< /admonition >}}

```shell
# Alternative with (POSIX) awk.
```

```bash
awk '{print toupper($0)}' <<< "$CURRENT_SONG" # bash herestrings.
awk '{print tolower($0)}' <<< "$CURRENT_SONG"
```

{{< admonition success "/proc/self/fd/1" true >}}
AVENGED SEVENFOLD - NIGHTMARE  
avenged sevenfold - nightmare
{{< /admonition >}}

```shell
# Alternative with (GNU) sed.
```

```bash
sed 's/.*/\U&/' <<< "$CURRENT_SONG" # bash herestrings.
sed 's/.*/\L&/' <<< "$CURRENT_SONG"
sed 's/.*/\u&/' <<< "$CURRENT_SONG"
sed 's/.*/\l&/' <<< "$CURRENT_SONG"
```

{{< admonition success "/proc/self/fd/1" true >}}
AVENGED SEVENFOLD - NIGHTMARE  
avenged sevenfold - nightmare  
Avenged Sevenfold - Nightmare  
avenged Sevenfold - Nightmare
{{< /admonition >}}


```shell
# zsh 5+: Parameter Expansion Flags
```

```shell
printf '%s\n' "${(U)CURRENT_SONG}" "${(L)CURRENT_SONG}"
```

{{< admonition success "/proc/self/fd/1" true >}}
AVENGED SEVENFOLD - NIGHTMARE  
avenged sevenfold - nightmare
{{< /admonition >}}

```shell
# zsh 5+: Parameter Expansion Modifiers
```

```shell
printf '%s\n' "${CURRENT_SONG:u}" "${CURRENT_SONG:l}"
```

{{< admonition success "/proc/self/fd/1" true >}}
AVENGED SEVENFOLD - NIGHTMARE  
avenged sevenfold - nightmare
{{< /admonition >}}

---

{{< /style >}}

## Brace Expansion

### Nested

{{< style "text-align:justify" >}}

```shell
# ksh93, bash, zsh, yash, mksh: {a,b}
#                               {a{,lpha},b{,eta}}
```

```bash
printf '%s\n' /{,usr/}{{,s}bin,lib{,64}}
```

{{< admonition success "/proc/self/fd/1" true >}}
/bin  
/sbin  
/lib  
/lib64  
/usr/bin  
/usr/sbin  
/usr/lib  
/usr/lib64
{{< /admonition >}}

---

{{< /style >}}

### Incremental Sequence

{{< style "text-align:justify" >}}

```shell
# ksh93, bash, zsh, yash, mksh: {x..y..incr}
```

```bash
printf '%s\n' {A..C} '' {0..100..10}
```

{{< admonition success "/proc/self/fd/1" true >}}
A  
B  
C  
  
0  
10  
20  
30  
40  
50  
60  
70  
80  
90  
100
{{< /admonition >}}

---

{{< /style >}}

## I/O Redirection

### Clobbering Output

#### Create/overwrite

{{< style "text-align:justify" >}}

```shell
# POSIX.1-2017: > /path/to/file
```

```shell
echo 'the first line' > /tmp/file
```

---

{{< /style >}}

#### Create/append to

{{< style "text-align:justify" >}}

```shell
# POSIX.1-2017: >> /path/to/file
```

```shell
echo 'appended line' >> /tmp/file
```

---

{{< /style >}}

#### Disable clobbering

{{< style "text-align:justify" >}}

```shell
# ksh, bash, zsh: set -o noclobber
#                 set +o noclobber
# csh, tcsh:      set noclobber
#                 ?
# dash:           set -C
#                 set +C
```

```shell
set -C # Disable, use +C to re-enable.
echo '... overwrite data.' > /tmp/file
```

{{< admonition failure "/proc/self/fd/2" true >}}
dash: 4: cannot create /tmp/file: File exists
{{< /admonition >}}

---

{{< /style >}}

#### Bypass noclobber

{{< style "text-align:justify" >}}

```shell
# POSIX.1-2017: >| /path/to/file
```

```shell
echo '... overwrite data.' >| /tmp/file
```

---

{{< /style >}}

### Reading Input ft. POSIX `read`

#### File Standard Input

{{< style "text-align:justify" >}}

```shell
# POSIX.1-2017: < /path/to/file
```

```shell
read -r FILE < /tmp/file # Only read the first line.
echo "$FILE"             # Show the value.
```

{{< admonition success "/proc/self/fd/1" true >}}
... overwrite data.
{{< /admonition >}}

---

```shell
# bash 4.4+: $(< /path/to/file)
```

```bash
FILE="$(< /tmp/file)" # Read the whole contents.
echo "$FILE"          # Show the value.
```

{{< admonition success "/proc/self/fd/1" true >}}
... overwrite data.
{{< /admonition >}}

---

{{< /style >}}

#### Here Documents Input

{{< style "text-align:justify" >}}

```shell
# POSIX.1-2017: << KEYWORD
#               << "KEYWORD"
#               <<- KEYWORD
#               <<- "KEYWORD"
```

```shell
while read -r DOC; do # Read every line in a loop.
    echo "$DOC"       # Show the value of each loop.
done <<- "EOL"        # Quotes for string, hyphen for tab indentation.
	this is heredocs
	second line ...
	third line ...
EOL
```

{{< admonition success "/proc/self/fd/1" true >}}
this is heredocs  
second line ...  
third line ...
{{< /admonition >}}

---

{{< /style >}}

#### Here Strings Input

{{< style "text-align:justify" >}}

```shell
# ksh, bash, zsh: <<< "contents"
```

```bash
read -r STRING <<< 'this is herestrings' # Indeed, only contains single line.
echo "$STRING"                           # Show the value.
```

{{< admonition success "/proc/self/fd/1" true >}}
this is herestrings
{{< /admonition >}}

---

{{< /style >}}

#### Internal Field Separator

##### Replicate `uname -r`

{{< style "text-align:justify" >}}

```shell
uname -r # Show the contents.
```

{{< admonition success "/proc/self/fd/1" true >}}
5.19.10-hikari-x86_64
{{< /admonition >}}

```shell
cat /proc/version # Show the contents.
```

{{< admonition success "/proc/self/fd/1" true >}}
Linux version 5.19.10-hikari-x86_64 (root@localh3art) (clang version 14.0.6, LLD 14.0.6) #1 ...
{{< /admonition >}}

```shell
IFS=' ' read -r _ _ KVER _ < /proc/version # Parse the 3rd word, IFS is space.
echo "$KVER"                               # Show the final value.
```

{{< admonition success "/proc/self/fd/1" true >}}
5.19.10-hikari-x86_64
{{< /admonition >}}

---

{{< /style >}}

##### Replicate `uptime -p`

{{< style "text-align:justify" >}}

```shell
uptime -p # Show the contents.
```

{{< admonition success "/proc/self/fd/1" true >}}
up 5 hours, 39 minutes
{{< /admonition >}}

```shell
cat /proc/uptime # Show the contents.
```

{{< admonition success "/proc/self/fd/1" true >}}
20372.66 69096.54
{{< /admonition >}}

| Seconds since boot | Seconds of CPU cores while idle |
|:---:|:---:|
| 20372.66 | 69096.54 |

```shell
IFS='.' read -r S _ < /proc/uptime                       # Remove period suffix.
D="$((S/60/60/24))"                                      # Calculate day(s).
H="$((S/60/60%24))"                                      # Calculate hour(s).
M="$((S/60%60))"                                         # Calculate minute(s).
[ "$D" -lt 2 ] || DP='s'                                 # Day(s) plural.
[ "$H" -lt 2 ] || HP='s'                                 # Hour(s) plural.
[ "$M" -lt 2 ] || MP='s'                                 # Minute(s) plural.
[ "$S" -lt 2 ] || SP='s'                                 # Second(s) plural.
[ "$D" -eq 0 ] || UPTIME_P="${D} day${DP}, "             # Day(s) format.
[ "$H" -eq 0 ] || UPTIME_P="${UPTIME_P}${H} hour${HP}, " # Hour(s) format.
[ "$M" -eq 0 ] || UPTIME_P="${UPTIME_P}${M} minute${MP}" # Minute(s) format.
[  -n  "$M"  ] || UPTIME_P="${UPTIME_P}${S} second${SP}" # Second(s) format.
echo 'up' "$UPTIME_P"                                    # Show the final value.
```

{{< admonition success "/proc/self/fd/1" true >}}
up 5 hours, 39 minutes
{{< /admonition >}}

---

{{< /style >}}

<!--CUT-HERE-->

{{< style "text-align:right" >}}

{{< typeit tag=h3 >}}
*To be continued ...*
{{< /typeit >}}

---

{{< /style >}}

<!--CUT-HERE-->

## Additional References

{{< style "text-align:justify" >}}

1. Manpage: dash([1](https://linux.die.net/man/1/dash))
2. Manpage: [bash](https://gnu.org/software/bash/manual/bash.html)([1](https://linux.die.net/man/1/bash))
3. Manpage: [zsh](https://zsh.sourceforge.io/Doc/Release/zsh_toc.html)([1](https://linux.die.net/man/1/zsh))
4. Article: [Bashism](https://mywiki.wooledge.org/Bashism)
5. Specs: [POSIX.1-2017](https://pubs.opengroup.org/onlinepubs/9699919799)
6. Book: [Pure /bin/sh](https://github.com/dylanaraps/pure-sh-bible)
7. Book: [Pure bash](https://github.com/dylanaraps/pure-bash-bible)

{{< /style >}}
