+++
draft = false
+++

## <span class="org-todo done DONE">DONE</span> My first post <span class="tag"><span class="tag1">tag1</span><span class="_category1">@category1</span></span> {#my-first-post}

This is my post body


## papers {#papers}


### <span class="org-todo done DONE">DONE</span> MPC in Multi Heads {#multi_heads}

This paper is about extending the classical [IKOS07] MPC in the Head
framework to prove statements that are shared among multiple provers.

This is somewhat dual to the distributed ZKP object. I gave a talk about
this Crypto 2019 paper [Fully Linear PCP](#flpcp)

Published as _MPC-in-Multi-Heads: A Multi-Prover Zero-Knowledge Proof
System._ In European Symposium on Research in Computer Security
(pp. 332-351). Springer, Cham. [PDF](https://link.springer.com/content/pdf/10.1007%2F978-3-030-88428-4_17.pdf)


### <span class="org-todo done DONE">DONE</span> Simple GCZK {#simple_gczk}

In this paper we describe a simple GCZK protocol that works in the
reverse order compared to [JKO16]. Here the prover is the garbler and
the verifier use cut-and-choose to verify that the correct
verification circuit is garbled. In this way, the protocol can be made
public-coin.

Published as _A Simple Post-Quantum Non-interactive Zero-Knowledge
Proof from Garbled Circuits. In International Conference on
Information Security and Cryptology (pp. 269-280). Springer, Cham._
[PDF](https://eprint.iacr.org/2021/1068.pdf)


### <span class="org-todo done DONE">DONE</span> Authenticated Garbling From Correlated OT {#cot_ag}

Inspired by [DILO22], we investigate what is the bare minimum we can
achieve using the correlated OT functionality in actively secure
two-party computation. We found that with the following two techniques

-   block COT and compression idea of [DILO22]
-   dual execution

We can achieve constant (up to 5 bits per AND gate) overhead in terms of
one-way communication compared to semi-honest half-gate [ZRE15].


#### One-way Communication {#one-way-communication}

The one-way communication result is published as _Actively Secure
Half-Gates with Minimum Overhead under Duplex Networks. In Advances in
Cryptology–EUROCRYPT 2023: 42nd Annual International Conference on the
Theory and Applications of Cryptographic Techniques, Lyon, France,
April 23–27, 2023, Proceedings, Part II (pp. 35-67). Cham: Springer
Nature Switzerland._ [PDF](https://link.springer.com/content/pdf/10.1007/978-3-031-30617-4_2.pdf)


#### Two-way Communication {#two-way-communication}

We then extended the result towards minimizing two-way communication.
We manage to achieve \\( 2\kappa + \lambda + C \\) bits per AND gate
where \\( \kappa \\) is the computational security parameter and \\(
\lambda \\) is the statistical security parameter. This work is
available at [ePrint 2023/278](https://eprint.iacr.org/2023/278).


### <span class="org-todo done DONE">DONE</span> Optimal One-time Signature {#cs_wots}

Hash-based signature is to be standardized by NIST <span class="timestamp-wrapper"><span class="timestamp">&lt;2024-02-28 Wed&gt;</span></span>. So
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


### <span class="org-todo done DONE">DONE</span> LPN-based Signature from VOLE in the Head {#resolved}

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

I gave several talks about this project, summarized in [this post](#resolved_talk).


## Notes {#notes}


### <span class="org-todo done DONE">DONE</span> My first note {#first_note}

My first note is about the CIS 2019 winter school


## Talks {#talks}


### <span class="org-todo done DONE">DONE</span> My first talk {#first_talk}

My first talk is about memory-hard functions but they are kind of lost


### <span class="org-todo done DONE">DONE</span> Fully Linear PCP {#flpcp}

This is a Crypto 2019 paper by Boneh et al. In this paper the authors
utilize the fact that the verifier can only make linear queries to the
instance string and the PCP/IOP proof string in order to make a
decision. Building on this property, we can design proof systems that
allow proving statements that are shared among multiple verifiers.
This proof system in particular appear useful for the GMW transformation,
which is the topic of another talk.

Also this work appear to be dual to our previous work [MPC in Multi Heads](#multi_heads)


### <span class="org-todo done DONE">DONE</span> Sublinear GMW {#sublinear_gmw}

This is a follow-up work of [Fully Linear PCP](#flpcp).

-   LATTICE group meeting at <span class="timestamp-wrapper"><span class="timestamp">&lt;2021-10-27 Wed&gt; </span></span> [Slides](/ox-hugo/Sublinear-GMW.pptx)
-   Meeting with Huawei at <span class="timestamp-wrapper"><span class="timestamp">&lt;2021-11-18 Thu&gt; </span></span> [Slides](/ox-hugo/Sublinear-GMW-Huawei.pptx)


### <span class="org-todo done DONE">DONE</span> Ring-LPN PCG {#ring_lpn_pcg}

The \\( n^2 \\) computational overhead of PCGs for the OLE/MT correlation
has long been a trouble and only recently have we come up with some
creative solution (for authenticated triples over \\( \mathbb{F}\_2 \\)).

This is a Crypto 2020 paper that shows how to create such a
correlation over \\( \mathbb{F}\_{2^{\rho}} \\) using Ring-LPN. I recall
giving talks about this construction in various occacions but the
details have been lost now. <span class="timestamp-wrapper"><span class="timestamp">&lt;2024-02-28 Wed&gt;</span></span>

Anyway, here is the slides I have prepared for a LATTICE group meeting
at Dec. 2021 [Slides](</ox-hugo/Ring-LPN PCG.pptx>).


### <span class="org-todo done DONE">DONE</span> Authenticated Garbling from Compressed Randomness {#dilo}

This is a Crypto 2022 paper that describes how to construct
authenticated garbled circuit using correlations that allow efficient
PCGS (e.g., MT, VOLE). Using the AGC, we can run actively secure 2PC
afterwards.

This work inspired us to conduct a follow-up work [Authenticated Garbling From Correlated OT](#cot_ag).

Here is the slides I have prepared [Slides](/ox-hugo/Auth-GC-from-VOLE.pdf).


### <span class="org-todo todo TODO">TODO</span> PCG for Garbled Circuit Correlations {#gcpcgpcf}

This is a Eurocrypt 2023 submission that describes the application of
EA-LPN in constructing PCF for garbled circuit correlations. They also
present three applications of their construction, albeit not very
convincing in their practical values.

I gave a talk about this paper and also discussed the merit of it at
<span class="timestamp-wrapper"><span class="timestamp">&lt;2024-02-27 Tue&gt;</span></span>. Here is the [ipe source](Slides/GC-PCG-PCF.ipe).


### <span class="org-todo done DONE">DONE</span> Efficient Random Vector Commitment from AES {#vc-aes}

Since random vector commitment is used extensively in MPCitH and
VOLEitH applications, with some of them being post quantum signatures,
which is efficiency sensitive (e.g. TLS needs fast authentications for
smooth browsing experience), it's a natural question to optimize
this component.

One possible way to do this is to replace the cryptograhpic hash
function invocation at the bottom layer of the GGM tree with AES-based
hash functions which are relatively lightweight when the key is fixed.

Two groups of researchers have proposed similar solutions. Bui, Cong,
and Delpech de Saint Guilhem proposed a CCR-hash-based construction
which they instantiate with the [GKWY20] construction with a
\\(\lambda\\)-bit permutation. The down-side is that AES only offers
128-bit block size and they have to resort to Rijndael for higher
security parameters, which kind of goes against the initial goal of
optimization since AES being fast is largely due to the instruction
set AES-NI.

So Prof. Guo tries to tackle this problem using only AES. We are
having an discussion about this topic at <span class="timestamp-wrapper"><span class="timestamp">&lt;2024-03-06 Wed&gt;</span></span>. Here are
the [slides](/ox-hugo/AES-VC.pdf).


### <span class="org-todo done DONE">DONE</span> PCG for Boolean Beaver Triples {#boolean-beaver-pcg}

Generating Boolean Beaver triples has always been an intriguing
problem.  On one hand, Overdrive-type FHE-based solutions offers
asympototically-good solutions, and for suitable field size the
concrete efficiency is also considered state-of-the-art. On the other
hand, the current best practice for generating authenticated Boolean
Beaver triples remains MASCOT-type COT-based protocols, which has
communication of \\(O(N^2 m)\\) for generating \\(m\\) triples among \\(N\\)
parties.

I guess this is a follow-up of [Ring-LPN Talk](#ring_lpn_pcg).

There has been a number of works (<a href="#citeproc_bib_item_2">Bombar et al. 2024</a>, <a href="#citeproc_bib_item_3">2023</a>; <a href="#citeproc_bib_item_4">Boyle et al. 2022</a>, <a href="#citeproc_bib_item_6">2020b</a>, <a href="#citeproc_bib_item_5">2020a</a>) trying to change the
status quo, with the ultimate goal of creating a concretely efficient
end-to-end MPC protocol. I made some [slides](/ox-hugo/FOLEAGE-DPF.pdf) about them.

## References

<style>.csl-entry{text-indent: -1.5em; margin-left: 1.5em;}</style><div class="csl-bib-body">
  <div class="csl-entry"><a id="citeproc_bib_item_1"></a>Baum, Carsten, Lennart Braun, Cyprien Delpech De Saint Guilhem, Michael Klooß, Emmanuela Orsini, Lawrence Roy, and Peter Scholl. 2023. “Publicly Verifiable Zero-Knowledge and Post-Quantum Signatures from VOLE-in-the-Head.” In <i>Advances in Cryptology – CRYPTO 2023</i>, edited by Helena Handschuh and Anna Lysyanskaya, 14085:581–615. Cham: Springer Nature Switzerland. <a href="https://doi.org/10.1007/978-3-031-38554-4_19">https://doi.org/10.1007/978-3-031-38554-4_19</a>.</div>
  <div class="csl-entry"><a id="citeproc_bib_item_2"></a>Bombar, Maxime, Dung Bui, Geoffroy Couteau, Alain Couvreur, Clément Ducros, and Sacha Servan-Schreiber. 2024. “FOLEAGE: \$mathbb\\F\\\_4\$OLE-Based Multi-Party Computation for Boolean Circuits.”</div>
  <div class="csl-entry"><a id="citeproc_bib_item_3"></a>Bombar, Maxime, Geoffroy Couteau, Alain Couvreur, and Clément Ducros. 2023. “Correlated Pseudorandomness from the Hardness of Quasi-Abelian Decoding.”</div>
  <div class="csl-entry"><a id="citeproc_bib_item_4"></a>Boyle, Elette, Geoffroy Couteau, Niv Gilboa, Yuval Ishai, Lisa Kohl, Nicolas Resch, and Peter Scholl. 2022. “Correlated Pseudorandomness from Expand-Accumulate Codes.” In <i>Advances in Cryptology – CRYPTO 2022</i>, edited by Yevgeniy Dodis and Thomas Shrimpton, 13508:603–33. Cham: Springer Nature Switzerland. <a href="https://doi.org/10.1007/978-3-031-15979-4_21">https://doi.org/10.1007/978-3-031-15979-4_21</a>.</div>
  <div class="csl-entry"><a id="citeproc_bib_item_5"></a>Boyle, Elette, Geoffroy Couteau, Niv Gilboa, Yuval Ishai, Lisa Kohl, and Peter Scholl. 2020a. “Efficient Pseudorandom Correlation Generators from Ring-LPN.” In <i>Advances in Cryptology – CRYPTO 2020</i>, edited by Daniele Micciancio and Thomas Ristenpart, 12171:387–416. Cham: Springer International Publishing. <a href="https://doi.org/10.1007/978-3-030-56880-1_14">https://doi.org/10.1007/978-3-030-56880-1_14</a>.</div>
  <div class="csl-entry"><a id="citeproc_bib_item_6"></a>———. 2020b. “Correlated Pseudorandom Functions from Variable-Density LPN.” In <i>2020 IEEE 61st Annual Symposium on Foundations of Computer Science (FOCS)</i>, 1069–80. Durham, NC, USA: IEEE. <a href="https://doi.org/10.1109/FOCS46700.2020.00103">https://doi.org/10.1109/FOCS46700.2020.00103</a>.</div>
  <div class="csl-entry"><a id="citeproc_bib_item_7"></a>“Durandal: A Rank Metric Based Signature Scheme SpringerLink.” n.d. https://link.springer.com/chapter/10.1007/978-3-030-17659-4\_25. Accessed October 17, 2023.</div>
</div>


### <span class="org-todo done DONE">DONE</span> Digital Signature from Regular Syndrome Decoding and VOLEitH {#resolved_talk}

This is a project that runs in the ****Lattice**** lab, starting
from Dalao Hanlin, who first envisioned the possibility of substituting
LWE-based cryptography with LPN (spoiler alert we currently do not know
how to achieve this goal). A significant goal is to construct a digital
signature a la Dilithium at least in terms of performance.

Alas, the **Fiat-Shamir with Abort** technique does not work directly with
LPN, although some folks have come up with variants of the LPN assumption
to accommendate with this technqiue (e.g. (<a href="#citeproc_bib_item_7">“Durandal: A Rank Metric Based Signature Scheme SpringerLink” n.d.</a>)). We
consider the status quo unsatisfactory.

Luckily, the MPC-in-the-Head branch is constantly being optimized,
with the state-of-the-art proposed under the name "VOLE-in-the-Head"
(<a href="#citeproc_bib_item_1">Baum et al. 2023</a>) in Crypto 2023. We tried
this new framework on the RSD problem at the first moment. Anyway, this
framework proves to be effective when proving small circuits, and our work
is summarized in a [PKC 2024 paper](#resolved).

I have given three talks about this topic:

-   One in the group meeting last year (by that time we call the project
    SPED). [Slides](/ox-hugo/SPED.pdf)
-   One on AC 2023 at Guangzhou during Rump Session <span class="timestamp-wrapper"><span class="timestamp">&lt;2023-12-06 Wed&gt;</span></span>
    [Slides](/ox-hugo/ReSolveD-AC23-RumpSession.pdf)
-   One on PKC 2024 at Syndey <span class="timestamp-wrapper"><span class="timestamp">&lt;2024-04-16 Tue&gt;</span></span>.  [Slides](/ox-hugo/ReSolveD-PKC2024.pdf)

## References

<style>.csl-entry{text-indent: -1.5em; margin-left: 1.5em;}</style><div class="csl-bib-body">
  <div class="csl-entry"><a id="citeproc_bib_item_1"></a>Baum, Carsten, Lennart Braun, Cyprien Delpech De Saint Guilhem, Michael Klooß, Emmanuela Orsini, Lawrence Roy, and Peter Scholl. 2023. “Publicly Verifiable Zero-Knowledge and Post-Quantum Signatures from VOLE-in-the-Head.” In <i>Advances in Cryptology – CRYPTO 2023</i>, edited by Helena Handschuh and Anna Lysyanskaya, 14085:581–615. Cham: Springer Nature Switzerland. <a href="https://doi.org/10.1007/978-3-031-38554-4_19">https://doi.org/10.1007/978-3-031-38554-4_19</a>.</div>
  <div class="csl-entry"><a id="citeproc_bib_item_2"></a>Bombar, Maxime, Dung Bui, Geoffroy Couteau, Alain Couvreur, Clément Ducros, and Sacha Servan-Schreiber. 2024. “FOLEAGE: \$mathbb\\F\\\_4\$OLE-Based Multi-Party Computation for Boolean Circuits.”</div>
  <div class="csl-entry"><a id="citeproc_bib_item_3"></a>Bombar, Maxime, Geoffroy Couteau, Alain Couvreur, and Clément Ducros. 2023. “Correlated Pseudorandomness from the Hardness of Quasi-Abelian Decoding.”</div>
  <div class="csl-entry"><a id="citeproc_bib_item_4"></a>Boyle, Elette, Geoffroy Couteau, Niv Gilboa, Yuval Ishai, Lisa Kohl, Nicolas Resch, and Peter Scholl. 2022. “Correlated Pseudorandomness from Expand-Accumulate Codes.” In <i>Advances in Cryptology – CRYPTO 2022</i>, edited by Yevgeniy Dodis and Thomas Shrimpton, 13508:603–33. Cham: Springer Nature Switzerland. <a href="https://doi.org/10.1007/978-3-031-15979-4_21">https://doi.org/10.1007/978-3-031-15979-4_21</a>.</div>
  <div class="csl-entry"><a id="citeproc_bib_item_5"></a>Boyle, Elette, Geoffroy Couteau, Niv Gilboa, Yuval Ishai, Lisa Kohl, and Peter Scholl. 2020a. “Efficient Pseudorandom Correlation Generators from Ring-LPN.” In <i>Advances in Cryptology – CRYPTO 2020</i>, edited by Daniele Micciancio and Thomas Ristenpart, 12171:387–416. Cham: Springer International Publishing. <a href="https://doi.org/10.1007/978-3-030-56880-1_14">https://doi.org/10.1007/978-3-030-56880-1_14</a>.</div>
  <div class="csl-entry"><a id="citeproc_bib_item_6"></a>———. 2020b. “Correlated Pseudorandom Functions from Variable-Density LPN.” In <i>2020 IEEE 61st Annual Symposium on Foundations of Computer Science (FOCS)</i>, 1069–80. Durham, NC, USA: IEEE. <a href="https://doi.org/10.1109/FOCS46700.2020.00103">https://doi.org/10.1109/FOCS46700.2020.00103</a>.</div>
  <div class="csl-entry"><a id="citeproc_bib_item_7"></a>“Durandal: A Rank Metric Based Signature Scheme SpringerLink.” n.d. https://link.springer.com/chapter/10.1007/978-3-030-17659-4\_25. Accessed October 17, 2023.</div>
</div>


## misc {#misc}


### <span class="org-todo done DONE">DONE</span> My first misc {#first_misc}

My first misc is proabably clarify my CV

Reference to [Custom ID](#test_id)


#### Cusom ID Test {#test_id}

This is the content of a subtree with custom id.


## <span class="org-todo done DONE">DONE</span> Hongrui's Personal Information {#about}

<span class="icons-item"> <a href="https://github.com/freemanrickcui" target="_blank"><i class="fab fa-github"></i></a></span>
<span class="icons-item"> <a href="https://www.stackoverflow.com/users/8865477/rick-freeman" target="_blank"><i class="fab fa-stack-overflow fa-1x"></i></a></span>
<span class="icons-item"> <a href="https://orcid.org/0000-0002-6203-413X" target="_blank"><i class="fab fa-orcid fa-1x"></i></a></span>
<span class="icons-item"> <a href="https://scholar.google.com/citations?user=bWNvN0UAAAAJ" target="_blank"><i class="fab fa-google fa-1x"></i></a></span>
<span class="icons-item"> <a href="mailto:freemanrickcui@outlook.com"><i class="fas fa-envelope fa-1x"></i></a></span>
<span class="icons-item"> <a href="/gpg_public_key.txt"><i class="fas fa-key fa-1x"></i></a></span>

Ph.D. Student in Cryptography<br />
[LATTICE Group, Shanghai Jiao Tong University](https://crypto.sjtu.edu.cn/)


### Interests {#interests}

-   Theoretical Cryptography
-   Multiparty Computation
-   MPC-in-the-Head


### Education {#education}

-   MSc in Computer Science, Shanghai Jiao Tong University, 2022
-   BSc in Information Security, Shanghai Jiao Tong University, 2019


### About {#about}

I am a second-year Ph.D. student majoring in Cryptography at SJTU. My
past projects include MPC-in-the-Head, COT-AG, and ReSolveD. I am very
interested in objects that are both theoretically interesting and of
practical significance.
