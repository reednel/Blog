---
layout: post
author: Reed Nelson
title: "Data Compression"
---

## Overview

**Data compression** is a process of modifying the representation of some information so that it can be stored using less data. Storing and transmitting data is obviously expensive in large quantities, making an optimal compression (one which minimizes storage size) extremely valuable. In this post we will learn how to quantify data information-theoretically, build intuition for ___, and learn how to get the optimal compression remarkably quickly.

## Entropy - ?Formally Quantifying Information?

[^0]
Let $\Omega$ be some set, and $P = \{p_i,\, i\in \Omega\}$ be the probability distribution over $\Omega$, i.e. the frequency with which each element of $\Omega$ occurs. The entropy of $\Omega$ is a measure of how structured (non-uniform) $P$ is. So for example, the uniform distribution, where $\forall p_i \in \Omega,\, p_i = \frac{1}{|\Omega|}$, is the least structured, and the lowest entropy. Conversely, the distribution where $p_{i_0} = 1,\, p_i = 0 \, \forall i \neq i_0$, is the most structured, and has the most entropy.

More intuitively, entropy can be thought of as a measure of uncertainty in random choices from $\Omega$, using $P$.

Formally, the **entropy** of $P$ is given by $H(P) = - \sum\limits_{i \in \Omega} p_i (\log(p_i))$.

Fact: $0 \leq H(P) \leq \log(|\Omega|) = H(P_{uniform})$.

#### Applying Entropy 

?Remarkably, a choice from $\Omega$ contains $H$ bits of information per element.

Take $\Omega = \{A, B, ..., Z\}$. $\log(|\Omega|) = \log(26) = 4.17$. Then naively we can represent the alphabet using 5 bits. Perhaps $A = 00000, B = 00001, ..., Z = 11001$. Now we can imagine using this coding on a text file we wrote (of only these 26 characters). The size of this file (ignoring metadata and whatever) is 5 bits per character $\times$ the number of characters.

Already you might see that this is suboptimal. With 5 bits, you can represent as many as 32 characters, so we could add 6 more chacters to our alphabet without using any extra data per character. This is an improvement, but still we're restricting ourselves. What if we used a variable number of bits per character?

## Coding

Let's formalize what a coding is:
A **coding** of $\Omega$ is a unique mapping between the elements of $\Omega$ and a set of binary strings.
A **prefix code** is a code where no coded character is a prefix of another character. For example, a code with $A = 01, B = 010$ is not a prefix code, because $C(B)$ begins with $C(A)$. If we aren't using fixed-length codings, it's important to use a prefix code so there isn't ambiguity about where one character ends and another begins.

With this we can talk about expected lengths...

The expected length $L$ of a code is the sum of the probability $p$ of each character ocurring, multiplied by the length $\ell$ of that character's code.
That is, $L(C) = \sum\limits_{x \in \Omega}p(x) \cdot \ell(x)$.
Practically, this means that on average we expect a message $n$ characters long (using this coding) to take up $n \times L(C)$ bits.

Of course, the goal of compression is to use a coding of minimal expected length. It is essential to this project that language is not uniform. When speaking English, $A$ doesn't appear with the same frequence as $Z$. In fact, $A$ makes up about $8\%$ of all letters we write, but $Z$ makes up a mere $0.07\%$[^1]. Intuitively, we want our code to reserve the shortest bit strings for the most common letters, like $A$ and $E$, and assign the longer codings to the rare characters, like $Z$ and $Q$. To reiterate, the higher the entropy in a set of characters, the more compressible it is.

Theorem: there exists a prefix code for ...

## Huffman Coding

- Something super cool and super rare: Huffman's one-shot
- Somehow we knew what the optimal is
- Huffman's simple ?$O(n\log(n))$ algorithm finds an optimal coding.

[^0]: [Claude Shannon](https://en.wikipedia.org/wiki/Claude_Shannon) is the father of [Information Theory](https://en.wikipedia.org/wiki/Information_theory), and an absolute legend. He wrote the book *A Mathematical Theory of Communication*, which a professor of mine once described as "one of the most important books in science in the last century".

[^1]: This statistic is from the Wikipedia page on [Letter Frequency](https://en.wikipedia.org/wiki/Letter_frequency).