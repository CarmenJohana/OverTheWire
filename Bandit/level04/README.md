# Preliminaries

In this level, we are told that the password is stored in the only human-readable file in the *inhere* directory.

When we enter this level, the only visible directory inside */home/bandit3* is *inhere*. Using *ls -l*, we can see there are many files named *-file0i* with *i = 0, ..., 9*. I expected the *-l* flag would show some useful properties — and it does, but not the ones we need here.

# Commands used

To find a way to determine the file type, I use the command:

*man -k "file type"*


From the results, the *file* command stood out. Its manual page begins with:

       This manual page documents version 5.45 of the file command.

       file  tests  each  argument  in  an  attempt to classify it.  There are three sets of
       tests, performed in this order: filesystem tests, magic tests,  and  language  tests.
       The first test that succeeds causes the file type to be printed.

       The  type  printed will usually contain one of the words text (the file contains only
       printing characters and a few common control characters and is probably safe to  read
       on  an  ASCII terminal), executable (the file contains the result of compiling a pro‐
       gram in a form understandable to some UNIX kernel or another), or data  meaning  any‐
       thing  else  (data  is usually “binary” or non-printable).  Exceptions are well-known
       file formats (core files, tar archives) that are known to contain binary data.   When
       modifying  magic  files  or the program itself, make sure to preserve these keywords.
       Users depend on knowing that all the readable files in  a  directory  have  the  word
       “text”  printed.  Don't do as Berkeley did and change “shell commands text” to “shell
       script”.

       The filesystem tests are based on examining the return from a  stat(2)  system  call.
       The program checks to see if the file is empty, or if it's some sort of special file.
       Any  known file types appropriate to the system you are running on (sockets, symbolic
       links, or named pipes (FIFOs) on those systems that implement them) are  intuited  if
       they are defined in the system header file <sys/stat.h>.

       The  magic  tests  are used to check for files with data in particular fixed formats.
       The canonical example of this is a binary executable (compiled program)  a.out  file,
       whose  format  is defined in <elf.h>, <a.out.h> and possibly <exec.h> in the standard
       include directory.  These files have a “magic number” stored in  a  particular  place
       near  the beginning of the file that tells the UNIX operating system that the file is
       a binary executable, and which of several types thereof.  The  concept  of  a  “magic
       number”  has  been  applied by extension to data files.  Any file with some invariant
       identifier at a small fixed offset into the file can usually  be  described  in  this
       way.   The  information  identifying these files is read from /etc/magic and the com‐
       piled  magic  file  /usr/share/misc/magic.mgc,  or  the  files   in   the   directory
       /usr/share/misc/magic  if  the  compiled  file  does  not  exist.   In  addition,  if
       $HOME/.magic.mgc or $HOME/.magic exists, it will be used in preference to the  system
       magic files.

       If  a file does not match any of the entries in the magic file, it is examined to see
       if it seems to be a text file.  ASCII, ISO-8859-x, non-ISO 8-bit extended-ASCII char‐
       acter sets (such as those used on Macintosh and IBM PC systems),  UTF-8-encoded  Uni‐
       code,  UTF-16-encoded  Unicode, and EBCDIC character sets can be distinguished by the
       different ranges and sequences of bytes that constitute printable text in  each  set.
       If  a  file  passes  any  of  these  tests,  its  character  set is reported.  ASCII,
       ISO-8859-x, UTF-8, and extended-ASCII files are identified  as  “text”  because  they
       will be mostly readable on nearly any terminal; UTF-16 and EBCDIC are only “character
       data”  because, while they contain text, it is text that will require translation be‐
       fore it can be read.  In addition, file will attempt to determine other  characteris‐
       tics  of text-type files.  If the lines of a file are terminated by CR, CRLF, or NEL,
       instead of the Unix-standard LF, this will be reported.  Files that contain  embedded
       escape sequences or overstriking will also be identified.

       Once  file has determined the character set used in a text-type file, it will attempt
       to determine in what language the file is written.  The language tests look for  par‐
       ticular  strings (cf.  <names.h>) that can appear anywhere in the first few blocks of
       a file.  For example, the keyword .br indicates  that  the  file  is  most  likely  a
       troff(1)  input  file, just as the keyword struct indicates a C program.  These tests
       are less reliable than the previous two groups, so they are performed last.  The lan‐
       guage test routines also test for some miscellany  (such  as  tar(1)  archives,  JSON
       files).

       Any  file  that  cannot  be identified as having been written in any of the character
       sets listed above is simply said to be “data”.

From this, I understood that human-readable essentially means a file identified as text — for example, an ASCII text file containing characters most people can recognize.
(Here’s a related discussion on LinuxQuestions: https://www.linuxquestions.org/questions/slackware-14/what-is-the-difference-between-ascii-english-text-and-ascii-text-895403/).

However, running file ./-file00 for each file manually would be tedious.

Then I remembered something from the bash manual page under Pattern Matching:

Pattern Matching

       Any character that appears in a pattern, other than the special
       pattern characters described below, matches itself.  The NUL
       character may not occur in a pattern.  A backslash escapes the
       following character; the escaping backslash is discarded when
       matching.  The special pattern characters must be quoted if they
       are to be matched literally.

       The special pattern characters have the following meanings:

              *      Matches any string, including the null string.  When
                     the globstar shell option is enabled, and * is used
                     in a pathname expansion context, two adjacent *s
                     used as a single pattern will match all files and
                     zero or more directories and subdirectories.  If
                     followed by a /, two adjacent *s will match only
                     directories and subdirectories.
              ?      Matches any single character.
              [...]  Matches any one of the enclosed characters.  A pair
                     of characters separated by a hyphen denotes a range
                     expression; any character that falls between those
                     two characters, inclusive, using the current
                     locale's collating sequence and character set, is
                     matched.  If the first character following the [ is
                     a !  or a ^ then any character not enclosed is
                     matched.  The sorting order of characters in range
                     expressions, and the characters included in the
                     range, are determined by the current locale and the
                     values of the LC_COLLATE or LC_ALL shell variables,
                     if set.  To obtain the traditional interpretation of
                     range expressions, where [a-d] is equivalent to
                     [abcd], set value of the LC_ALL shell variable to C,
                     or enable the globasciiranges shell option.  A - may
                     be matched by including it as the first or last
                     character in the set.  A ] may be matched by
                     including it as the first character in the set.

                     Within [ and ], character classes can be specified
                     using the syntax [:class:], where class is one of
                     the following classes defined in the POSIX standard:
                     alnum alpha ascii blank cntrl digit graph lower
                     print punct space upper word xdigit
                     A character class matches any character belonging to
                     that class.  The word character class matches
                     letters, digits, and the character _.

                     Within [ and ], an equivalence class can be
                     specified using the syntax [=c=], which matches all
                     characters with the same collation weight (as
                     defined by the current locale) as the character c.

                     Within [ and ], the syntax [.symbol.] matches the
                     collating symbol symbol.

       If the extglob shell option is enabled using the shopt builtin,
       the shell recognizes several extended pattern matching operators.
       In the following description, a pattern-list is a list of one or
       more patterns separated by a |.  Composite patterns may be formed
       using one or more of the following sub-patterns:

              ?(pattern-list)
                     Matches zero or one occurrence of the given patterns
              *(pattern-list)
                     Matches zero or more occurrences of the given
                     patterns
              +(pattern-list)
                     Matches one or more occurrences of the given
                     patterns
              @(pattern-list)
                     Matches one of the given patterns
              !(pattern-list)
                     Matches anything except one of the given patterns

       Theextglob option changes the behavior of the parser, since the
       parentheses are normally treated as operators with syntactic
       meaning.  To ensure that extended matching patterns are parsed
       correctly, make sure that extglob is enabled before parsing
       constructs containing the patterns, including shell functions and
       command substitutions.

       When matching filenames, the dotglob shell option determines the
       set of filenames that are tested: when dotglob is enabled, the set
       of filenames includes all files beginning with ``.'', but ``.''
       and ``..'' must be matched by a pattern or sub-pattern that begins
       with a dot; when it is disabled, the set does not include any
       filenames beginning with ``.'' unless the pattern or sub-pattern
       begins with a ``.''.  As above, ``.'' only has a special meaning
       when matching filenames.

       Complicated extended pattern matching against long strings is
       slow, especially when the patterns contain alternations and the
       strings contain multiple matches.  Using separate matches against
       shorter strings, or using arrays of strings instead of a single
       long string, may be faster.


Looking closely, each filename starts with -file0. So using:

*file ./-file0* *

we can apply the file command to all of them at once.

The result showed that all files except *-file07* were classified as **data**. This one file was identified as an **ASCII text file**, meaning it is human-readable.

# Result

The password for the next level is:

2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ