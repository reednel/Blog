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
$e_k(x) = x + k (mod 26)$
$d_k(y) = x - k (mod 26)$
What this means is we're working with a 26 character alphabet (i.e. $A, ..., Z$), where each character is mapped to a number (i.e. $A = 0, ..., Z = 25$). Then if we choose the key to be $3$, we have $e_3(A) = D, e_3(B) = E, ..., e_3(Z) = B$. So all we've done is shifted (rotated) each character in our message by 3 characters. $k$ can be any integer from 0 through 25 ($26 \cong 0 (mod 26)$). When $k = 3$ specifically, this is called the Caesar cipher.

yes

### RSA

### Culture
- RSA stands for Rivest Shamir Adleman, the names of the algorithm's designers.
- An equivalent system was developed and used by the British government years before RSA was independently developed and published about.
