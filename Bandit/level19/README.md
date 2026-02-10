# Bandit Level 19 — Using a SetUID Binary

## Overview

In **Bandit Level 19**, the objective is to gain access to the next level by
using a **setuid binary** located in the home directory.

The password for **bandit20** is stored in the usual location:


	/etc/bandit_pass/bandit20


However, this file is not readable by bandit19.
The challenge is to understand and correctly use the provided setuid binary.

## Understanding SetUID

Before solving the level, some research was done on setuid.

A highly recommended reference (apart from the Wikipedia webpage for setuid):

	https://www.howtogeek.com/656646/how-to-use-suid-sgid-and-sticky-bits-on-linux/

## Exploring the home directory

Listing the files:

	bandit19@bandit:~$ ls
	bandit20-do

Checking permissions:

	bandit19@bandit:~$ ls -l
	-rwsr-x--- 1 bandit20 bandit19 14884 Oct 14 09:26 bandit20-do

Important details:

- Owner: bandit20
- Group: bandit19
- Permissions: rwsr-x---
	- The s indicates the setuid bit

## Binary inspection

	bandit19@bandit:~$ file bandit20-do

And the output was:

	bandit20-do: setuid ELF 32-bit LSB executable, Intel 80386, dynamically linked

This confirms that:

	- The binary is setuid
	- It will execute with bandit20 privileges

## Executing the binary

Running the binary without arguments:

	bandit19@bandit:~$ ./bandit20-do

Output:

	Run a command as another user.
	  	Example: ./bandit20-do whoami

This reveals that the binary:

- Executes arbitrary commands
- Runs them as bandit20

## Locating the password file

Listing the password directory:
	
	ls /etc/bandit_pass

The target file:

	/etc/bandit_pass/bandit20

Checking its permissions:

	ls -l /etc/bandit_pass/bandit20

	-r-------- 1 bandit20 bandit20 33 Oct 14 09:25 /etc/bandit_pass/bandit20

This confirms:

	- Only bandit20 can read the file
	- Direct access is denied for bandit19

Using the binary to run cat as bandit20:

	./bandit20-do cat /etc/bandit_pass/bandit20

## Output:

	0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO

## Password

The password for bandit20 is:

	0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO






		