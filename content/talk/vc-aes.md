+++
title = "Efficient Random Vector Commitment from AES"
draft = false
+++

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
