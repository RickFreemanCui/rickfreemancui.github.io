+++
title = "Optimal One-time Signature"
draft = false
+++

Hash-based signature is to be standardized by NIST <span class="timestamp-wrapper"><span class="timestamp">&lt;2024-02-28 三&gt;</span></span>. So
it is a natural question to study whether the currently being standarized
algorithm **SPHINCS+** is indeed optimal.

Towards this end, we discovered that the constant-sum encoding method
that appear previously in the literature, is encoding-size-optimal
among all tree-based one-time signature schemes. Moreover, by refuting
a DAG-based construction [BM96] our scheme appears to be the optimal
among all existing constructions.

This work is published as _Revisiting the Constant-Sum Winternitz
One-Time Signature with Applications to and XMSS. In: Handschuh, H.,
Lysyanskaya, A. (eds) Advances in Cryptology –
CRYPTO 2023. CRYPTO 2023. Lecture Notes in Computer Science,
vol 14085. Springer, Cham._ [PDF](https://link.springer.com/content/pdf/10.1007/978-3-031-38554-4_15.pdf)
