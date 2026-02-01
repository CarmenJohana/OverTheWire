# Preliminaries

The password (or access for the next level) is not given directly. Instead, this level provides a private SSH key that can be used to log in as bandit14. The file _sshkey.private_ is located in /home/bandit13 and is readable by the current user (bandit13). The next-level SSH service listens on port 2220 (not the SSH default port 22).

## Important context:

- There is one Bandit server (_bandit.labs.overthewire.org_). Each level (bandit0, bandit1, …, bandit14) is a different user account on the same machine, not a separate machine.

- localhost always refers to the machine you are currently on. If you are logged into the Bandit server as bandit13, _localhost_ means the Bandit server itself.

- From my local computer, _localhost_ means my own PC — so ssh ... @localhost run on my PC will try to connect to port 2220 on my PC, not the Bandit server.

# Commands used

1. Use the private key from inside the Bandit server (as bandit13)

First, we logged into the Bandit server as usual (from my local machine):

_ssh bandit13@bandit.labs.overthewire.org -p 2220_

Once I was in the remote shell as bandit13, I used the private key to SSH into bandit14 on the same server. The correct command (run from the bandit13 shell) is:

_ssh -i /home/bandit13/sshkey.private bandit14@localhost -p 2220_

# Notes and important details:

-  _-i /home/bandit13/sshkey.private_ tells SSH to use the provided private key file.

	- My initial attempt failed because I gave a wrong path (I forgot the leading / — e.g. home/bandit13/sshkey.private instead of /home/bandit13/sshkey.private). That path error caused the client not to find the key file.
- _bandit14@localhost_ means “connect to user bandit14 on the same server (loopback).”
- This works from the bandit13 account because sshkey.private is readable by bandit13 and is authorized for bandit14.

# Sources

- https://monovm.com/blog/how-to-connect-to-ssh-with-private-key/

- https://help.ubuntu.com/community/SSH/OpenSSH/Keys

# Modifications

# Bandit Level 13 — SSH Key Authentication

## Overview

In **Bandit Level 13**, the password for the next level (**bandit14**) is not provided directly.  
Instead, this level introduces **SSH key-based authentication** by providing a private key that can be used to log in as `bandit14`.

This level reinforces the idea that all Bandit levels exist on **the same server**, not on separate machines.

---

## Environment Notes

- Server: `bandit.labs.overthewire.org`
- SSH Port: `2220`
- Each Bandit level (`bandit0`, `bandit1`, …) is a different **user account on the same machine**

Important clarification:

- From your **local computer**, `localhost` refers to your own PC.
- From inside the Bandit server, `localhost` refers to **the Bandit server itself**.

---

## Initial Access (bandit13)

Login from the local machine:


	ssh bandit13@bandit.labs.overthewire.org -p 2220

Once logged in, the private key is located at /home/bandit13/sshkey.private

# Original Intended Solution (In-Server SSH)
The intended solution is to SSH from bandit13 into bandit14 using the provided private key:

ssh -i /home/bandit13/sshkey.private bandit14@localhost -p 2220

## Explanation

- -i /home/bandit13/sshkey.private specifies the private key
- bandit14@localhost means “connect to bandit14 on the same server”
- This works because:
	- The key is readable by bandit13
	- The corresponding public key is authorized for bandit14

# Change in Behavior (Observed Later)

When attempting this level again months later, direct SSH from bandit13 to bandit14 no longer worked.

This is likely due to server-side configuration changes, such as:

Restricting SSH lateral movement between users

Modifying sshd configuration

Hardening the environment to prevent local SSH chaining

Since Bandit is a live wargame, its internal configuration may change over time even if the level description remains the same.

# Alternative Solution (Using SCP)

To work around this, the private key was copied to the local machine using scp:

scp -P 2220 bandit13@bandit.labs.overthewire.org:sshkey.private .

# SSH Key Permission Issue

Attempting to use the key resulted in the following warning:

	Permissions 0640 for 'sshkey.private' are too open.

SSH requires private keys to be readable only by the owner.

## Fixing Permissions

	chmod 700 sshkey.private

Resulting permissions:

	-rwx------
# Logging in as bandit14 (From Local Machine)

With correct permissions:

	ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220

# Retrieving the Password

Once logged in as bandit14, the password for the next level is stored in:

	/etc/bandit_pass/bandit14

Password:

	MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
