
Ed with Syntax Highlighting - A simple ed fork by Mathias Fuchs 2022.

Based on ed 1.18 and GNU source-highlight for C/C++ on a linux console with ANSI escape sequences.

GPLv2.

![screenshot](screenshot.png)

I added the files sh.cpp and sh.h to the original ed sources, and modified the function print_line in io.c slighty.

To avoid headache, I had to remove the autotools files, and the test suite :).
Instead, building happens from a hand-written simplistic Makefile for Linux instead.
Assumes the GNU source-highlight library is installed and available for inclusion and linking, for instance from the package manager.

To build, for instance on Ubuntu/Debian, do

```
sudo apt install libsource-highlight-dev
make
```

Feel free to add other languages than C/C++ etc.



Part of the original ed README below.


Description

GNU ed is a line-oriented text editor. It is used to create, display, modify
and otherwise manipulate text files, both interactively and via shell
scripts. A restricted version of ed, red, can only edit files in the current
directory and cannot execute shell commands. Ed is the 'standard' text
editor in the sense that it is the original editor for Unix, and thus widely
available. For most purposes, however, it is superseded by full-screen
editors such as GNU Emacs or GNU Moe.

Extensions to and deviations from the POSIX standard are described below.

See the file INSTALL for compilation and installation instructions.

Try 'ed --help' for usage instructions.

Report bugs to bug-ed@gnu.org

Ed home page: http://www.gnu.org/software/ed/ed.html

For a description of the ed algorithm, see Brian W. Kernighan and
P. J. Plauger's book "Software Tools in Pascal", Addison-Wesley, 1981.

GNU ed(1) is not strictly POSIX compliant, as described in the
POSIX 1003.1-2004 document. The following is a summary of omissions and
extensions to, and deviations from, the POSIX standard.

OMISSIONS
---------
  * Locale(3) is not supported.

EXTENSIONS
----------
  * Though GNU ed is not a stream editor, it can be used to edit binary files.
    To assist in binary editing, when a file containing at least one ASCII
    NUL character is written, a newline is not appended if it did not
    already contain one upon reading. If the last line has been modified,
    reading an empty file, for example /dev/null, prior to writing prevents
    appending a newline to a binary file.

    For example, to create a file with GNU ed containing a single NUL character:
      $ ed file
      a
      ^@
      .
      r /dev/null
      wq

    Similarly, to remove a newline from the end of binary 'file':
      $ ed file
      r /dev/null
      wq

  * BSD commands have been implemented wherever they do not conflict with
    the POSIX standard.  The BSD-ism's included are:
      * 's' (i.e., s[1-9rgp]*) to repeat a previous substitution,
      * 'W' for appending text to an existing file,
      * 'wq' for exiting after a write, and
      * 'z' for scrolling through the buffer.

  * The POSIX interactive global commands 'G' and 'V' are extended to
    support multiple commands, including 'a', 'i' and 'c'.  The command
    format is the same as for the global commands 'g' and 'v', i.e., one
    command per line with each line, except for the last, ending in a
    backslash (\).

  * The file commands 'E', 'e', 'r', 'W' and 'w'  process a <file>
    argument for backslash escapes; i.e., any character preceded by a
    backslash is interpreted literally. If the first character of a <file>
    argument is a bang (!), then the rest of the line is interpreted as a
    shell command, and no escape processing is performed by GNU ed.

  * For SunOS ed(1) compatibility, GNU ed runs in restricted mode if invoked
    as red.  This limits editing of files in the local directory only and
    prohibits shell commands.

DEVIATIONS
----------
  * To support the BSD 's' command (see EXTENSIONS above), substitution
    patterns cannot be delimited by the digits '1' to '9' or by the
    characters 'r', 'g' and 'p'. In contrast, POSIX specifies that any
    character except space and newline can be used as a delimiter.

  * Since the behavior of 'u' (undo) within a 'g' (global) command list is
    not specified by POSIX, GNU ed follows the behavior of the SunOS ed:
    undo forces a global command list to be executed only once, rather than
    for each line matching a global pattern.  In addtion, each instance of
    'u' within a global command undoes all previous commands (including
    undo's) in the command list.  This seems the best way, since the
    alternatives are either too complicated to implement or too confusing
    to use.

  * The 'm' (move) command within a 'g' command list also follows the SunOS
    ed implementation: any lines moved are removed from the global command's
    'active' list.

  * For backwards compatibility, errors in piped scripts do not force ed
    to exit.  POSIX only specifies ed's response for input via regular
    files (including here documents) or tty's.



Copyright (C) 1993, 1994 Andrew Moore
Copyright (C) 2006-2022 Antonio Diaz Diaz.
Copyright (C) 2022 syntax highlighting fork Mathias Fuchs

This file is free documentation: you have unlimited permission to copy,
distribute, and modify it.

The file Makefile.in is a data file used by configure to produce the
Makefile. It has the same copyright owner and permissions that configure
itself.
