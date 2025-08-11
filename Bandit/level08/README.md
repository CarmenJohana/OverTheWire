# Preliminaries

In this level, the password is stored in the file *data.txt*. The password is the only line that appears exactly once in the file.

# Problem

Using the command:

*uniq -zu data.txt*

returns many lines instead of just one. This is unexpected because the level says there should be only one line that appears once.

# Explanation and Solution

The *uniq* command only works correctly on sorted input. It compares adjacent lines and detects duplicates accordingly. Since *data.txt* is likely unsorted, many lines are treated as unique just because duplicates are not adjacent.

To solve this, we need to sort the file first before using *uniq*. Use the following pipeline:

*sort data.txt | uniq -u*

- sort data.txt sorts the lines alphabetically, bringing duplicate lines together.
- uniq -u then prints only the lines that appear exactly once.

This will correctly identify the unique line, which contains the password.

# Result

The password for the next level is:

4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
