
---

## `README_LEVEL_14.md`

```md
# Bandit Level 14 — Netcat and Local Services

## Overview

In **Bandit Level 14**, the objective is to retrieve the password for **bandit15**.

This level introduces interaction with a **local network service** listening on a specific port and demonstrates how to send data to it.

---

## Key Information

- The password must be sent to a local service
- Host: `localhost` (127.0.0.1)
- Port: `30000`

---

## Tool Discovery

Searching for tools capable of sending data to a specific port led to **netcat (`nc`)**.

Netcat is a versatile networking utility commonly used for:

- Sending and receiving data over TCP/UDP
- Debugging services
- Interacting with open ports

Reference:

- https://www.varonis.com/blog/netcat-commands

---

## Solution Using Netcat

The password for `bandit14` is stored in:


	/etc/bandit_pass/bandit14

To send it to the service listening on port 30000:

	cat /etc/bandit_pass/bandit14 | nc localhost 30000

## Notes

- localhost is equivalent to 127.0.0.1
- nc reads from standard input and sends the data to the specified port
- The pipe (|) passes the file contents directly to the network service

## Results

The service returns the password for bandit15:

_8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo_

## Key Takeaways

- localhost always refers to the current machine

- Netcat can act as a simple client for local services

- Piping data into network services is a common CTF technique

- Minimal tools can be extremely powerful


