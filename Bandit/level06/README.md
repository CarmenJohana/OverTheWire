# Preliminaries

In this level, the password is stored somewhere on the server with all these properties:

   - Owned by user bandit7

   - Owned by group bandit6

   - Exactly 33 bytes in size

Because the exact location isn’t given, we need to search the filesystem for a file matching these criteria.

# Commands used

The best tool for this task is the find command, which allows filtering by owner, group, and size. Relevant options from the man find page:

    - user bandit7 to match files owned by user bandit7

    - group bandit6 to match files owned by group bandit6

    - size 33c to match files exactly 33 bytes in size (c means bytes)

Since the file could be anywhere, a good starting point is the /home directory, but we do not have permission to access all subdirectories. When running find, permission denied errors appear for some directories. To avoid cluttering the output, error messages can be redirected to /dev/null like this:

find /home -user bandit7 -group bandit6 -size 33c -print 2>/dev/null

Here, 2>/dev/null means: redirect all error messages (file descriptor 2) to /dev/null, effectively hiding them. This lets us see only the files that match the search criteria without being distracted by permission errors.

Since no results appeared in /home, the search was extended to the entire filesystem /:

find / -user bandit7 -group bandit6 -size 33c -print 2>/dev/null

This allowed us to find the desired file.

# Result

The password for the next level is:

morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
