---
layout: post
author: Reed Nelson
title: "An Introduction to RSA Encryption"
---


### Overview

Encryption is

- What, broadly, is an encryption scheme
- Where does RSA sit among these
- y

### Traditional Ciphersystems

A ciphersystem $(P, C, K, e, d)$ is defind as follows:
$P = $ a set of plaintexts
$C = $ a set of ciphertexts
$K = $ a set of keys
$e:\, P \to C = $ an encryption function
$d:\, C \to P = $ a decryption function

The role of all these pieces will be apparent with a simple example:
The Shift Cipher
$P = C = K = \{0, 1, ..., 25\}$
$e_k(x) = x + k (\text{mod } 26)$
$d_k(y) = x - k (\text{mod } 26)$
What this means is we're working with a 26 character alphabet (i.e. $A, ..., Z$), where each character is mapped to a number (i.e. $A = 0, ..., Z = 25$). Then if we choose the key to be $3$, we have $e_3(A) = D, e_3(B) = E, ..., e_3(Z) = B$. So all we've done is shifted (rotated) each character in our message by 3 characters. $k$ can be any integer from 0 through 25 ($26 \cong 0 (\text{mod } 26)$). When $k = 3$ specifically, this is called the Caesar cipher.

yes

### RSA

RSA is a public key ciphersystem, which means that everyone can know how to encrypt a message, but the encryption key is not sufficient to decrypt the message. So the encryption function is still invertible (otherwise there would be no way to decrypt), but it is not easy to find the inverse of the encryption function. A function like this is sometimes called a one-way function, or a trapdoor function.

RSA leverages this essential fact to create its one-way functions: it is relatively easy to compute very large prime numbers, but very difficult to find the prime factors of large numbers.

Let $p$ and $q$ be two large primes, and $n = p \cdot q$. Then take $e$ and $d$ in $\{0, 1, ..., (p-1)(q-1)\}$, such that $e \cdot d = 1 (\text{mod } 26)$. That is, $e$ and $d$ are inverses in $\mathbb{Z} \text{ mod } (p-1)(q-1)$.

### Culture

- RSA stands for Rivest Shamir Adleman, the names of the algorithm's designers.
- An equivalent system was developed and used by the British government years before RSA was independently developed and published about.
