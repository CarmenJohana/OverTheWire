# Preliminaries

In this level, we need to find the password inside a file called *data.txt*. The password is hidden in a line that contains a specific pattern.

# Commands used

To search for a specific pattern within a file, I looked for commands related to searching patterns by using:

*man -k "search" "pattern"*

Among the results, I found the command *grep*, which is described as:

*grep (1) - print lines that match patterns*

Therefore, I used the following command to search for the word "millionth" inside the file *data.txt*:

*grep millionth data.txt*

# Result

The command output contained the password for the next level:

dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc