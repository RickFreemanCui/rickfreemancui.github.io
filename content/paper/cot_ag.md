+++
title = "Authenticated Garbling From Correlated OT"
draft = false
+++

Inspired by [DILO22], we investigate what is the bare minimum we can
achieve using the correlated OT functionality in actively secure
two-party computation. We found that with the following two techniques

-   block COT and compression idea of [DILO22]
-   dual execution

We can achieve constant (up to 5 bits per AND gate) overhead in terms of
one-way communication compared to semi-honest half-gate [ZRE15].


## One-way Communication {#one-way-communication}

The one-way communication result is published as _Actively Secure
Half-Gates with Minimum Overhead under Duplex Networks. In Advances in
Cryptology–EUROCRYPT 2023: 42nd Annual International Conference on the
Theory and Applications of Cryptographic Techniques, Lyon, France,
April 23–27, 2023, Proceedings, Part II (pp. 35-67). Cham: Springer
Nature Switzerland._ [PDF](https://link.springer.com/content/pdf/10.1007/978-3-031-30617-4_2.pdf)


## Two-way Communication {#two-way-communication}

We then extended the result towards minimizing two-way communication.
We manage to achieve \\( 2\kappa + \lambda + C \\) bits per AND gate
where \\( \kappa \\) is the computational security parameter and \\(
\lambda \\) is the statistical security parameter. This work is
available at [ePrint 2023/278](https://eprint.iacr.org/2023/278).
