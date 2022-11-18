---
title: "Optimisasi dan Portabilitas Unix Shell"
subtitle: ""
date: 2022-03-14T22:36:11+07:00
lastmod: 2022-03-14T22:36:11+07:00
draft: false
author: "Harry Kurn"
authorLink: "/id/posts/"
description: " "
license: ""
images: ["https://ik.imagekit.io/owl4ce/id/opts~unix-shell/f"]

tags: ["Optimization", "Shell", "Unix-like"]
categories: ["Technical"]

featuredImage: ""
featuredImagePreview: "https://ik.imagekit.io/owl4ce/id/opts~unix-shell/f"

hiddenFromHomePage: false
hiddenFromSearch: false
twemoji: false
lightgallery: false
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
  images: ["https://ik.imagekit.io/owl4ce/id/opts~unix-shell/f"]
  # ...
---

<!--more-->

---

{{< style "text-align:justify" >}}

Memahami spesifikasi POSIX maka otomatis menguasai berbagai (Unix) *shell*. Memahami bukanlah hanya diketahui,
tetapi juga mempelajari lingkungan [*userspace* :(fas fa-arrow-up-right-from-square fa-fw):][shebang]. Mempelajari
tidak sekadar *trial-error*, melainkan diaplikasikan, guna [<u>memperkukuh</u>](#preferrable-shell-syntaxes)
paradigma dalam menyusun sebuah algoritma. Demikian, rangkuman praktis ini didedikasikan
bagi para "pragmatis" terhadap segala urusan teknis.

[shebang]: https://www.in-ulm.de/~mascheck/various/shebang "The #! magic, details about the shebang/hash-bang mechanism on various Unix flavours"

---

{{< typeit code=shell >}}
#!/usr/bin/env sh
{{< /typeit >}}

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
dash: ?: VARIABLE: $VARIABLE is unset.
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

```shell
# Alternative with (GNU) sed.
```

```bash
sed 's/(feat. .*)/(feat. Guitar Lord)/' <<< "$CURRENT_SONG" # bash herestrings.
```

{{< admonition success "/proc/self/fd/1" true >}}
Polyphia - Ego Death (feat. Guitar Lord)
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
dash: ?: cannot create /tmp/file: File exists
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

## Statements

### `if` Construction

{{< style "text-align:justify" >}}

```shell
# POSIX.1-2017: if TRUE; then CONSEQ; fi
#               if TRUE; then CONSEQ; else CONSEQ; fi
#               if TRUE; then CONSEQ; elif TRUE; then CONSEQ; else CONSEQ; fi
```

```shell
if [ -e / -a ! -d / ]; then # If root exists and is not a directory.
    echo 'Root is not a directory is an impossibility.' >&2 # I/O redirection:
elif [ -e / -a -d / ]; then # If root exists and is a directory.
    echo 'Root is a directory is a clear true.' # Output true as stdin, and
else # If either `if` and `elif` above are false (failure).
    echo 'Errors are red, your screen always blue.' >&2 # false as stderr.
fi
```

{{< admonition failure "/proc/self/fd/2" false >}}
Root is not a directory is an impossibility.
{{< /admonition >}}

{{< admonition success "/proc/self/fd/1" true >}}
Root is a directory is a clear true.
{{< /admonition >}}

{{< admonition failure "/proc/self/fd/2" false >}}
Errors are red, your screen always blue.
{{< /admonition >}}

---

{{< /style >}}

### `case` Construction

{{< style "text-align:justify" >}}

```shell
KERNEL="$(uname -s)"
```

```shell
# POSIX.1-2017: case STRING in GLOB) CONSEQ;; GLOB) CONSEQ;; esac
#               case STRING in (GLOB) CONSEQ;; (GLOB) CONSEQ;; esac
```

```shell
case "$KERNEL" in # The value of $KERNEL is Linux.
    Linux|GNU*|*BSD) echo "You are using ${KERNEL} operating system."
    ;;
         [Mm]ac*OS*) echo 'You are using 4.3BSD+Mach operating system.'
    ;;
                  *) echo 'Errors are red, your screen always blue.' >&2
    ;;
esac
```

{{< admonition success "/proc/self/fd/1" true >}}
You are using Linux operating system.
{{< /admonition >}}

{{< admonition success "/proc/self/fd/1" false >}}
You are using 4.3BSD+Mach operating system.
{{< /admonition >}}

{{< admonition failure "/proc/self/fd/2" false >}}
Errors are red, your screen always blue.
{{< /admonition >}}

---

{{< /style >}}

## Tests

### Preferrable Shell Syntaxes

#### Built-in (**faster**)

{{< style "text-align:justify" >}}

```shell
command -V 'set'
command -V 'read'
command -V '['
```

{{< admonition success "/proc/self/fd/1" true >}}
set is a special shell builtin  
read is a shell builtin  
\[ is a shell builtin
{{< /admonition >}}

---

{{< /style >}}

#### Reserved word (**fast**)

{{< style "text-align:justify" >}}

```bash
command -V 'if'
command -V 'case'
command -V '[['
```

{{< admonition success "/proc/self/fd/1" true >}}
if is a shell keyword  
case is a shell keyword  
\[\[ is a shell keyword
{{< /admonition >}}

---

{{< /style >}}

#### External program (**slow**)

{{< style "text-align:justify" >}}

```shell
command -V 'cat'
command -V 'awk'
command -V 'sed'
```

{{< admonition success "/proc/self/fd/1" true >}}
cat is /bin/cat  
awk is /usr/bin/awk  
sed is /bin/sed
{{< /admonition >}}

---

{{< /style >}}

### Tests' Expressions

{{< style "text-align:justify" >}}

| `[` / `test` | `[[` | ? |
|:---:|:---:|:---|
| `-b` file | <sup><sub>(identical)</sub></sup> | Is a block special file. |
| `-c` file | <sup><sub>(identical)</sub></sup> | Is a character special file. |
| `-d` file | <sup><sub>(identical)</sub></sup> | Is a directory. |
| `-e` file | <sup><sub>(identical)</sub></sup> | Is a file or directory (exists). |
| `-f` file | <sup><sub>(identical)</sub></sup> | Is a file. |
| `-g` file | <sup><sub>(identical)</sub></sup> | Is a file with SGID. |
| `-G` file | <sup><sub>(identical)</sub></sup> | Is a file with effective group id from the current process. |
| `-h` file <br> `-L` file | <sup><sub>(identical)</sub></sup> | Is a symbolic link. |
| `-k` file | <sup><sub>(identical)</sub></sup> | Is a file with sticky bit. |
| `-O` file | <sup><sub>(identical)</sub></sup> | Is a file with effective user id from the current process. |
| `-p` file | <sup><sub>(identical)</sub></sup> | Is a named pipe (FIFO). |
| `-r` file | <sup><sub>(identical)</sub></sup> | Is a readable file. |
| `-s` file | <sup><sub>(identical)</sub></sup> | File size is not or greater than null. |
| `-S` file | <sup><sub>(identical)</sub></sup> | Is an Unix socket. |
| `-t` fdN | <sup><sub>(identical)</sub></sup> | Is an open file descriptor which connected. |
| `-u` file | <sup><sub>(identical)</sub></sup> | Is a file with SUID. |
| `-w` file | <sup><sub>(identical)</sub></sup> | Is a writable file, based on permission bit. |
| `-x` file | <sup><sub>(identical)</sub></sup> | Is an executable file, based on permission bit. |
| <sup><sub>file</sub></sup>1 `-nt` <sup><sub>file</sub></sup>2 | <sup><sub>(identical)</sub></sup> | 1st file is newer than the 2nd. |
| <sup><sub>file</sub></sup>1 `-ot` <sup><sub>file</sub></sup>2 | <sup><sub>(identical)</sub></sup> | 1st file is older than the 2nd. |
| <sup><sub>file</sub></sup>1 `-ef` <sup><sub>file</sub></sup>2 | <sup><sub>(identical)</sub></sup> | Both files are the same file. |
| `-n` string | <sup><sub>(identical)</sub></sup> | String length is not or greater than null. |
| `-z` string | <sup><sub>(identical)</sub></sup> | String length is null. |
| <sup><sub>string</sub></sup>1 `=` <sup><sub>string</sub></sup>2 | `==` | Both strings are equal. Inside `[[` `]]`, globbing supported. |
| <sup><sub>(none)</sub></sup> | `=~` | Both strings are equal, based on regular expression. |
| <sup><sub>string</sub></sup>1 `!=` <sup><sub>string</sub></sup>2 | <sup><sub>(identical)</sub></sup> | Both strings are not equal. |
| <sup><sub>string</sub></sup>1 `\<` <sup><sub>string</sub></sup>2 | `<` | 1st string before the 2nd, lexicographically. |
| <sup><sub>string</sub></sup>1 `\>` <sup><sub>string</sub></sup>2 | `>` | 1st string after the 2nd, lexicographically. |
| <sup><sub>integer</sub></sup>1 `-eq` <sup><sub>integer</sub></sup>2 | <sup><sub>(identical)</sub></sup> | Both integers are equal, algebraically. |
| <sup><sub>integer</sub></sup>1 `-ne` <sup><sub>integer</sub></sup>2 | <sup><sub>(identical)</sub></sup> | Both integers are not equal, algebraically. |
| <sup><sub>integer</sub></sup>1 `-gt` <sup><sub>integer</sub></sup>2 | <sup><sub>(identical)</sub></sup> | 1st integer is greater than the 2nd, algebraically. |
| <sup><sub>integer</sub></sup>1 `-ge` <sup><sub>integer</sub></sup>2 | <sup><sub>(identical)</sub></sup> | 1st integer is greater than or equal to the 2nd, algebraically. |
| <sup><sub>integer</sub></sup>1 `-lt` <sup><sub>integer</sub></sup>2 | <sup><sub>(identical)</sub></sup> | 1st integer is smaller than the 2nd, algebraically. |
| <sup><sub>integer</sub></sup>1 `-le` <sup><sub>integer</sub></sup>2 | <sup><sub>(identical)</sub></sup> | 1st integer is smaller than or equal to the 2nd, algebraically. |
| `!` expression | <sup><sub>(identical)</sub></sup> | Inverts true/false values of the expression's exit status. |
| `\(` expression `\)` | `( )` | Groups multiple expressions, with final expression value. |
| <sup><sub>expression</sub></sup>1 `-a` <sup><sub>expression</sub></sup>2 | `&&` | Execute next expression if the previous expression is true. |
| <sup><sub>expression</sub></sup>1 `-o` <sup><sub>expression</sub></sup>2 | `\|\|` | Execute next expression if the previous expression is false. |

---

{{< /style >}}

### `[` Built-in

{{< style "text-align:justify" >}}

```shell
SOCKET="${HOME}/.urxvt/urxvtd-localh3art"
```

```shell
# POSIX.1-2017: [ EXPRESSIONS ]
#               test EXPRESSIONS
```

```shell
[ \( -n "$SOCKET" -o ! -z "$SOCKET" \) -a \( -e "$SOCKET" -o -S "$SOCKET" \) ]
```

```shell
{ [ "$?" -eq 0 ] || [ ! "$?" -gt 0 ]; } && file "$SOCKET" # Grouped.
```

{{< admonition success "/proc/self/fd/1" true >}}
/home/rachel/.urxvt/urxvtd-localh3art: socket
{{< /admonition >}}

---

```shell
QUEEN='Lucy (Kaede)'
```

```shell
[ $QUEEN = 'Lucy (Kaede)' ] && echo "$QUEEN" # Inside [ ], need to be quoted.
```

{{< admonition failure "/proc/self/fd/2" true >}}
dash: ?: \[: Lucy: unexpected operator
{{< /admonition >}}

---

{{< /style >}}

#### `test`

{{< style "text-align:justify" >}}

```shell
test -t 0 -a -h "/proc/$$/fd/0" && file "${_%%/fd*}/exe"
```

{{< admonition success "/proc/self/fd/1" true >}}
/proc/1337/exe: symbolic link to /bin/dash
{{< /admonition >}}

---

{{< /style >}}

### `[[` Keyword

{{< style "text-align:justify" >}}

```shell
# ksh, bash, zsh, yash, busybox sh: [[ EXPRESSIONS ]]
```

```bash
[[ ( -n "$SOCKET" || ! -z "$SOCKET" ) && ( -e "$SOCKET" || -S "$SOCKET" ) ]]
```

```bash
[[ "$?" -eq 0 || "$?" -gt '1 / -1' ]] && file "$SOCKET" # Arithmetic supported.
```

{{< admonition success "/proc/self/fd/1" true >}}
/home/rachel/.urxvt/urxvtd-localh3art: socket
{{< /admonition >}}

---

```bash
[[ $QUEEN = [A-Za-z]*\ * ]] && echo "$QUEEN" # Inside [[ ]], no need to quote.
```

{{< admonition success "/proc/self/fd/1" true >}}
Lucy (Kaede)
{{< /admonition >}}

---

{{< /style >}}

## Strings

### File Format Notation

{{< style "text-align:justify" >}}

[POSIX.1-2017](https://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap05.html#tagtcjh_2)

---

{{< /style >}}

### Escape Sequences

{{< style "text-align:justify" >}}

| POSIX <br><sup><sub>(+extensions)</sub></sup> | bash <br><sup><sub>(and others)</sub></sup> | ? |
|:---:|:---:|:---|
| `\a` | <sup><sub>(identical)</sub></sup> | To hide warning, denoted with bell character. |
| `\b` | <sup><sub>(identical)</sub></sup> | As backspace character. |
| `\c` | <sup><sub>(identical)</sub></sup> | To suppress more output. Usually used at the end of argument. |
| <sup><sub>(none)</sub></sup> | `\e` <br> `\E` | As [escape character](https://gist.github.com/fnky/458719343aabd01cfb17a3a4f7296797). Alternatively octal 8-bit (`\033`), 2 digits. |
| `\f` | <sup><sub>(identical)</sub></sup> | As form feed character. |
| `\n` | <sup><sub>(identical)</sub></sup> | As newline character. |
| `\r` | <sup><sub>(identical)</sub></sup> | As carriage return character. |
| `\t` | <sup><sub>(identical)</sub></sup> | As horizontal tab character. |
| `\v` | <sup><sub>(identical)</sub></sup> | As vertical tab character. |
| `\\` | <sup><sub>(identical)</sub></sup> | As backslash character. |
| `\0nnn` | <sup><sub>(identical)</sub></sup> | As octal 8-bit character (`nnn`), 0-3 digits. |
| <sup><sub>(none)</sub></sup> | `\xHH` | As hexadecimal 8-bit character (`HH`), 1-2 digits. |
| <sup><sub>(none)</sub></sup> | `\uHHHH` | As hexadecimal unicode character (`HHHH`), 1-4 digits. |
| <sup><sub>(none)</sub></sup> | `\UHHHHHHHH` | As hexadecimal unicode character (`HHHHHHHH`), 1-8 digits. |

---

{{< /style >}}

### Fancy `printf`

{{< style "text-align:justify" >}}

```shell
# POSIX.1-2017: printf FILE_FORMAT_NOTATION ARG1 ARG2 ARGS
```

```shell
printf '%.7s\n' 'My Last Farewell' # Cut 7 bytes string.
```

{{< admonition success "/proc/self/fd/1" true >}}
My Last
{{< /admonition >}}

---

```shell
printf '%X\n' "$((50*255/100))" # Calculate 50% alpha, decimal into hexadecimal.
```

{{< admonition success "/proc/self/fd/1" true >}}
7F
{{< /admonition >}}

---

```shell
printf '%.16f\n' "$((77/7))e-1" # Tricky 7.7/7 floating-point arithmetic.
```

{{< admonition success "/proc/self/fd/1" true >}}
1.1000000000000001
{{< /admonition >}}

---

{{< /style >}}

### Plain `echo`

{{< style "text-align:justify" >}}

```shell
# POSIX.1-2017: echo STRINGS
```

```shell
echo 'My Last Farewell' | cut -b1-7 # pipe to cut (from GNU coreutils).
```

{{< admonition success "/proc/self/fd/1" true >}}
My Last
{{< /admonition >}}

---

```shell
echo "ibase=10; obase=16; $((50*255/100))" | bc # pipe to (POSIX) bc.
```

{{< admonition success "/proc/self/fd/1" true >}}
7F
{{< /admonition >}}

```shell
# zsh 5+: Arithmetic Evaluation
```

```shell
echo "$(([##16]50*255/100))"
```

{{< admonition success "/proc/self/fd/1" true >}}
7F
{{< /admonition >}}

---

```shell
echo '7.7/7' | bc -l # pipe to (POSIX) bc.
```

{{< admonition success "/proc/self/fd/1" true >}}
1.10000000000000000000
{{< /admonition >}}

```shell
# ksh93, zsh, yash: $((X.Y/Z))
```

```shell
echo "$((7.7/7))"
```

{{< admonition success "/proc/self/fd/1" true >}}
1.1000000000000001
{{< /admonition >}}

---

{{< /style >}}

## Refs

{{< style "text-align:justify" >}}

1. Manpage: dash([1](https://linux.die.net/man/1/dash))
2. Manpage: [bash](https://gnu.org/software/bash/manual/bash.html)([1](https://linux.die.net/man/1/bash))
3. Manpage: [zsh](https://zsh.sourceforge.io/Doc/Release/zsh_toc.html)([1](https://linux.die.net/man/1/zsh))
4. Article: [Bashism](https://mywiki.wooledge.org/Bashism)
5. Specs: [POSIX.1-2017](https://pubs.opengroup.org/onlinepubs/9699919799)
6. Book: [Pure /bin/sh](https://github.com/dylanaraps/pure-sh-bible)
7. Book: [Pure bash](https://github.com/dylanaraps/pure-bash-bible)

{{< /style >}}
