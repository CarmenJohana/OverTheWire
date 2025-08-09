# Preliminaries

In this level, the password is stored in a file within the *inhere* directory.

# Commands used

After changing into the *inhere* directory and running:

*ls -a*

I confirmed the presence of directories named maybeherei (where i ranges from 00 to 19), along with the hidden entries . and ...

The challenge specifies that the target file can be identified by certain properties. To locate it, I searched for commands related to file searching:

*man -k "search" "files"*

Among the results, the following entry stood out:

*find (1) – search for files in a directory hierarchy*

From the man find page, I identified relevant options:

   - -size — search by file size

   - -execdir — execute a command in the directory of the matched file (safer than -exec)

   - -executable — search for files with execute permissions

Using these, I ran:

find . -size 1033c ! -executable -execdir file {} \;

This returned:

*./maybehere07/.file02: ASCII text, with very long lines (1000)*

# Result

Opening the file revealed the password:

HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
