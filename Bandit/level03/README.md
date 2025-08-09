# Preliminaries

In this level, we are told that the password is stored in a hidden file inside the *inhere* directory.

# Commands used

According to the documentation for *ls* (one of the commands suggested in the level’s description), this command lists directory contents. With the option -a or --all, it will also show entries starting with . (hidden files).

Using this command in /home/bandit3, you can see the hidden directories . and .., along with the hidden files .bash_logout, .bashrc, and .profile.

To change into a directory, you use cd *name_of_the_directory*. In our case, the command was:

*cd inhere*

Then, I used:

*ls -a*

and found the hidden file *...Hiding-From-You*.

To see the contents of this file, I used:

*cat ./...Hiding-From-You*

# Result

The password for the next level is:

2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ

