# Preliminaries

According to the level description, the password is stored in the file *data.txt*.
It is part of one of the few human-readable strings in the file and is preceded by several = characters.

# Commands Used

The strings command is useful here because it extracts human-readable text from binary files.
According to its manual, it prints sequences of printable characters, which allows us to filter out binary data and focus on meaningful text.

To find the exact password pattern, I combined strings with grep using a regular expression.
The command was:

*strings data.txt | grep -E '([=]* [a-zA-Z0-9]+)'*

Here, *strings data.txt* extracts readable text from the file, *grep -E* enables extended regular expressions and *'([=]* [a-zA-Z0-9]+)'* matche strings preceded by zero or more = characters, followed by a space and then alphanumeric characters (the likely password).

The relevant output from the above command was:

*
========== the

D========== password

 U1-

w========== is

 QO'

yZ X

========== FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey

 Bn`

^ j+

*

# Result

From the text above, we can clearly see that the password is:

FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey