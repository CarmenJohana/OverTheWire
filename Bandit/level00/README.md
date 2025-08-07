# Preliminaries

At Bandit Level 0, we are introduced to the way we can connect to the game using SSH.
According to the provided documentation, the correct syntax is:

*ssh username@hostname -p port*

For level 0, the actual command would be:

*ssh bandit0@bandit.labs.overthewire.org -p 2220*

Once you run this command in the terminal, you will be prompted to enter a password.
The password for Level 0 is given on the Bandit website.

After successfully logging in, the goal is to find the password for the next level (Bandit1).

# Level 0 → Level 1: Description

According to the instructions, the password for the next level is stored in a file called readme, located in the home directory.

# Commands Used

We need to perform a few basic operations:

## Knowing the place we are:

First we check our current directory using pwd.

This confirms that we are in the user's home directory (e.g., /home/bandit0).

## Listing the files in the current directory:

We now employ ls to show the files available -in this case, we should see readme.

## Viewing the content of the file:

Finally, *cat readme* prints the contents of readme, which contains the password for Bandit1.

# Result

Password we are looking for is: ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If