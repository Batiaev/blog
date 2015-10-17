---
layout: post
title:  "Выявление ошибок работы с памятью при помощи Valgrind"
date:   2013-05-13 23:26:31
categories: analyzer, linux, memcheck, memoryLeaks, Valgrind, IT
---
Официальный сайт: http://valgrind.org/

Valgrind имеет модульную архитектуру, и состоит из ядра, которое выполняет эмуляцию процессора, а конкретные модули выполняют сбор и анализ информации, полученной во время выполнения кода на эмуляторе. Valgrind работает под управлением ОС Linux на процессорах x86, amd64, ppc32 и ppc64, при этом существуют некоторые ограничения, которые потенциально могут повлиять на работу исследуемых программ.

В поставку valgrind входят следующие модули-анализаторы:

 - `memcheck` - основной модуль, обеспечивающий обнаружение утечек памяти, и прочих ошибок, связанных с неправильной работой с областями памяти -- чтением или записью за пределами выделенных регионов и т.п.
 - `cachegrind` - анализирует выполнение кода, собирая данные о (не)попаданиях в кэш, и точках перехода (когда процессор неправильно предсказывает ветвление). Эта статистика собирается для всей программы, отдельных функций и строк кода
 - `callgrind` - анализирует вызовы функций, используя примерно ту же методику, что и модуль cachegrind. Позволяет построить дерево вызовов функций, и соответственно, проанализировать узкие места в работе программы
 - `massif` - позволяет проанализировать выделение памяти различными частями программы
 - `helgrind` - анализирует выполняемый код на наличие различных ошибок синхронизации, при использовании многопоточного кода, использующего POSIX Threads

Установка

`# sudo aptitude install valgrind`

Синтаксис:

`valgrind [опции] программа_и_аргументы`

Список опций команды valgrind:

`$ valgrind --help`

 - `--tool=<name>`             use the Valgrind tool named <name> [memcheck]
 - `-h --help`                 show this message
 - `--help-debug`              show this message, plus debugging options
 - `--version`                 show version
 - `-q --quiet`                run silently; only print error msgs
 - `-v --verbose`              be more verbose -- show misc extra info
 - `--trace-children=no|yes`   Valgrind-ise child processes (follow execve)? [no]
 - `--trace-children-skip=patt1,patt2,...`    specifies a list of executables
                                that `--trace-children=yes` should not trace into
 - `--trace-children-skip-by-arg=patt1,patt2,...`   same as --trace-children-skip=
                                but check the argv[] entries for children, rather
                                than the exe name, to make a follow/no-follow decision
 - `--child-silent-after-fork=no|yes` omit child output between fork & exec? [no]
 - `--vgdb=no|yes|full`        activate gdbserver? [yes]
                                full is slower but provides precise watchpoint/step
 - `--vgdb-error=<number>`     invoke gdbserver after <number> errors [999999999]
                                to get started quickly, use --vgdb-error=0
                                and follow the on-screen directions
 - `--track-fds=no|yes`        track open file descriptors? [no]
 - `--time-stamp=no|yes`       add timestamps to log messages? [no]
 - `--log-fd=<number>`         log messages to file descriptor [2=stderr]
 - `--log-file=<file>`         log messages to <file>
 - `--log-socket=ipaddr:port`  log messages to socket ipaddr:port

    user options for Valgrind tools that report errors:
 - `--xml=yes`                 emit error output in XML (some tools only)
 - `--xml-fd=<number>`         XML output to file descriptor
 - `--xml-file=<file>`         XML output to <file>
 - `--xml-socket=ipaddr:port`  XML output to socket ipaddr:port
 - `--xml-user-comment=STR`    copy STR verbatim into XML output
 - `--demangle=no|yes`         automatically demangle C++ names? [yes]
 - `--num-callers=<number>`    show <number> callers in stack traces [12]
 - `--error-limit=no|yes`      stop showing new errors if too many? [yes]
 - `--error-exitcode=<number>` exit code to return if errors found [0=disable]
 - `--show-below-main=no|yes`  continue stack traces below main() [no]
 - `--suppressions=<filename>` suppress errors described in <filename>
 - `--gen-suppressions=no|yes|all`    print suppressions for errors? [no]
 - `--db-attach=no|yes`        start debugger when errors detected? [no]
 - `--db-command=<command>`    command to start debugger [/usr/bin/gdb -nw %f %p]
 - `--input-fd=<number>`       file descriptor for input [0=stdin]
 - `--dsymutil=no|yes`         run dsymutil on Mac OS X when helpful? [no]
 - `--max-stackframe=<number>` assume stack switch for SP changes larger
                                than <number> bytes [2000000]
 - `--main-stacksize=<number>` set size of main thread's stack (in bytes)
                                [use current 'ulimit' value]

    user options for Valgrind tools that replace malloc:
 - `--alignment=<number>`      set minimum alignment of heap allocations [16]

    uncommon user options for all Valgrind tools:
 - `--fullpath-after=`         (with nothing after the '=')
                                show full source paths in call stacks
 - `--fullpath-after=string`   like --fullpath-after=, but only show the
                                part of the path after 'string'.  Allows removal
                                of path prefixes.  Use this flag multiple times
                                to specify a set of prefixes to remove.
 - `--smc-check=none|stack|all|all-non-file` [stack]
                                checks for self-modifying code: none, only for
                                code found in stacks, for all code, or for all
                                code except that from file-backed mappings
 - `--read-var-info=yes|no`    read debug info on stack and global variables
                                and use it to print better error messages in
                                tools that make use of it (Memcheck, Helgrind,
                                DRD) [no]
 - `--vgdb-poll=<number>`      gdbserver poll max every <number> basic blocks [5000] 
 - `--vgdb-shadow-registers=no|yes`   let gdb see the shadow registers [no]
 - `--vgdb-prefix=<prefix>`    prefix for vgdb FIFOs [/tmp/vgdb-pipe]
 - `--run-libc-freeres=no|yes` free up glibc memory at exit on Linux? [yes]
 - `--sim-hints=hint1,hint2,...`  known hints:
                                   lax-ioctls, enable-outer, fuse-compatible [none]
 - `--kernel-variant=variant1,variant2,...`  known variants: bproc [none]
                                handle non-standard kernel variants
 - `--show-emwarns=no|yes`     show warnings about emulation limits? [no]
 - `--require-text-symbol=:sonamepattern:symbolpattern`    abort run if the
                                stated shared object doesn't have the stated
                                text symbol.  Patterns can contain ? and *.

    user options for Memcheck:
 - `--leak-check=no|summary|full`     search for memory leaks at exit?  [summary]
 - `--leak-resolution=low|med|high`   differentiation of leak stack traces [high]
 - `--show-reachable=no|yes`          show reachable blocks in leak check? [no]
 - `--show-possibly-lost=no|yes`      show possibly lost blocks in leak check?
                                       [yes]
 - `--undef-value-errors=no|yes`      check for undefined value errors [yes]
 - `--track-origins=no|yes`           show origins of undefined values? [no]
 - `--partial-loads-ok=no|yes`        too hard to explain here; see manual [no]
 - `--freelist-vol=<number>`          volume of freed blocks queue      [20000000]
 - `--freelist-big-blocks=<number>`   releases first blocks with size >= [1000000]
 - `--workaround-gcc296-bugs=no|yes`  self explanatory [no]
 - `--ignore-ranges=0xPP-0xQQ[,0xRR-0xSS]`   assume given addresses are OK
 - `--malloc-fill=<hexnumber>`        fill malloc'd areas with given value
 - `--free-fill=<hexnumber>`          fill free'd areas with given value
