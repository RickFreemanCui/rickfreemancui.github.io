+++
title = "ListOT and PCF"
date = 2024-10-26T00:00:00+08:00
draft = false
+++

Here are my [Slides.](</ox-hugo/Public Key PCF.pdf>)

The design of PCF follows two paradigms in general.

-   The "DPF+LPN" approach, where one uses binary-tree-based DPF as FSS for point functions for comparison functions to generate correlations on sparse vectors (e.g. sparse COT, sparse VOLE), and then compress the correlation with an appropriate Learning Parity with Noise (LPN) assumption. Notice that we want to achieve super-polynomial "stretch" so that the LPN assumption must support a "fast" evaluation algorithm. Existing works uses Expand-Accumulate LPN (<a href="#citeproc_bib_item_1">Boyle et al. 2022</a>) assumption or the Variable-Density LPN assumption (<a href="#citeproc_bib_item_5">Couteau and Ducros 2023</a>; <a href="#citeproc_bib_item_2">Boyle et al. 2020</a>).
-   Another line of work focuses on working with more expressive HSS/FSS and propose to use public key operation to generate each correlation. Notice that the LPN assumption only requires matrix-vector multiplication operation and is generally considered to be much "lighter" than public-key operations (e.g., exponentiation modulo an RSA modulus or lattice operations with superpolynomial modulus to noise ratio). The advantage of this line of work is that the constructions are very simple and elegant. One work by Orlandi et al. uses Pailliar to construct PCF for OT (<a href="#citeproc_bib_item_6">Orlandi, Scholl, and Yakoubov 2021</a>) while a recent work by Bui et al. uses Naor-Reingold PRF to achieve the same goal (<a href="#citeproc_bib_item_3">Bui et al. 2024</a>). One interesting observation is that the "public-key PCF" constructions can generate OT correlations directly, while constructions in the previous genre usually generate Correlated OT first.

In Asiacrypt 2024, a new paradigm is proposed, trying to achieve a middle ground between the two genres (<a href="#citeproc_bib_item_4">Couteau et al. 2024</a>). The work builds on the framework of (<a href="#citeproc_bib_item_3">Bui et al. 2024</a>) but replaces the Naor-Reingold constrained PRF with a much simpler RO design. This brings the following changes:

-   RO is much more efficient than NR-PRF.
-   By using RO, we loose the homomorphism of NR-PRF. As a result, we can only achieve the "ListOT" correlation, rather than standard OT.

ListOT means that the sender can get two lists \\(L\_0, L\_1\\) while the receiver gets an index \\(b\\), a "list index" \\(v\\), and a value \\(y\\). The values should satisfy the following requirements.

-   **Correctness:** Viewing \\(L\_0, L\_1\\) as Python `dict`'s, it should hold that \\(y = L\_b[v]\\).
-   **Sender Security:** The missing values in \\(L\_0, L\_1\\) should appear pseudorandom to the receiver.
-   **Receiver Security:** The index \\(b\\) should be pseudorandom to the sender (notice that the \\(v\\) value is **not** pseudorandom.)

By running benchmark on the **extension phase** (without setup), the authors claim that their protocol achieves better throughput than SoftSpokenOT at the same communication level. Compared with previous PCF designs, the new protocol shows advantage in every metric. Compared with the state of the art LPN-based PCG (<a href="#citeproc_bib_item_7">Raghuraman, Rindal, and Tanguy 2023</a>), their protocol still falls behind in terms of performance.

One very nice feature of their protocol and public-key PCF in general, is that they support the PKI-style setup. This means that the parties only need to interact in one round to exchange the public keys of each other. Then they can generate the correlations by only local computation. This is the minimal communication possible to generate multiparty correlations and is highly desirable in practice.

## References

<style>.csl-entry{text-indent: -1.5em; margin-left: 1.5em;}</style><div class="csl-bib-body">
  <div class="csl-entry"><a id="citeproc_bib_item_1"></a>Boyle, Elette, Geoffroy Couteau, Niv Gilboa, Yuval Ishai, Lisa Kohl, Nicolas Resch, and Peter Scholl. 2022. “Correlated Pseudorandomness from Expand-Accumulate Codes.” In <i>Advances in Cryptology – CRYPTO 2022</i>, edited by Yevgeniy Dodis and Thomas Shrimpton, 13508:603–33. Cham: Springer Nature Switzerland. <a href="https://doi.org/10.1007/978-3-031-15979-4_21">https://doi.org/10.1007/978-3-031-15979-4_21</a>.</div>
  <div class="csl-entry"><a id="citeproc_bib_item_2"></a>Boyle, Elette, Geoffroy Couteau, Niv Gilboa, Yuval Ishai, Lisa Kohl, and Peter Scholl. 2020. “Correlated Pseudorandom Functions from Variable-Density LPN.” In <i>2020 IEEE 61st Annual Symposium on Foundations of Computer Science (FOCS)</i>, 1069–80. Durham, NC, USA: IEEE. <a href="https://doi.org/10.1109/FOCS46700.2020.00103">https://doi.org/10.1109/FOCS46700.2020.00103</a>.</div>
  <div class="csl-entry"><a id="citeproc_bib_item_3"></a>Bui, Dung, Geoffroy Couteau, Pierre Meyer, Alain Passelègue, and Mahshid Riahinia. 2024. “Fast Public-Key Silent OT and More from Constrained Naor-Reingold.”</div>
  <div class="csl-entry"><a id="citeproc_bib_item_4"></a>Couteau, Geoffroy, Lalita Devadas, Srinivas Devadas, Alexander Koch, and Sacha Servan-Schreiber. 2024. “QuietOT: Lightweight Oblivious Transfer with a Public-Key Setup.”</div>
  <div class="csl-entry"><a id="citeproc_bib_item_5"></a>Couteau, Geoffroy, and Clément Ducros. 2023. “Pseudorandom Correlation Functions from Variable-Density LPN, Revisited.”</div>
  <div class="csl-entry"><a id="citeproc_bib_item_6"></a>Orlandi, Claudio, Peter Scholl, and Sophia Yakoubov. 2021. “The Rise of Paillier: Homomorphic Secret Sharing and Public-Key Silent OT.”</div>
  <div class="csl-entry"><a id="citeproc_bib_item_7"></a>Raghuraman, Srinivasan, Peter Rindal, and Titouan Tanguy. 2023. “Expand-Convolute Codes for Pseudorandom Correlation Generators from LPN.”</div>
</div>
