# Bandit Level 15 — SSL/TLS and Secure Local Services

## Overview

In **Bandit Level 15**, the objective is to retrieve the password for **bandit16**.

Unlike the previous level, the service listening on `localhost` requires the password to be submitted using **SSL/TLS encryption**.

This level introduces the use of encrypted network communication and tools capable of interacting with TLS-enabled services.

---

## Key Information

- The password of the current level must be submitted securely
- Host: `localhost` (127.0.0.1)
- Port: `30001`
- Encryption: **SSL/TLS**

Helpful note from the level description:

> Getting “DONE”, “RENEGOTIATING” or “KEYUPDATE”?  
> Read the “CONNECTED COMMANDS” section in the manpage.

This hint suggests using a tool that properly handles SSL/TLS sessions and standard input.

---

## Tool Used: OpenSSL (`s_client`)

To interact with the SSL/TLS-enabled service, **OpenSSL's `s_client`** utility was used.  
This tool allows establishing a raw TLS connection to a server and manually sending data.

---

## Solution Using OpenSSL

The password for `bandit15` is:

8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo

This password was sent to the service using the following command:

	echo "8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo" | openssl s_client -connect localhost:30001 -ign_eof

---

## Command Breakdown

- echo "password"

	Outputs the password to standard output

- |

	Pipes the output of _echo_ into the next command

- openssl s_client

	Acts as a generic SSL/TLS client

- -connect localhost:30001

	Connects to the TLS-enabled service runnning on port 30001

- -ign_eof

	- Prevents the connection from closing immediately after input is sent
	- This is important because the server may respond after processing the input

This approach was guided by the following reference:

	- https://stackoverflow.com/questions/23352152/how-to-send-a-string-to-server-using-s-client

---

## Output

The server responded with:

	...read R BLOCK

	Correct!

	kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx


	closed

The password for _bandit16_ is:

	kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx

---

## Alternative Solution Using Netcat (ncat)

An alternative solution **ncat**, a modern version of netcat with SSL/TLS support.

	ncat localhost --ssl 30001

Once connected, manually enter the password:

	8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo

The server responds:
	
	Correct!

	kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx

This alternative solution was referenced from:

	https://medium.com/@ismailahmedmohamed04/bandit-overthewire-all-levels-d12e8db8d5da


