# Preliminaries

In this level, our goal is to find the password for the next level, which is stored in a file with an unusual name:

*--Spaces in this filename--*

This file is located in the */home/bandit2* directory, which is the home directory of the user bandit2.

Because of the spaces in the filename, I suspected this might involve the concept of metacharacters — special characters that are interpreted by the shell in unique ways, rather than as literal input. My first instinct was to check the manual pages to better understand how to handle such filenames.

I tried searching the man page index using:

*man -k metacharacters*

*man -k quoting*

*man -k wildcard*

*apropos metacharacters*

Unfortunately, these didn’t yield useful or directly relevant results. Most hits were related to unrelated topics like namespaces, and I couldn’t find anything explaining how to work with filenames containing spaces or special symbols.

Later on, I realized that many useful manual pages aren’t indexed under intuitive keywords and can’t always be found using man -k or apropos. For example, I couldn’t find the bash man page this way either, which turned out to contain exactly the information I needed.

After hitting a dead end with the man pages, I turned to the web and found this helpful tutorial explaining Unix quoting mechanisms:

*https://www.tutorialspoint.com/unix/unix-quoting-mechanisms.htm*

This page explained that to handle filenames with spaces or metacharacters, we can either escape each special character (using a backslash \), or enclose the entire filename in quotes.

Commands used

With this knowledge, I tried the following commands:

*cat ./\--Spaces\ in\ this\ filename--*

and 

*cat ./"--Spaces in this filename--"*

Both worked correctly and revealed the password.

# Result

The password for the next level is

MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx

# Note

Later, I realized that the best source of information for this topic was the Bash manual page, as it clearly defines how the shell interprets words, spaces, and special characters. Although man -k didn’t help me at first, I eventually found what I needed by running man -k shell and checking the Bash entry listed there.

Inside man bash, I found the DEFINITIONS and QUOTING sections particularly helpful. These sections provided key insights, such as:

	metacharacter: A character that, when unquoted, separates words. One of the following:
		| & ; ( ) < > space tab newline

And further:

    Quoting is used to remove the special meaning of certain characters or words to the shell.
    There are three quoting mechanisms:

        Escape character (\)

        Single quotes (')

        Double quotes (")

