+++
title = "Fully Linear PCP"
draft = false
+++

This is a Crypto 2019 paper by Boneh et al. In this paper the authors
utilize the fact that the verifier can only make linear queries to the
instance string and the PCP/IOP proof string in order to make a
decision. Building on this property, we can design proof systems that
allow proving statements that are shared among multiple verifiers.
This proof system in particular appear useful for the GMW transformation,
which is the topic of another talk.

Also this work appear to be dual to our previous work [MPC in Multi Heads]({{< relref "multi_heads" >}})
