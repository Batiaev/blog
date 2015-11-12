---
layout: post
title:  "Crib on vim"
date:   2015-03-31 18:32:11
categories: vim linux terminal
---


- Open file 	`vim file.txt`

###Commands
- `:e <scp|ftp|ftps>://user@host/path/to/the/file.txt` - Edit file
- `:e ./` or `Ex` - File manager 	
- `: <n>` - Move on line <n> 	
- `:w <filename>` - Write changes
- `:wa` - Write changes on all files
- `:q` - Exit from editor
- `:q!` - Exit without changes
- `!<cmd>` - Execute commang
- `:syntax on` - Enable syntax
- `:syntax off` - Disable syntax
- `:set number` - Show row number
- `:g/^$/d` - delete all empty strings
- `:s/source_string/result_string/g` - Replase source_string on result_string
- `Ctrl + N` - autocompletion
- `:abbr Lunix Linux` - error correction
- `/` - search
- `?` - search above
- `:set list` show whitespace symbols <span class="label label-primary">UPD: <time datetime="2015-11-12">2015-11-12</time></span>
- `:set nolist` hide whitespace symbols <span class="label label-primary">UPD: <time datetime="2015-11-12">2015-11-12</time></span>


###Moving
- `h` - left
- `l` - right
- `j` - down
- `k` - up
- `|`, `0`, `home` — start line
- `^` — first not empty symbol in line
- `$`, `end` — end of line
- `m` — middle of screen widht
- `g` — bottom line
- `e` - end of word
- `-` - first not empty symbol on line about
- `G` - latest line
- `H` — first line on screen
- `M` — middle line on screen
- `L` — latest line on screen
- `w` — next word
- `b` — previous word

###Modes
- `v` - visual mode
- `:` - command mode