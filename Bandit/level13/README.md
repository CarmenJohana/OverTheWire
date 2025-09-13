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
- The ownership and permissions of the private key file in /home/bandit13 don’t matter for the authentication process itself.