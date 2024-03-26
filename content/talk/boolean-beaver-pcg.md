+++
title = "PCG for Boolean Beaver Triples"
draft = false
+++

Generating Boolean Beaver triples has always been an intriguing
problem.  On one hand, Overdrive-type FHE-based solutions offers
asympototically-good solutions, and for suitable field size the
concrete efficiency is also considered state-of-the-art. On the other
hand, the current best practice for generating authenticated Boolean
Beaver triples remains MASCOT-type COT-based protocols, which has
communication of \\(O(N^2 m)\\) for generating \\(m\\) triples among \\(N\\)
parties.

I guess this is a follow-up of [Ring-LPN Talk]({{< relref "ring_lpn_pcg" >}}).

There has been a number of works (<a href="#citeproc_bib_item_1">Bombar et al. 2024</a>, <a href="#citeproc_bib_item_2">2023</a>; <a href="#citeproc_bib_item_3">Boyle et al. 2022</a>, <a href="#citeproc_bib_item_5">2020b</a>, <a href="#citeproc_bib_item_4">2020a</a>) trying to change the
status quo, with the ultimate goal of creating a concretely efficient
end-to-end MPC protocol. I made some [slides](/ox-hugo/FOLEAGE-DPF.pdf) about them.

## References

<style>.csl-entry{text-indent: -1.5em; margin-left: 1.5em;}</style><div class="csl-bib-body">
  <div class="csl-entry"><a id="citeproc_bib_item_1"></a>Bombar, Maxime, Dung Bui, Geoffroy Couteau, Alain Couvreur, Clément Ducros, and Sacha Servan-Schreiber. 2024. “FOLEAGE: \$mathbb\\F\\\_4\$OLE-Based Multi-Party Computation for Boolean Circuits.”</div>
  <div class="csl-entry"><a id="citeproc_bib_item_2"></a>Bombar, Maxime, Geoffroy Couteau, Alain Couvreur, and Clément Ducros. 2023. “Correlated Pseudorandomness from the Hardness of Quasi-Abelian Decoding.”</div>
  <div class="csl-entry"><a id="citeproc_bib_item_3"></a>Boyle, Elette, Geoffroy Couteau, Niv Gilboa, Yuval Ishai, Lisa Kohl, Nicolas Resch, and Peter Scholl. 2022. “Correlated Pseudorandomness from Expand-Accumulate Codes.” In <i>Advances in Cryptology – CRYPTO 2022</i>, edited by Yevgeniy Dodis and Thomas Shrimpton, 13508:603–33. Cham: Springer Nature Switzerland. <a href="https://doi.org/10.1007/978-3-031-15979-4_21">https://doi.org/10.1007/978-3-031-15979-4_21</a>.</div>
  <div class="csl-entry"><a id="citeproc_bib_item_4"></a>Boyle, Elette, Geoffroy Couteau, Niv Gilboa, Yuval Ishai, Lisa Kohl, and Peter Scholl. 2020a. “Efficient Pseudorandom Correlation Generators from Ring-LPN.” In <i>Advances in Cryptology – CRYPTO 2020</i>, edited by Daniele Micciancio and Thomas Ristenpart, 12171:387–416. Cham: Springer International Publishing. <a href="https://doi.org/10.1007/978-3-030-56880-1_14">https://doi.org/10.1007/978-3-030-56880-1_14</a>.</div>
  <div class="csl-entry"><a id="citeproc_bib_item_5"></a>———. 2020b. “Correlated Pseudorandom Functions from Variable-Density LPN.” In <i>2020 IEEE 61st Annual Symposium on Foundations of Computer Science (FOCS)</i>, 1069–80. Durham, NC, USA: IEEE. <a href="https://doi.org/10.1109/FOCS46700.2020.00103">https://doi.org/10.1109/FOCS46700.2020.00103</a>.</div>
</div>
