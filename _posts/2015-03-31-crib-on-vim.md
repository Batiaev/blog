---
layout: post
title:  "Crib on vim"
date:   2015-03-31 18:32:11
categories: vim linux terminal
---

- Open file 	`vim file.txt`

###Commands
- Edit file 	`:e <scp|ftp|ftps>://user@host/path/to/the/file.txt`
- File manager 	`:e ./` or `Ex`
- Move on line <n> 	`: <n>`
- Write changes 	`:w <filename>`
- Write changes on all files 	`:wa`
- Exit from editor 	`:q`
- Exit without changes 	`:q!`
- Execute commang 	`!<cmd>`
- Enable syntax 	`:syntax on`
- Disable syntax 	`:syntax off`
- Show row number 	`:set number`

- Grep
 `:g/pattern/d`
 `:g/^$/d` - delete all empty strings
- Search
 `:s/source_string/result_string/g`

###Modes
- `v` - visual mode
- `:` - command mode