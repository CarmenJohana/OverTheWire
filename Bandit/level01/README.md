# Preliminaries

After closing the previous session using the *exit* command, we now want to log in to the next level.
The method is almost identical to before — the only change is the username:

*ssh bandit1@bandit.labs.overthewire.org -p 2220*

You’ll be prompted to enter the password for this user, which is the password obtained from the previous level.

According to the level description, the password for the next level is stored in a file named -.
As you’ll notice, trying to use *cat -* directly can cause problems — the system interprets *-* as an option or flag, not a filename.

# Commands Used

We start in the home directory of bandit1 — we can confirm this by the ~ symbol in the shell prompt.

By running ls we see the file named listed

An important thing to remember is that one can access a file or directory using a relative or absolute path — or even just the name of the file, as we have been doing.

So, we can try using other alternatives.

With the absolute path, we would use:

*cat /home/bandit1/-*

If we're inside /home/bandit1, we can use the relative path:

*cat ./-*

# Result

Using either method, we obtain the password for the next level:

263JGJPfgU6LtdEvgfWU1XP5yac29mFx
