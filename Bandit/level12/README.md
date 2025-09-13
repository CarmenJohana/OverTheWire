# Preliminaries

In this level, the password is stored in the file data.txt.
The twist is that this file is a hexdump of a file that has been repeatedly compressed.
The task is to reverse the hexdump and then decompress the file step by step until the password is revealed.

Because this process generates many intermediate files, and because of permission restrictions inside */home/bandit12*, it’s recommended to work inside a temporary directory under /tmp. The level description itself suggests using:

*mktemp -d*

This creates a new, randomly named directory where you can freely copy and manipulate files without running into permission errors (this is why *xxd -r* initially failed when run directly inside */home/bandit12*).

# Commands used

## 1. Set up a workspace

*mktemp -d*

*cd /tmp/<generated_directory>*

*cp /home/bandit12/data.txt .*

## 2. Reverse the hexdump

The file is a hexdump, so the first step is to convert it back into its original binary form:

*xxd -r data.txt > file1*

## 3. Identify file type

The file command helps detect the compression format:

*file file1*

At each stage, this indicated whether the file was gzip, bzip2, tar, etc.

## 4. Decompress repeatedly

Depending on the file type, I used the appropriate tool:

 - For gzip:
	
	*mv file1 file1.gz*

	*gzip -d file1.gz*

 - For bzip2:
	*bzip2 -d file1*
 
 - For tar archives:
	*tar -xf file1*

After each decompression, I ran file <filename> again to determine the next step.

## 5.Final step

After several layers, one file turned out to be plain ASCII text. Viewing it gave the password.

# Result

The password for the next level is:

*FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn*