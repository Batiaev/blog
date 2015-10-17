---
layout: post
title:  "Статический анализатор исходного кода Cppcheck"
date:   2013-06-15 23:43:31
categories: analyzer, cplusplus, CppCheck, IT 
---
Официальный сайт : http://cppcheck.sf.net/

###Установка

`# sudo aptitude install cppckeck`

###Синтаксис:

`cppcheck [опции] [файл или папка]`

Если вместо имени файла будет задана директория значит будут проверяться рекурсивно все файлы в этой директории с разрешениями: *.cpp, *.cxx, *.cc, *.c++, *.c, *.tpp, and *.txx.

###Список опций команды cppcheck:

`user@user-desktop:~$ cppcheck --help`

 - `--append=<file>` - This allows you to provide information about functions by providing an implementation for them.

 - `--check-config` - Check cppcheck configuration. The normal code analysis is disabled by this flag.

 - `-D<ID>` - By default Cppcheck checks all configurations. Use '-D' to limit the checking. When '-D' is used the checking is limited to the given configuration.
Example: `'-DDEBUG=1 -D__cplusplus'`.

 - `-U<ID>` - By default Cppcheck checks all configurations. Use '-U' to explicitly hide certain #ifdef <ID> code paths from checking.
Example: '-UDEBUG'

 -  `--enable=<id>` - Enable additional checks. The available ids are:

    - all - Enable all checks
    - style - Enable all coding style checks. All messages with the severities 'style', 'performance' and 'portability' are enabled.
    - performance - Enable performance messages
    - portability - Enable portability messages
    - information - Enable information messages
    - unusedFunction - Check for unused functions
    - missingInclude - Warn if there are missing includes. For detailed information, use '--check-config'.

Several ids can be given if you separate them with commas.

 - `--error-exitcode=<n>` - If errors are found, integer [n] is returned instead of the default '0'. '1' is returned if arguments are not valid or if no input files are provided. Note that your operating system can modify this value, e.g. '256' can become '0'.

 - `--errorlist` - Print a list of all the error messages in XML format.

 - `--exitcode-suppressions=<file>` - Used when certain messages should be displayed but should not cause a non-zero exitcode.

 - `--file-list=<file>` - Specify the files to check in a text file. Add one filename per line. When file is '-,' the file list will be read from standard input.

 - `-f, --force` - Force checking of all configurations in files. If used together with '--max-ifdefs=', the last option is the one that is effective.

 - `-h, --help` - Print this help.

 - `-I <dir>` - Give path to search for include files. Give several -I parameters to give several paths. First given path is searched for contained header files first. If paths are relative to source files, this is not needed.

 - `--includes-file=<file>` - Specify directory paths to search for included header files in a text file. Add one include path per line. First given path is searched for contained header files first. If paths are relative to source files, this is not needed.

 - `-i <dir or file>` - Give a source file or source file directory to exclude from the check. This applies only to source files so header files included by source files are not matched. Directory name is matched to all parts of the path.

 - `--inline-suppr` - Enable inline suppressions. Use them by placing one or more comments, like: '// cppcheck-suppress warningId' on the lines before the warning to suppress.

 - `-j <jobs>` - Start [jobs] threads to do the checking simultaneously.

 - `--max-configs=<limit>` - Maximum number of configurations to check in a file before skipping it. Default is '12'. If used together with '--force', the last option is the one that is effective.

 - `--platform=<type>` - Specifies platform specific types and sizes. The available platforms are:

    unix32 - 32 bit unix variant
    unix64 - 64 bit unix variant
    win32A - 32 bit Windows ASCII character encoding
    win32W - 32 bit Windows UNICODE character encoding
    win64 - 64 bit Windows


 - `-q, --quiet` - Only print error messages.

 - `--report-progress` - Report progress messages while checking a file.

 - `--rule=<rule>` - Match regular expression.

 - `--rule-file=<file>` - Use given rule file. For more information, see:
https://sourceforge.net/projects/cppcheck/files/Articles/

 - `-s, --style` - Deprecated, please use '--enable=style' instead

 - `--std=<id>` - Environment. The available options are:

    posix - Use this if a posix environment is available
    c99 - Use this if the compiler is C99 compatible
    c++11 - Use this if the compiler is C++11 compatible. note: you probably want to also use 'c99'.


 - `--suppress=<spec>` - Suppress warnings that match <spec>. The format of <spec> is:
[error id]:[filename]:[line]
The [filename] and [line] are optional. If [error id] is a wildcard '*', all error ids match.

 - `--suppressions-list=<file>` - Suppress warnings listed in the file. Each suppression is in the same format as <spec> above.

 - `--template='<text>'` - Format the error messages. E.g.
'{file}:{line},{severity},{id},{message}' or
'{file}({line}):({severity}) {message}'
Pre-defined templates: gcc, vs, edit.

 - `-v, --verbose` - Output more detailed error information.

 - `--version`  - Print out version number.

 - `--xml` - Write results in xml format to error stream (stderr).

 - `--xml-version=<version>` - Select the XML file version. Currently versions 1 and 2 are available. The default version is 1.

###Example usage:

Recursively check the current folder. Print the progress on the screen and write errors to a file:
    
    cppcheck . 2> err.txt

Recursively check ../myproject/ and don't print progress:

    cppcheck --quiet ../myproject/

Check only files one.cpp and two.cpp and give all information there is:

    cppcheck -v -s one.cpp two.cpp

Check f.cpp and search include files from inc1/ and inc2/:

    cppcheck -I inc1/ -I inc2/ f.cpp

For more information: http://cppcheck.sf.net/manual.pdf