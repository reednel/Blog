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

#### A bit about modular arithmetic

The modulus operator gives the remainder of an integer division. For example, $5 \text{ mod } 3 = 2$. Equivalently, we say $5 \equiv 2 (\text{mod } 3)$. $\mathbb{Z}$ denotes the set of integers, and $\mathbb{Z}_n$ denotes the set of integers modulo $n$, i.e. $\{0, 1, 2, ..., n-1\}$.

### Traditional Ciphersystems

A ciphersystem $(P, C, K, e, d)$ is defind as follows:
$P = $ a set of plaintexts
$C = $ a set of ciphertexts
$K = $ a set of keys
$e:\, P \to C = $ an encryption function
$d:\, C \to P = $ a decryption function

The role of all these pieces will be apparent with a simple example:

#### The Shift Cipher

$P = C = K = \mathbb{Z}_{26}$
$e_k(x) = x + k (\text{mod } 26)$
$d_k(y) = x - k (\text{mod } 26)$
What this means is we're working with a 26 character alphabet (i.e. $A, ..., Z$), where each character is mapped to a number (i.e. $A = 0, ..., Z = 25$). Then if we choose the key to be $3$, we have $e_3(A) = D, e_3(B) = E, ..., e_3(Z) = B$. So all we've done is shifted (rotated) each character in our message by 3 characters. $k$ can be any integer from 0 through 25 ($26 \equiv 0 (\text{mod } 26)$). When $k = 3$ specifically, this is called the Caesar cipher.

yes

### RSA

RSA is a public key ciphersystem, which means that everyone can know how to encrypt a message, but the encryption key is not sufficient to decrypt the message. So the encryption function is still invertible (otherwise there would be no way to decrypt), but it is not easy to find the inverse of the encryption function. A function like this is sometimes called a one-way function, or a trapdoor function.

RSA leverages this essential fact to create its one-way functions: it is relatively easy to compute very large prime numbers, but very difficult to find the prime factors of large numbers.

Let $p$ and $q$ be two large primes, and $n = p \cdot q$. Then take $e$ and $d$ in $\{0, 1, ..., (p-1)(q-1)\}$, such that $e \cdot d = 1 (\text{mod } 26)$. That is, $e$ and $d$ are inverses in $\mathbb{Z} \text{ mod } (p-1)(q-1)$. At this point we can throw out everything but $e$, $d$, and $n$, we no longer need them and their dicovery would break the security of our scheme. Now we can share $(e, n)$ publicly, and must keep $d$ secret. The encryption for a message $M$ is simply $M^e (\text{mod } n)$, and the decryption is $(M^e)^d (\text{mod } n)$.

It's not obvious at all that $M^{e \cdot d} = M (\text{mod } p \cdot q)$ when $e \cdot d = 1 (\text{mod } (p-1)(q-1))$, but this fact is also essential for RSA to work as it does. I'll prove this statement below in case you're interested.

I've already mentioned that RSA is widely used today, but in particular many RSA systems use a 2048 bit (~600 digit) "$n$" value, and an "$e$" value of precisely 65,537. If you like your powers of two, you may recognize this as $2^{16}+1$[^1].

For a sense of scale, the number of atoms in the universe has about 80 digits. So the numbers we're working with here are truly massive. This raises the question: how do we efficienly encrypt and (especially) decrypt messages? The key here is modular exponentiation. 

### Culture

- RSA stands for Rivest Shamir Adleman, the names of the algorithm's designers.
- An equivalent system was developed and used by the British government years before RSA was independently developed and published about.

#### Proof that $\forall x \in \mathbb{Z}_{pq},\, x^{ed} = x$

Fermat's Little Theorem[^0]: if $p$ is prime, then $x^p \equiv x (\text{mod } p)$.
By construction, $ed = 1 \text{mod } (p-1)(q-1)$, so $(ed-1)$ is a multiple of $(p-1)(q-1)$. That is, $\exists k \in \mathbb{Z}:\, ed-1 = k(p-1)$.
Then $(x^e)^d = x^{ed} = x \cdot x^{ed-1} = x \cdot x^{k(p-1)} = x \cdot (x^p)^k \cdot x^{-k}$.
By Fermat's Little Theorem, $x^p \equiv x (\text{mod } p)$, so $x \cdot (x^p)^k \cdot x^{-k} = x \cdot x^k \cdot x^{-k} = x (\text{mod } p)$.
By symmetry, $(x^e)^d = x (\text{mod } q)$.
So we have $\forall x \in \mathbb{Z}_n, x^{ed} = x (\text{mod } pq)$.

[^1]: Numberphile did an [RSA video](LINK) which explains why this choice of $e$ is pretty good.
[^0]: The second coolest theorem with a name of the form "Fermat's L___ Theorem".
