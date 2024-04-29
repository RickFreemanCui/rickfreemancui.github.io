+++
title = "LPN-based Signature from VOLE in the Head"
draft = false
+++

The **VOLE in the Head** framework demonstrates very competetive
performance as compared to the traditional MPC in the Head
framework. This has been demonstrated in the **FAEST** signature scheme
(Crypto 2023).

One natural ideal is to utilize this framework to prove other OWF,
e.g. LPN-based. In this work, we apply the sketching technique of
[BGI16] to prove that the LPN noise consists of a series of unit
vectors, and then apply QuickSilver to prove the validity of LPN
witness. After transforming the proof system under the VOLE in the
Head framework from designated verifier to public verifier, we get a
signature scheme called **ReSolveD**. The scheme shows smaller signature
size as compared to previous state-of-the-art **SDitH** (Eurocrypt 2023,
Asiacrypt 2023)

This work is published as _ReSolveD: Shorter Signatures from Regular
Syndrome Decoding and VOLE-in-the-Head, Public Key Cryptogrpahy 2024_
[ePrint 2024/040](https://eprint.iacr.org/2024/040.pdf)

I gave several talks about this project, summarized in [this post]({{< relref "resolved_talk" >}}).
