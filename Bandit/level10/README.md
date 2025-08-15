# Preliminaries

The password for the next level is stored in the file *data.txt*, which contains Base64-encoded data.

To understand the task, I referred to the following website:

*https://www.baeldung.com/linux/cli-base64-encode-decode*

From that source, I learned that Base64 encoding is a common method for representing binary data as ASCII text, often used to transfer or store data safely in text-based systems.

# Commands Used

Linux includes a built-in command, *base64*, which can both encode and decode Base64 data.

First, I checked the contents of *data.txt* using *cat*:

*cat data.txt*

The output was:

VGhlIHBhc3N3b3JkIGlzIGR0UjE3M2ZaS2IwUlJzREZTR3NnMlJXbnBOVmozcVJyCg==

To decode this Base64 string, I used the -d flag (short for --decode) with the base64 command:

*cat data.txt | base64 -d*

# Result

The decoded output revealed the password:

dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr

