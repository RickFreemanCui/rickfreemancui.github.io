+++
title = "Digital Signature from Regular Syndrome Decoding and VOLEitH"
draft = false
+++

This is a project that runs in the ****Lattice**** lab, starting
from Dalao Hanlin, who first envisioned the possibility of substituting
LWE-based cryptography with LPN (spoiler alert we currently do not know
how to achieve this goal). A significant goal is to construct a digital
signature a la Dilithium at least in terms of performance.

Alas, the **Fiat-Shamir with Abort** technique does not work directly with
LPN, although some folks have come up with variants of the LPN assumption
to accommendate with this technqiue (e.g. (<a href="#citeproc_bib_item_2">“Durandal: A Rank Metric Based Signature Scheme SpringerLink” n.d.</a>)). We
consider the status quo unsatisfactory.

Luckily, the MPC-in-the-Head branch is constantly being optimized,
with the state-of-the-art proposed under the name "VOLE-in-the-Head"
(<a href="#citeproc_bib_item_1">Baum et al. 2023</a>) in Crypto 2023. We tried
this new framework on the RSD problem at the first moment. Anyway, this
framework proves to be effective when proving small circuits, and our work
is summarized in a [PKC 2024 paper]({{< relref "resolved" >}}).

I have given three talks about this topic:

-   One in the group meeting last year (by that time we call the project
    SPED). [Slides](/ox-hugo/SPED.pdf)
-   One on AC 2023 at Guangzhou during Rump Session <span class="timestamp-wrapper"><span class="timestamp">&lt;2023-12-06 Wed&gt;</span></span>
    [Slides](/ox-hugo/ReSolveD-AC23-RumpSession.pdf)
-   One on PKC 2024 at Syndey <span class="timestamp-wrapper"><span class="timestamp">&lt;2024-04-16 Tue&gt;</span></span>.  [Slides](/ox-hugo/ReSolveD-PKC2024.pdf)

## References

<style>.csl-entry{text-indent: -1.5em; margin-left: 1.5em;}</style><div class="csl-bib-body">
  <div class="csl-entry"><a id="citeproc_bib_item_1"></a>Baum, Carsten, Lennart Braun, Cyprien Delpech De Saint Guilhem, Michael Klooß, Emmanuela Orsini, Lawrence Roy, and Peter Scholl. 2023. “Publicly Verifiable Zero-Knowledge and Post-Quantum Signatures from VOLE-in-the-Head.” In <i>Advances in Cryptology – CRYPTO 2023</i>, edited by Helena Handschuh and Anna Lysyanskaya, 14085:581–615. Cham: Springer Nature Switzerland. <a href="https://doi.org/10.1007/978-3-031-38554-4_19">https://doi.org/10.1007/978-3-031-38554-4_19</a>.</div>
  <div class="csl-entry"><a id="citeproc_bib_item_2"></a>“Durandal: A Rank Metric Based Signature Scheme SpringerLink.” n.d. https://link.springer.com/chapter/10.1007/978-3-030-17659-4\_25. Accessed October 17, 2023.</div>
</div>
