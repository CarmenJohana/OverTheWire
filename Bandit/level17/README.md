
---

# README
# Bandit Level 17 — Finding Differences Between Files

### Overview

In **Bandit Level 17**, the objective is to find the password for **bandit18**.

The home directory contains two files:

- `passwords.old`
- `passwords.new`

The password is located in **`passwords.new`**, on **the only line that differs**
between the two files.

---

## Solution Strategy

To identify the difference between the files, the `diff` utility was used.

	diff passwords.new passwords.old

## Command Output

	42c42
	< x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
	---
	> BMIOFKM7CRSLI97voLp3TD80NAq5exxk

## Understanding the Output

### Line Reference

42c42

This means:

	- Line 42 in passwords.new
	- Was changed (c) from line 42 in passwords.old

So:

	< x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO

is the line present in _passwords.new_

	> BMIOFKM7CRSLI97voLp3TD80NAq5exxk

is the line present in _passwords.old_

## Password

Since the password is located in passwords.new, the correct password for
logging into bandit18 is:

	x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
