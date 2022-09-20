---
tags: Note
---

# Bash Note

[TOC]

## source data

- https://superuser.com/questions/522714/in-zsh-how-can-i-run-a-script-which-is-written-for-bash
- https://www.cyberciti.biz/faq/bash-for-loop/
- https://linuxhint.com/bash_loop_list_strings/

## loop

### for

```bash=
music_url[0]="https://youtu.be/KhV57_EH3AA" # 猛毒來襲
music_url[1]="https://youtu.be/eq8r1ZTma08" # 被生命厭惡著
music_url[2]="https://youtu.be/olWvy0PiLfA" # ツユ - くらべられっ子

for((i=0; i<${#music_url[@]}; i++))

do
    eval "youtube-dl -x --audio-format mp3 ${music_url[i]}"
done
```