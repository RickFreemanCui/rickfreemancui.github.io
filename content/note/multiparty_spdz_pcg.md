+++
title = "PCG for Multiparty SPDZ Triples"
draft = false
+++

Unlike the two party case, currently we do not know how to construct a PCG for the multiparty (\\(\geq 3\\) parties) SPDZ correlation where the seed size is \\(\mathsf{polylog}(N)\\) bits, where \\(N\\) is the number of triples to be generated. The best effort has seed size \\(\mathsf{poly}(p) \cdot \sqrt{N}\\) where \\(p\\) is the number of parties. A work in PKC21 sketched the basic idea (check out my [slide](/ox-hugo/Auth-Triples.pptx) for this paper), and a CRYPTO25 paper improved the dependency on the number of parties to \\(\mathsf{poly}(p)\\) (also check out my [slide](/ox-hugo/Multiparty-DPF-C25.pdf) for this paper.)

After some consideration, I roughly categorize this problem as coming up with a sublinear communication protocol for 3-party computation. The task at hand is that \\(P\_i\\) has a secret index \\(\alpha\\), \\(P\_j\\) has a secret index \\(\beta\\), while \\(P\_k\\) has a secret payload \\(\Delta\\). The three parties run the functionality \\(\mathcal{F}\_{3PC}\\) to get shares of \\(e\_{\alpha + \beta} \cdot \Delta\\) where the addition is on some integer ring. At the time being I am pretty grim about the possiblity of constructing this functionality using the 2-party DPF functionality alone.

Also I checked out the FHE-based approach (like the preprocessing protocol in the original SPDZ paper.) In LWE-based encryption schemes (which is the only scheme supporting distributed decryption for multiple parties to the best of our knowledge,) the distributed decryption process introduces noise, which is removed by rounding. It seems pretty hard to perform rounding in the distributed setting.
