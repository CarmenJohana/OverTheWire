# Bandit Level 18 — Bypassing Restricted Shell Access

## Overview

In **Bandit Level 18**, the password for the next level is stored in a file
named `.readme` located in the **home directory** of `bandit18`.

However, direct SSH access is not possible because the `.bashrc` file has been
modified to **immediately log the user out upon login**.

This level demonstrates that even if an interactive shell is blocked,
other SSH-based mechanisms may still be available.

---

## Problem

- SSH login succeeds at the authentication stage
- Immediately after login, the session is terminated
- This behavior is caused by commands in `.bashrc`

As a result:
- No interactive shell is available
- Commands cannot be executed normally via SSH

---

## Solution

Although interactive SSH access is blocked, **`scp` is still allowed**.

This works because:
- `scp` uses SSH for transport
- It does **not** require an interactive shell
- `.bashrc` is not executed during non-interactive `scp` sessions

Using the password obtained in the previous level, the `.readme` file can be
downloaded directly from the home directory.

---

## Retrieving the File

From the local machine, the following command was used:


	scp -P 2220 bandit18@bandit.labs.overthewire.org:~/.readme .

# Password

The downloaded _.readme_ file contains the password for bandit19:

	cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8
