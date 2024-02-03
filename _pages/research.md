---
layout: page
permalink: /research/
title: Research
description: 
nav: true
nav_order: 6
---

My research area is in cryptography. Specifically, most of my work is in an area of cryptography known as homomorphic encryption.

### What is homomorphic encryption?

Homomorphic encryption describes encryption schemes in which ciphertexts (ie, encrypted messages) can be added and multiplied together by parties who have access only to public information. In this scenario, anyone can perform computation on encrypted data, while learning nothing about the data (or any private information).

### Why is homomorphic encryption useful?

The most relevant application of homomorphic encryption is for secure cloud computing. Since homomorphic encryption allows for computation on data without any knowledge of what the data is, sensitive information can be outsourced for secure computation.

### How does homomorphic encryption work?

The standard homomorphic encryption schemes take advantage of the ring learning with errors (RLWE) problem. For some polynomial $$\Phi(x)$$ of degree $$n$$, define the following rings $$R$$ and $$R_q$$:

$$ R = \mathbb{Z}[x]/(\Phi (x)) $$

$$ R_q = \mathbb{Z}[x]/(\Phi (x),q) $$

First, choose secret $$s \in R$$ random with small coefficients. Then, sample some polynomial $$a$$ uniform randomly from $$R_q$$, and sample random polynomial $$e$$ with small coefficients from $$R$$. Then, compute $$b\in R_q$$ via $$b= -as+e \mod (\Phi,q)$$. The ordered pair $$(a,b)$$ is called an RLWE sample.

The RLWE problem is given many RLWE samples, to determine the secret polynomial $$s$$. The hardness of this problem was shown by [Lyubashevsky, Peikert, and Regev](https://dl.acm.org/doi/10.1007/978-3-642-13190-5_1) in 2010, and is the underlying problem in current homomorphic encryption schemes.

In these schemes, the ciphertext essentially forms a modified RLWE sample. For instance, in the [BGV](https://eprint.iacr.org/2011/277) scheme, we start with a message $$m \in R_t$$ for some plaintext modulus $$t$$. To encrypt $$m$$, we sample $$a$$, $$e$$, and secret $$s$$ as above, then calculate $$b\in R_q$$ via $$b= -as+m+te \mod (\Phi,q)$$. The ordered pair $$(a,b)$$ forms our BGV ciphertext. This describes the private key encryption algorithm, but a public key version of all these cryptosystems exist as well.

The unique aspect of the encryption is that our ciphertexts are in a format where we can define addition and multiplication operations between them. For example, let’s suppose we have two BGV ciphertexts $$(a_0,b_0)$$ and $$(a_1,b_1)$$ which satisfy

$$ b_0 + a_0s \equiv m_0 + te_0 $$

$$ b_1 + a_1s \equiv m_1 + te_1 $$

Then, we can add our ciphertexts together to form a new ciphertext $$(a_2,b_2) = (a_0,b_0)+(a_1,b_1)$$. If we define $$e_2 = e_0 + e_1$$, we then claim $$(a_2,b_2)$$ is an encryption of $$m_0+m_1$$. That is, $$(a_2,b_2)$$ satisfies the same relationship as $$(a_0,b_0)$$ and $$(a_1,b_1)$$ that we outline above, but for the message $$m_0+m_1$$ instead. Observe:

$$ b_2 + a_2s \equiv b_0 + b_1 + (a_0 + a_1)s \equiv (b_0 + a_0s) + (b_1 + a_1s)\equiv (m_0 + te_0) + (m_1 + te_1)$$

$$ \equiv m_0 + m_1 + t(e_0+e_1) \equiv m_0+m_1 + te_2 \mod (\Phi, q)$$

We omit some finer details here, but this captures the basic idea of how we can add ciphertexts together. We can define a procedure for multiplication as well, but it becomes far more complicated and involved.

### What part of homomorphic encryption do you study?

The part of homomorphic encryption I study is specifically on the “noise” term and the growing and shrinking of this term as operations happen. By noise, we are referring to the term $$e$$ in a ciphertext $$(a,b)$$ described above. 

The significance in the term $$e$$ is that if this term grows too large, we can no longer accurately decrypt our ciphertext. So, it is important to analyze and manage the noise growth as operations occur. In the [CKKS](https://eprint.iacr.org/2016/421) scheme, which allows for approximate homomorphic computation, the noise growth also affects the accuracy of the final decrypted message.

If you’re curious at a more in-depth look at what I study, my M.S. thesis is available [here](https://tigerprints.clemson.edu/all_theses/3868/).

### Resources and Libraries for Homomorphic Encryption

[FHE.org](https://fhe.org/)

[Microsoft SEAL](https://www.microsoft.com/en-us/research/project/microsoft-seal/)

[HEAAN](https://heaan.it/)

[OpenFHE](https://www.openfhe.org/)

[HElib](https://homenc.github.io/HElib/)



