+++
title = "计算复杂性课程笔记"
author = ["崔泓睿"]
draft = false
+++

This is my notes of the 18-19-1 course \`\`Computational Complexity''.


## Lecture 1: Introduction {#lecture-1-introduction}


### Introduction {#introduction}

This is the lecture note of Prof. Fu's _Computational Complexity_ (not
to be confused with the _Computational Complexity: Advanced Topics_ in
the second semester). As Prof. Fu is not following strictly the
structure of the book, I consider it necessary to take notes of the
essential contents taught in the lectures, and subsequently organized
them as a series.

The notes will be updated every week, sometimes twice a week. Some
elaborations based on reading from the book may also be added here.


#### Auxiliary Course Information {#auxiliary-course-information}

Information about the teaching assistant:

| Name          | 杨启哲                              |
|---------------|----------------------------------|
| Phone Number  | 15901917102                         |
| Email Address | <mailto:spacepenguin9494@gmail.com> |

Also homework will be handed down to us through email. I chose the
school's email address to communicate with him.


#### An Introduction to Computational Complexity {#an-introduction-to-computational-complexity}

There are some classical problems in computer science (or mathematics at
large):

1.  Diophantine Problem (i.e. finding integer solutions to linear
    equations)

2.  Matching Problem

3.  Vertex Cover Problem

4.  Graph Isomorphism Problem

There are most established results regarding the algorithmic solution to
these problems. The Diophantine Problem is known to be **undecidable** --
there does not exist algorithm to solve this problem. For the Matching
Problem, there is an algorithm that solves this problem in polynomial
time. The Vertex Cover Problem is **NP-Complete** -- any polynomial
algorithm that solves this problem would implies that
\\(\mathbf{P}=\mathbf{NP}\\), which is highly unlikely. The Graph
Isomorphism Problem is not known to be in \\(\mathbf{P}\\), but it is surely
in \\(\mathbf{NP}\\).

Complexity of computation is about classifying various problems in
computer science and comparing such classes. Throughout the course, some
main techniques in theoretical computer science would be explained,
including:

1.  Recursion Theoretical Method

2.  Algebraic Method

3.  Combinatorial Method

4.  Probabilistic Method


### Time Complexity {#time-complexity}


#### Definition of Turing Machine {#definition-of-turing-machine}

First the definition of Turing Machine is introduced. Informally, we
have a k-tape, unidirectional, input-read-only Turing Machine is
represented by a tuple \\(\mathbb{M}=(\Gamma, Q, \delta)\\), where \\(\Gamma\\)
is its finite alphabet, \\(Q\\) is its finite state sets, and
\\(\delta:Q\times\Gamma^{k}\to Q \times \Gamma^{k-1}\times \\{L,S,R\\}^{k}\\)
is its transition function. It should be noted that without loss of
generality we assume \\(q\_\text{start},q\_\text{halt}\in Q\\) and
\\(\\{{0,1,\triangleleft,\boxempty}\\}\subset \Gamma\\).

It is clear that the full configuration of a Turing Machine consists of
its 1. state, 2. contents of working tapes, and 3. head position. (As we
will see later, any Turing Machine \\(\mathbb{M}\\) can be transformed into
another _Oblivious Turing Machine_ \\(\mathbb{M}^\prime\\) whose head
movement is only dependent on its input length.)


#### Definition of Problems {#definition-of-problems}

After defining the Turing Machine, we need to describe the set of
problems suitable to the aforementioned definition, and the conditions a
Turing Machine solves this problem. This gives rise to the definition of
_problems_. A function \\(f:\\{0,1\\}^{\*}\to\\{0,1\\}^{\*}\\) is called a
problem, and a TM \\(\mathbb{M}\\) computes/solves this problem if for every
string \\(x\\) of finite length, whenever \\(x\\) is written on \\(\mathbb{M}\\)'s
input tape, \\(\mathbb{M}\\) halts with \\(y=f(x)\\) written on its output tape.
This can be written compactly as \\(\mathbb{M}(x)=f(x)\\) for all
\\(x\in\\{0,1\\}^{\*}\\).

We shall be focused on decisional problems
\\(d:\\{0,1\\}^{\*}\to\\{0,1\\}d:\\{0,1\\}^{\*}\to\\{0,1\\}^{}\\) from now on. A
language \\(L\\) is a set of finite strings. The term "\\(\mathbb{M}\\) accepts
\\(L\\)" means that for any string \\(x\\), \\[\mathbb{M}(x)=1\iff x\in L\\]

Some exercise on designing Turing Machines are provided. Actually there
more elaborate exercises on Arora's book. I will defer the solutions to
these interesting problems to a compilation of solutions to exercises in
Chapter 1 of Arora's book.


#### Time Constructible Functions {#time-constructible-functions}

Then the notion of _time constructible functions_ is introduced. There
are two definitions provided in this lecture. There are two definitions,
where the second one implies the first one.

Suppose \\(T:\mathbb{N}\to\mathbb{N}\\) and \\(T>n\\), then

1.  \\(T\\) is time constructible if there exists a TM that computes the
    function \\(1^n\mapsto \llcorner{T(n)}\lrcorner\\) in \\(O(T(n))\\) steps.

2.  \\(T\\) is time constructible if there exists a TM that halts at exactly
    \\(T(n)\\) steps.

By the fact that a counter that a counter TM that counts up to \\(n\\) runs
in \\(O(n)\\) steps (this can be proved using a simple counting trick), one
can confirm that the second definition implies the first one. From now
on we will only consider time constructible functions, since if a
function \\(T\\) is time constructible, we can hard-wire the TM in \\(T\\)'s
definition into arbitrary TM \\(\mathbb{M}\\), resulting a TM that will
exactly halt in \\(O(T(n))\\) time. This technique is called **hardwiring a
clock to a Turing Machine**.


#### Oblivious Turing Machine {#oblivious-turing-machine}

A Turing Machine is _oblivious_ if its head position at step \\(i\\) only
depends on its input length \\(|x|\\) and \\(i\\) itself. Actually, any TM can
be transformed into an oblivious one, from the technique that transform
arbitrary finite number of tapes into one read-write tape Turing
Machine. This will nevertheless introduce a quadratic overhead.


#### Church-Turing Thesis {#church-turing-thesis}

Church-Turing Thesis states that every physically realizable computing
device can be simulated by a Turing Machine. As there are (possibly)
infinitely many models of computing devices that may rely on bizarre
physical phenomenon, this is only a thesis so far, rather than a
theorem. Note that there is a strong version of this thesis, stating
that the overhead of such simulation is only polynomial in the length of
input.


#### Universal Turing Machine {#universal-turing-machine}

The fact that Turing Machine is finite sparkles the idea that as a
mathematical object, Turing Machine can be encoded, and furthermore
written on the input tape of other Turing Machine. This led to the
notation of _Universal Turing Machine_, which takes the description of
some Turing Machine \\(\mathbb{M}\\), its input \\(x\\), and outputs the result
\\(\mathbb{M}(x)\\) as \\(\mathbb{M}\\) would.

More precisely, Prof. Fu presented a simple scheme to encode the
transition function \\(\delta\\) of a Turing Machine, that I will skip due
to its triviality.

There are also two assumptions introduced regarding the encoding of
Turing Machine:

1.  Every TM is represented by infinitely many binary strings.

2.  Every finite binary string (canonically) represents a TM.

The first assumption can be satisfied by sticking arbitrary \\(1\\)'s to the
back of the encoding and regard them as the encodings of a same TM.
While the second restriction can be satisfied by mapping all the invalid
encodings to some dummy TM.

Encoding of Turing Machine gives rise to the efficient enumeration of
Turing Machine. By fixing an effective bijection between \\(\\{0,1\\}^{\*}\\)
and \\(\mathbb{N}\\), we can enumerate all the Turing Machine by natural
numbers.


## Lecture 2: Time Complexity {#lecture-2-time-complexity}

The main body of this lecture is devoted to the proof of the complexity
of universal Turing Machine. The main idea behind the proof is a
construction that minimize the movement of tapes by splitting the tape
into sparse zones. The analysis of this algorithm is called _amortized
analysis_ and maybe of independent interest. Prof. Fu has taught us the
essence of this proof, and I think it is most beneficial for me to work
out the fine details by myself in this note.


### Simulation Overhead of Universal Turing Machine {#simulation-overhead-of-universal-turing-machine}

Suppose \\(L\\) is computed by an time \\(O(T(n))\\) TM for some time
constructible \\(T\\). Then there is a universal TM that decides \\(L\\) in time
\\(O(T(n)\log(T(n)))\\). Where the constant hidden in the asymptotic
expression is only dependent on the number of tapes, alphabet size, and
the number of states of the simulated TM.

Another theorem and its corollary are also given in this lecture as
exercises.


### Diagonalization and Universal Turing Machine {#diagonalization-and-universal-turing-machine}

Using the technique of _diagonalization_, one can prove that there
exists some problems that is not decidable by any Turing Machine. Two of
them are introduced in Arora's book and in this lecture, they are

1.  \\(\mathsf{UC}:=\\{x|\mathbb{M}\_x(x)\text{ does not halt or outputs }1\\}\\),

2.  \\(\mathsf{HALT}:=\\{\langle
       \alpha,x\rangle|\mathbb{M}\_\alpha(x)\text{ halts within finite
       steps}\\}\\).

While the first one is strongly related to the diagonalization
technique, and second one is _reducible_ to the first one.


### Speedup Theorem {#speedup-theorem}

In the last part of this lecture, the speedup theorem is introduced.
There are two versions, and only the simple (and somewhat trivial)
version is introduced. This basically translate to using a machine with
bigger alphabet and bigger states to compress several steps in a TM into
one in a bigger TM. This theorem is proposed by Hennie and Stearns in
the context that omitting the constant factor is justifiable when
defining the \\(\mathbf{DTIME}(f(n))\\). I will omit the proof here.


## Lecture 3: Time Complexity {#lecture-3-time-complexity}

In this lecture the complexity class \\(\mathbf{P}\\) is defined by
computing the union of all the languages that is computable in
polynomial time. Formally, Let \\(T:\mathbb{N}\to\mathbb{N}\\) be a time
function, and a language (problem) is in \\(\mathbf{DTIME}(T)\\) if there
exists some constant \\(c>0\\) and a Turing Machine \\(\mathbb{M}\\) that
decides \\(L\\) in time \\(c\cdot T(n)\\).

The complexity class \\(\mathbf{P}\\) is defined by the union of all
polynomially computable languages (decisional problems), i.e.
\\[\mathbf{P}:= \mathop{\bigcup}\_{c\geq 1}\mathbf{DTIME}(n^c)\\]
Similarly, we have
\\[\mathbf{EXP}:= \mathop{\bigcup}\_{c\geq 1}\mathbf{DTIME}(2^{n^c})\\]


### Nondeterministic Turing Machine {#nondeterministic-turing-machine}

For pure theoretical interest, the _Non-Deterministic Turing Machine_
(NDTM) is introduced. This model incorporates the notion of "guessing"
into computation, and is not considered physically realizable.

The reason why a NDTM is considered capable of "guessing" is that it
allows two transition functions, and therefore on every input, a tree of
binary choices are made possible. Apart from that, a special state
called _accepting state_ is introduced, and some NDTM accepts on some
input string means that there _exists_ a path of binary choices such
that the machine halts with the accepting state. Note that this also
implies that it should be very hard to negate the result of some
Non-Deterministic Turing Machine, since it takes exponential steps to
determine its result (with no extra information). This trivial result is
related to the fact that \\(\mathbf{NP}\neq\mathbf{coNP}\\).

There are two points about NDTM in my notes on that lecture, they are:

-   That some Non-Deterministic Turing Machine runs in time \\(T(n)\\) means
    that every brunch of choices halts within \\(T(n)\\) steps.

-   A string \\(x\in\\{0,1\\}^{\*}\\) is accepted by some NDTM \\(\mathbb{N}\\) means
    that there exists a sequence of choice such that the machine
    \\(\mathbb{N}\\) on input \\(x\\) halts with the accepting state (contrarily,
    \\(\mathbb{N}\\) refuses \\(x\\) means that for every sequence of choice, the
    machine refuses this string). A language \\(L\subset\\{0,1\\}^{\*}\\) is
    accepted by a NDTM \\(\mathbb{N}\\) means that
    \\(x\in L \iff \mathbb{N}(x)=1\\).

Many classic algorithmic problems have trivial solutions on a NDTM. For
instance, let's consider the traveling salesman's problem. An NDTM can
simply use the two transition functions to guess a binary string that
corresponds to some canonical representation of a permutation of all the
vertices on graph, and then verify that such vertices actually consist
of a path, and such a path satisfies the distance requirement. If so, it
enters accepting state, or else, it halts without accepting. Trivially,
the language
\\[L := \\{{\langle{G,d}\rangle|G\text{ has a cycle of length less than }d}\\}\\]
can be accepted by such a NDTM.


### Classifying Complexity by Nondeterministic Turing Machine {#classifying-complexity-by-nondeterministic-turing-machine}

Following the definition of \\(\mathbf{DTIME}(T(n))\\), we can come up with
\\(\mathbf{NTIME}(T(n))\\). A language \\(L\in\mathbf{NTIME}(T(n))\\) if and
only if when there exists some NDTM \\(\mathbb{N}\\) that accepts \\(L\\) in
time \\(T(n)\\).

Naturally, we can define the complexity class that consists of all the
problems that can be polynomial-time determined by Nondeterministic
Turing Machine, i.e. \\(\mathbf{NP}\\).

\\[\mathbf{NP}:= \mathop{\bigcup}\_{c\geq 1} \mathbf{NTIME}(n^c)\\]

Similarly, extending polynomial to exponential leads to the definition
of \\(\mathbf{NEXP}\\).

\\[\mathbf{NEXP}:= \mathop{\bigcup}\_{c\geq 1} \mathbf{NTIME}(2^{n^c})\\]

The slides state that there is surprisingly small number of result
concerning the connection between the two versions of definitions of
complexity classes, except for some trivial results. And I remember
there is similar result in Arora's book. The trivial result is that
\\[\mathbf{P}\subseteq\mathbf{NP}\subseteq\mathbf{EXP}\subseteq\mathbf{NEXP}.\\]


### Universal Nondeterministic Turing Machine {#universal-nondeterministic-turing-machine}

It turns out it is rather easy to design a universal Turing Machine when
the "guessing" ability is at hand. Intuitively, this seems like the
result of the loosely definition of a Nondeterministic TM accepting a
string. By extending the running time of some NDTM linearly, the number
of possible brunches increases exponentially. And perhaps that is why
such a universal machine is so easy to design.

But first the notion of _snapshot_ is introduced. A snapshot consists of
the preimage of the transition function \\(\delta\\). Recall that transition
function has the form
\\[\delta:\Gamma^k\times Q \mapsto \Gamma^{k-1}\times Q \times\\{{L,S,R}\\}^{k}\\]
And therefore, a snapshot for a \\(k\\) tape Turing Machine at step \\(i\\) is
\\(\langle{a\_1,\ldots,a\_k,q}\rangle\in\Gamma^{k}\times Q\\), where
\\(a\_1,\ldots,a\_k\\) correspond to the \\(k\\) symbols under the read/write
heads at step \\(i\\), and \\(q\\) is the state in the state register at that
step.

Note that compared to the _configuration_ of a Turing Machine, a
snapshot is much more compact. More importantly, a snapshot alone is
able to determine the one-step computation process. This observation
(computation on a Turing Machine is local) is important to the proof of
Cook-Levin theorem.

In the lecture Prof. Fu presented a universal NDTM that takes three
working tapes:

1.  To guess a snapshot sequence;

2.  To guess a choice sequence;

3.  To verify the content of \\(k-1\\) working tapes is consistent with the
    computation process.

By the definition of NDTM, if some string \\(x\\) is accepted by a NDTM, it
means that there is a choice sequence (and therefore a snapshot
sequence) that leads the computation to a accepting state. Now, by the
above definition, such a sequence surely occurs in the universal TM's
choice tree, which means that \\(x\\) is also accepted by this universal
NDTM.

Assuming that the Turing Machine to be simulated runs in time
\\(T(n)\\)[^fn:1] The simulation takes time at most \\(c\cdot T(n)\\), where \\(c\\)
is a constant only dependent on the machine being simulated (ergo a
constant). A naive idea would be to represent the \\(k\\) tapes on the third
tape of the universal machine, and verification of each working tape
takes no more than \\(k\cdot T(n)\\) steps.


### Deterministic Time Hierarchy Theorem {#deterministic-time-hierarchy-theorem}

The time hierarchy theorem states that by allowing more time to a
(Deterministic) Turing Machine, the language it is capable of deciding
strictly grows. This and the nondeterministic version of this theorem
are both proved using the diagonalization technique, which is introduced
in the third chapter of Arora's book.

If \\(f\\) and \\(g\\) are time-constructible functions, and
\\(f(n)\log(f(n))=o(g(n))\\), then
\\(\mathbf{DTIME}(f(n))\subsetneq\mathbf{DTIME}(g(n))\\).

Define the Turing Machine \\(\mathbb{M}\\) that runs in time \\(c\cdot g(n)\\):
On input \\(x\\), \\(\mathbb{M}\\) computes \\(\mathbb{U}(x,x)\\) clocked with
\\(g(|x|)\\). If the simulation halts before the timer ends, \\(\mathbb{M}\\)
outputs the negated result; Else, it outputs \\(1\\).

Let \\(L\\) be the language accepted by \\(\mathbb{M}\\), then by definition
\\(L\in\mathbf{DTIME}(g(n))\\). Suppose by contradiction,
\\(\mathbf{DTIME}(f(n))=\mathbf{DTIME}(g(n))\\), we have
\\(L\in\mathbf{DTIME}(f(n))\\). Let \\(\mathbb{M}^\prime\\) be the machine
that computes \\(L\\) in \\(O(f(n))\\) time. Then since the simulation of
\\(\mathbb{M}\prime\\) takes at most \\(c^\prime\cdot f(n)\log(f(n))\\), we
have that we can find a representation
\\(\llcorner{\mathbb{M}^\prime}\lrcorner\\) large enough to be simulated
by universal TM \\(\mathbb{U}\\). Now consider
\\(\mathbb{M}(\llcorner{\mathbb{M}^\prime}\lrcorner,\llcorner{\mathbb{M}^\prime}\lrcorner)\\).
By the definition of universal TM, this value is \\(\mkern
1.5mu\overline{\mkern-1.5mu\mathbb{M}^\prime(\llcorner{\mathbb{M}^\prime}\lrcorner)\mkern-1.5mu}\mkern
1.5mu\\).  However, since \\(\mathbb{M}^\prime\\) and \\(\mathbb{M}\\) decide
the same language, this value should also be
\\(\mathbb{M}^\prime(\llcorner{\mathbb{M}^\prime}\lrcorner)\\), leading to
a contradiction.


## Lecture 4: Time Complexity {#lecture-4-time-complexity}

In the previous lecture we have learned the deterministic Time Hierarchy
theorem. By a simple observation that
\\[n^c\cdot2^{n^c}\approx2^{n^c}<2^{2^{n^c}}\\] We can define a
exponential hierarchy. That is, following the definition of
\\(\mathbf{EXP}\\), we can define
\\[\mathbf{2EXP}:=\mathop{\bigcup}\_{c\ge 1}2^{2^{n^c}}.\\]

Similarly, \\(\mathbf{3EXP},\mathbf{4EXP},\ldots\\) can be defined. Finally,
we define
\\[\mathbf{ELEMENTARY}:=\mathbf{EXP}\cup\mathbf{2EXP}\cup\ldots.\\]

Although the exact functionality of such definition is unclear for the
time being, I am sure when the course proceeds, those will come natural
to me.


### Nondeterministic Time Hierarchy Theorem {#nondeterministic-time-hierarchy-theorem}

Before stating this theorem a brief history of this theorem is
introduced. First of all, Cook proved in 1970 that
\\(\mathbf{NTIME}(r(n))\subsetneq\mathbf{NTIME}(r^\prime(n))\\) if
\\(1\leq r(n) < r^\prime(n)\\). I wrote in my notebook that this is a
slightly weaker result compared to the one stated in the textbook[^fn:1].

The theorem stated in the textbook and this lecture is as follows.

If \\(f\\) and \\(g\\) are time-constructible functions and \\(f(n+1)=o(g(n))\\),
then \\(\mathbf{NTIME}(f(n))\subsetneq\mathbf{NTIME}(g(n))\\).

The proof uses a technique called "lazy diagonalization", which is
necessary for the proof with nondeterministic Turing Machine. As
discussed earlier, negating the output of a nondeterministic machine is
not so easy, since all the brunches need to be computed. And therefore
to negate only one output in an exponential number of machines makes the
negation efficient (this actually means focusing the attention on
problems of smaller scale). The proof is proposed by Zak.

Like previous proofs using diagonalization, we need to define a Turing
Machine and its deciding language such that it lies in the set
\\(\mathbf{NTIME}(g(n))\setminus\mathbf{NTIME}(f(n))\\)[^fn:2]. The machine
we define has five working tapes[^fn:3], and its accepting strings have
the form \\(1^n\\). The function of its working tapes is as follows (we
denote the machine as \\(\mathbb{V}\\)):

1.  The heads of the first working tape and the input tape moves right at
    full speed until the machine halts. The first tape writes \\(1\\) at the
    first cell and then writes string of the form \\(0^n1\\). Let
    \\(h\_0,h\_1,\ldots\\) be the index of the \\(1\\)'s on the first working tape.

2.  The second working tape enumerates NDTM
    \\(\mathbb{L}\_1,\mathbb{L}\_2,\ldots\\) hardwired with a \\(g(n)\\) -timer.
    Upon generating \\(\mathbb{L}\_i\\), the machine _computes_ universal NDTM
    on input \\((\llcorner{\mathbb{L}\_i}\lrcorner, 1^{h\_{i-1}+1})\\). Notice
    that in this step, our machine is required to explore every brunch of
    the universal TM's choice, And this step takes exponential (in the
    length of \\(h\_{i-1}+1\\)) time. Upon acquiring the result, \\(\mathbb{V}\\)
    writes \\(1\\) on location \\(h\_i\\) of the first working tape (this gives
    the definition of \\(h\_i\\)), and the result on the second working tape
    (right after the description of \\(\mathbb{L}\_{i}\\)).

3.  Suppose the input is of form \\(1^n\\) with \\(n>1\\). After the input is
    scanned, \\(\mathbb{V}\\) distinguishes between the two cases:
    1.  If \\(n=h\_i\\), accepts \\(1^n\\) if \\(\mathbb{L}\_{i}(1^{h\_{i-1}+1})=0\\);
        refuses it otherwise.

    2.  If \\(h\_i<n<h\_{i+1}\\), \\(\mathbb{V}\\) simulates
        \\(\mathbb{L}\_{i}(1^{n+1})\\) for \\(g(n)\\) steps and outputs the
        simulation result.

Let \\(L\\) be the language decided by \\(\mathbb{V}\\), and by its definition,
\\(L\in\mathbf{NTIME}(g(n))\\). Suppose by contradiction, we have
\\(L\in\mathbf{NTIME}(f(n))\\), then we consider the machine \\(\mathbb{M}\\)
that decides \\(L\\) and runs in time \\(c \cdot f(n)\\). By simple padding, we
can find a encoding of \\(\mathbb{M}\\) that is of length \\(n^\prime\\) long
enough that \\(c\cdot f(n^\prime+1) < g(n^\prime)\\). By the definition of
\\(\mathbb{V}\\), the positive integer set is partitioned into intervals of
forms \\((h\_{i-1},h\_i]\\). Suppose \\(n\in(h\_{i-1},h\_i]\\). Then we have
\\[\begin{aligned}
    \mathbb{V}(1^{h\_{i-1} + 1}) &= \mathbb{L}\_{i-1}(1^{{h\_{i-1} + 2}})\\\\
    \mathbb{L}\_{i-1}(1^{{h\_{i-1} + 2}}) &= \mathbb{V}(1^{{h\_{i-1} + 2}}) \\\\
    &\hspace{.5em}\vdots \\\\
    \mathbb{V}(1^{h\_{i}-1}) &= \mathbb{L}\_{i-1}(1^{h\_{i}})\\\\
    \mathbb{L}\_{i-1}(1^{h\_{i}}) &= \mathbb{V}(1^{h\_i})\\\\
    \mathbb{V}(1^{h\_i}) &\ne \mathbb{V}(1^{h\_{i-1} + 1})
    \end{aligned}\\] This concludes the proof, since by the assumption we
have \\(\mathbb{V}(1^{h\_{i-1} + 1})\ne \mathbb{V}(1^{h\_{i-1} + 1})\\).

I think there are some interesting thought experiment about the above
proof. What if we set the requirement of \\(g\\) even higher, say
\\(f(n+c)=o(g(n))\\) for arbitrary constant \\(c\\)? Would this make the proof
harder? Maybe the core question is that what is the connection between
the difference in time function, and the language that lies in the
interval.


### Gap Theorem {#gap-theorem}

When we consider the opposite of time-constructible functions, some
interesting result can occur. Gap theorem is one of such astonishing
examples.

Suppose \\(r(x)>x\\) is a total computable function. Then there exists some
total computable function \\(b(x)\\) such that
\\(\mathbf{DTIME}(b(x))=\mathbf{DTIME}(r(b(x)))\\).

The proof uses a smart pigeon-hole argument.

Define a sequence of numbers \\(k\_0<k\_1<k\_2<\ldots<k\_x\\) by
\\[\begin{aligned}
    k\_0 &= 0\\\\
    k\_{n+1} &= r(k\_{n})+1.
    \end{aligned}\\] Then the set \\([0,r(k\_x)]\\) is partitioned in to \\(x+1\\)
disjoint intervals.

Now define a property \\(P(i,k)\\). This property is satisfied when for
every \\(j\leq i\\) and input \\(z\\) of length \\(i\\), we have \\(\mathbb{M}\_{j}(z)\\)
either halts within \\(k\\) steps or does not halt in \\(r(k)\\) steps.

Consider the number \\(n\_i=\sum\_{j\leq i}|\Gamma\_j|^i\\), which is the
number of all inputs of size \\(i\\) to machine
\\(\mathbb{M}\_0,\ldots,\mathbb{M}\_i\\). And consider the aforementioned
partition of set \\([0. r(k\_{n\_i})]\\). Every input corresponds to a running
time, and by pigeon-hole argument, these \\(n\_i\\) numbers cannot fill all
\\(n\_i +1\\) intervals. Meaning there is a minimal \\(j\\) such that \\(P(i,k\_j)\\)
is true. Let \\(b(i)\\) be such \\(k\_j\\).

Now that we defined the function \\(b(n)\\), lets consider
\\(\mathbf{DTIME}(r(b(n)))\\). Since by the definition of \\(b(n)\\), property
\\(P(i,b(i))\\) is true for all \\(i\\), for every language in
\\(\mathbf{DTIME}(r(b(n)))\\), we can find \\(x\\) long enough that the Turing
Machine that decide it has number \\(i<|x|\\). By the definition of \\(b(n)\\),
this machine halts in \\(b(|x|)\\) steps. Meaning that
\\(L\in\mathbf{DTIME}(b(n))\\).

It is also noted in the slides that by time hierarchy theorem, \\(b(n)\\) is
not time-constructible. Actually I think assuming \\(b(n)\\) is
time-constructible, this implies \\(b(n)\cdot\log(b(n))=\Omega(r(b(n)))\\),
I do not understand the further contradiction.


## Lecture 5: NP Completeness {#lecture-5-np-completeness}

Before the introduction of NP completeness (the Cook-Levin theorem), an
alternative definition of \\(\mathbf{NP}\\) is introduced. This definition
capture the intuition that \\(\mathbf{NP}\\) language are those that are
easy to verify, i.e. having short proofs that can be verified
efficiently. The following theorem states the equivalence between the
two definitions.

\\(L\in\mathbf{NP}\\) if and only if there is a polynomial \\(p\\) and a P-time
verifier \\(\mathbb{M}\\) such that \\(\forall x \in \\{0,1\\}^{\*}\\),
\\(x\in L \iff \exists u\in\\{0,1\\}^{p(|x|)} \land \mathbb{M}(x,u)=1\\).

If \\(x\in L\\) and \\(u\in\\{0,1\\}^{p(|x|)}\\) is such that \\(\mathbb{M}(x,u)=1\\),
then \\(u\\) is called a _certificate_ or _witness_ for \\(x\\), with respect to
\\(\mathbb{M}\\) and \\(L\\).

The theorem is actually trivial to prove. Assuming such certificate for
some language \\(L\\) exists, then a NDTM can simply guess the certificate
first (takes \\(p(|x|)\\) steps) and then simulate \\(\mathbb{M}\\) (the
verifier) to determine the result. In the other direction, the
certificate for a string \\(x\\) can simply be the sequence of choices made
by the NDTM. The verifier just apply the transition function according
to the certificate, and accepts \\(x\\) iff. the accepting state is reached.

This certificate-based definition actually reveals the fact that
\\(\mathbf{NP}\\) problems are easy to verify (in polynomial-time), while
\\(\mathbf{P}\\) problems are easy to solve (in polynomial-time). Some
examples of \\(\mathbf{NP}\\) problems include:

-   Independent Set, Traveling Salesman, Subset Sum, 0/1 Programming,
    Hamiltonian Path (\\(\mathbf{NP}\\) -complete)

-   Graph Isomorphism, Factoring (unknown)

-   Linear Programming, Primality (actually in \\(\mathbf{P}\\))


### Karp Reduction {#karp-reduction}

_Reduction_ allows us to compare the difficulty between two problems,
even though both of the problem may lack concrete solutions. _Karp
Reduction_ is perhaps the simplest one (without additional properties).
Suppose \\(L,L^\prime\\) are two languages, we say \\(L\\) is _Karp reducible_
to \\(L^\prime\\) if there exists some polynomial time computable function
\\(r\\) such that \\(x\in L\iff r(x)\in L^\prime\\).

Note that the reduction function \\(r\\) actually maps \\(L\\) onto \\(L^\prime\\)
(i.e. a surjection), and that means computing \\(L^\prime\\) is _at least as
hard as_ computing \\(L\\). We introduce two notions:

-   We say \\(L\\) is \\(\mathbf{NP}\\) -hard if
    \\(\forall L^\prime \in \mathbf{NP}\\), \\(L^\prime \le\_{K}L\\).

-   We say \\(L\\) is \\(\mathbf{NP}\\) -complete if \\(L\in\mathbf{NP}\\) and \\(L\\) is
    \\(\mathbf{NP}\\)-hard.

For this lecture and the next one, we answer the question "is there an example
of \\(\mathbf{NP}\\) -complete" problem? First of all, a natural idea may arise from
the certificate-based definition of \\(\mathbf{NP}\\) and universal Turing Machine.
Consider the following language: \\[\mathtt{TMSAT} :=
\\{{\langle{\alpha,x,1^n,1^t}\rangle|\exists u\in\\{0,1\\}^{n}\text{ s.t. }
\mathbb{M}\_{\alpha}(x,u) \text{ outputs 1 in t stpes}}\\}\\]

Clearly any language in \\(\mathbf{NP}\\) can be Karp reduced to
\\(\texttt{TMSAT}\\).


### Complementary of NP {#complementary-of-np}

A language \\(L\subseteq \\{0,1\\}^{\*}\\) is in
\\(\mathbf{coNP}:=\\{{L|\mkern 1.5mu\overline{\mkern-1.5muL\mkern-1.5mu}\mkern 1.5mu\in\mathbf{NP}}\\}\\),
iff. there exists a polynomial \\(p\\) and a Turing Machine \\(\mathbb{M}\\)
such that \\(x\in\L\iff \forall u\in\\{0,1\\}^{p(|x|)}\\),
\\(\mathbb{M}(x,u)=1\\).


### Padding Technique {#padding-technique}

There is a theorem related to the polynomial hierarchy[^fn:1].

If \\(\mathbf{P}=\mathbf{NP}\\), then \\(\mathbf{EXP}=\mathbf{NEXP}\\).

We only have to prove \\(\mathbf{NEXP}\subseteq\mathbf{EXP}\\), since
inclusion in the other direction is trivial. Suppose
\\(L\in\mathbf{NEXP}\\), then \\(\exists c\geq 1\\) and Turing Machine
\\(\mathbb{M}\\) such that \\(x\in L\iff\exists u\in\\{0,1\\}^{2^{{|x|}^c}}\\),
\\(\mathbb{M}(x,u)=1\\).

Now define the following language
\\(L^\prime:=\\{{x1^{2^{{|x|}^c}}|x\in L}\\}\\). By definition,
\\(L^\prime\in\mathbf{NP}\\) (the input is long enough now). By assumption,
\\(L^\prime\in P\\). \\(\forall x\in\\{0,1\\}^{\*}\\), by padding \\(1^{2^{{|x|}^c}}\\)
to the back of \\(x\\), and calls the polynomial time algorithm on the
padded result, \\(x\\) can be computed in \\(1^{2^{{|x|}^{c^\prime}}}\\) time
for some constant \\(c^\prime\\). This implies \\(\mathbf{EXP}=\mathbf{NEXP}\\).


### Cook-Levin Theorem {#cook-levin-theorem}

Cook-Levin theorem gives for the first time, a natural problem
(\\(\mathtt{3SAT}\\)) that is \\(\mathbf{NP}\\) -complete. This embarks on many
other \\(\mathbf{NP}\\) -complete problems since these problems can be
reduced to \\(\text{\texttt{3SAT}}\\). Before the proof of Cook-Levin
Theorem, the preliminary knowledge of conjunctive normal form is
introduced.


#### Conjunctive Normal Form {#conjunctive-normal-form}

A CNF formula has the form \\(\land\_{i}(\lor\_j{v\_{ij}})\\), where \\(v\_{ij}\\)
is a literal (a variable or its negation) and \\({v\_{ij}}\\) is a clause.

A \\(k\\) -CNF is a CNF where all the clauses have at most \\(k\\) literals. A
CNF is _satisfiable_ if there exists an assignment of variables such
that the value of the \\(CNF\\) is true.

\\(\mathtt{2CNF}\in\mathbf{P}\\)

Consider a graph of \\(2m\\) nodes, where \\(m\\) is the number of variables in
the CNF. Each pair of node represents the 0/1 assignment of a variable.
A clause \\(x\lor y\\) is interpreted as two edges: \\(\bar{x}\to y\\) and
\\(\bar{y}\to x\\) (If \\(x=0\\) then \\(y=1\\) and vise versa). This CNF is not
satisfiable if and only if there is a path on the graph from some \\(z\\) to
\\(\bar{z}\\).

\\(\text{\texttt{SAT}}\le\_{K}\text{\texttt{3SAT}}\\)

This can be proved by padding dummy literal into the clause. E.g.
Consider \\(v\_1\lor v\_2\lor \ldots\lor v\_n\\), we can introduce \\(n-3\\) dummy
variables \\(y\_1,\ldots,y\_{n-3}\\), and the resulting clause is
\\[(v\_1\lor v\_2\lor y\_1)\land(\mkern 1.5mu\overline{\mkern-1.5muy\_1\mkern-1.5mu}\mkern 1.5mu\lor v\_3\lor y\_2)\land\ldots\land(\mkern 1.5mu\overline{\mkern-1.5muy\_{k-3}\mkern-1.5mu}\mkern 1.5mu\lor v\_{n-1}\lor v\_{n})\\]
Notice that the previous CNF is satisfiable if and only if the latter
one is. And therefore we have that the satisfiable property is
inherited.


## Lecture 6: Cook-Levin Theorem {#lecture-6-cook-levin-theorem}

Some preliminary knowledge before the lecture is introduced. They are:

1.  The Boolean formula \\(x=y\\) can be expressed in CNF form
    \\((\bar{x}\lor y)\land(x\lor \bar{y})\\).

2.  Any Boolean function \\(f:\\{0,1\\}^{l}\to\\{0,1\\}\\) can be represented by
    an equivalent \\(l\\) -variable CNF, whose size is at most \\(l\cdot 2^{l}\\).

The second point is similar to the _maximum solution_ concept in digital
circuit. The conversion is quite simple. Consider the truth table of
\\(f\\), of which some entry corresponds to \\(f=0\\). For each such entry, we
convert it into a clause as follows: if some variable \\(x\\) in that entry
is \\(0\\), then add \\(x\\) to the clause; else, add \\(\bar{x}\\). In this way, we
ensure this restriction is encoded. By taking the logical and of all the
terms, the whole function can be encoded.

The rest of this lecture is dedicated to the proof of Cook-Levin
theorem, i.e. \\(\text{\texttt{3SAT}}\\) is \\(\mathbf{NP}\\) -complete.
Formally, we need to prove two results:

1.  \\(\text{\texttt{3SAT}}\in\mathbf{NP}\\) (trivial)

2.  \\(\forall L\in\mathbf{NP}, L\le\_{K}\text{\texttt{3SAT}}\\)

The first result is trivial to prove, using the certificate based
definition of \\(\mathbf{NP}\\). For the second result, remember that we
proved \\(\text{\texttt{SAT}}\le\_{K}\text{\texttt{3SAT}}\\), this means that
we only need to prove \\(L\le\_{K}\text{\texttt{SAT}}\\) because this with
the transitivity of reduction implies the second result.

Since we need to prove a result that is true to all the \\(\mathbf{NP}\\)
languages, there is no resource we can rely on other than its
definition. In this proof we actually utilize the certificate-based
definition and represent the computation process as a CNF formula. The
formula is satisfiable iff. some certificate exists of polynomial length
and makes the verifier outputs 1.

A naive idea would be to consider the computation of the verifier (by
which we denote \\(\mathbb{M}\\)) as a \\(|x|+p(|x|)\\) -length Boolean function.
But that would incur complexity trouble, since the resulting formula
would have exponential size. The key idea behind this proof is that for
each step of \\(\mathbb{M}\\), the transition function only relies on the
\\(k\\) symbols under the heads and the state information, which altogether
can be encoded to a constant length. And the steps of transition is a
polynomial, therefore the resulting CNF would be of polynomial length,
and is satisfiable iff. there is a certificate that leads \\(\mathbb{M}\\)
outputs 1.

I think the idea behind this proof is that a TM can not compute
functions with too many high-degree variables. While a \\(l\cdot 2^l\\)
variable formula can achieve this, such exaggeration is not necessary,
since computation on a TM is highly local.

Now we present the proof sketch of Cook-Levin theorem.

Let \\(L\in\mathbf{NP}\\) has verifier \\(\mathbb{M}\\), with running time
\\(T(n)\\), certificate length \\(p(n)\\) and its alphabet can be encoded into
\\(c\_1\\) bits. Without loss of generality, we can assume a snapshot of
\\(\mathbb{M}\\) can be encoded into \\(c\_2\\) bits. Consider \\(x\in L\\) and its
verification process on \\(\mathbb{M}\\). The computation can be represented
by a sequence of snapshots \\(z\_1,\ldots,z\_{T(|x|+p(|x|))}\\), where without
loss of generality we let
\\(z\_1=\langle{q\_{start},\triangleleft,\boxempty,\ldots,\boxempty}\rangle\\)
and
\\(z\_{T(|x|+p(|x|))}=\langle{q\_{halt},\triangleleft,1,\boxempty,\ldots,\boxempty}\rangle\\)
to be constant. We also make the assumption that \\(\mathbb{M}\\) is
oblivious.

Since \\(\mathbb{M}\\) is deterministic, we only need to verify

1.  the input is well-formed (of the form \\(xu|u\in\\{0,1\\}^{p(|x|)}\\))

2.  the snapshots are well formed (the first one and the last one are the
    constants as required and the rest according to the transition
    function).

The only tricky part is how to verify every snapshot satisfies the
transition function. The observation here is that each snapshot is only
dependent on

-   its previous snapshot (contains the state)

-   the symbol on each tapes at that step.

Note that by assumption, \\(\mathbb{M}\\) is oblivious, meaning at the
beginning of the reduction, we can first append \\(x\\) with \\(1^{p(|x|)}\\) to
find out the head movement of \\(\mathbb{M}\\), and then use this
information to proceed with the reduction. Altogether, \\(z\_i\\) only
depends on \\(z\_{i-1}\\), \\(y\_{\text{inputpos}(i)}\\), and
\\(z\_{\text{prev}(i)}\\). And its total number of variables is a constant.
Altogether, the reduction takes polynomial time and the resulting CNF
has polynomial size. This concludes the proof of Cook-Levin theorem.

Some properties of Cook-Levin theorem are that:

-   the reduction can be done in logspace;

-   the reduction is actually a Levin reduction (there exists a bijection
    between the certificates of the two languages);

-   the reduction is parsimonious (#(certificates for \\(x\\)) =
    \#(certificates for \\(r(x)\\) in \\(\text{\texttt{SAT}}\\))).


### Decision versus Search {#decision-versus-search}

The next theorem proves that if the decision version of some
\\(\mathbf{NP}\\) -complete language is solved, its witness can also be found
in polynomial time.

If \\(\mathbf{P}=\mathbf{NP}\\), then there exists a P-time TM \\(\mathbb{M}\\)
that \\(\forall L\in\mathbf{NP}\\) on input \\(x\in L\\), it outputs a
certificate \\(u\in\\{0,1\\}^{p(|x|)}\\) for \\(x\\).

The proof is very easy, using the fact that the reduction to
\\(\text{\texttt{SAT}}\\) is actually a Levin-reduction.


### \\(\mathbf{coNP}\\) Completeness {#mathbf-conp-completeness}

The complementary problem \\(\texttt{TAUTOLOGY}\\) of \\(\text{\texttt{SAT}}\\)
is actually a \\(\mathbf{coNP}\\) complete problem. The following theorem
states this fact.

\\(\texttt{TAUTOLOGY} := \\{{\varphi| \varphi(x)=1, \forall x\in\\{0,1\\}^{n}}\\}\\)
is \\(\mathbf{coNP}\\) complete.

First we prove that \\(\texttt{TAUTOLOGY}\in\mathbf{coNP}\\), which is
trivial since its complementary problem is just \\(\text{\texttt{SAT}}\\).
In other words, whether \\(x\not\in\texttt{TAUTOLOGY}\\) can be determined
by an NDTM in polynomial time.

Secondly, consider any language \\(L\in\mathbf{coNP}\\). Since
\\(\mkern 1.5mu\overline{\mkern-1.5muL\mkern-1.5mu}\mkern 1.5mu\in\mathbf{NP}\\),
we have that
\\(\mkern 1.5mu\overline{\mkern-1.5muL\mkern-1.5mu}\mkern 1.5mu\le\_{K}\text{\texttt{SAT}}\\),
and
\\(\texttt{TAUTOLOGY}=\mkern 1.5mu\overline{\mkern-1.5mu\text{\texttt{SAT}}\mkern-1.5mu}\mkern 1.5mu\\).
By the definition of Karp reduction, the process is a reduction from \\(L\\)
to \\(\texttt{TAUTOLOGY}\\).


## Lecture 7: Implications of Cook-Levin Theorem {#lecture-7-implications-of-cook-levin-theorem}


### Efficiently Verifiable Theorems is NPC {#efficiently-verifiable-theorems-is-npc}

In this lecture the implications of Cook Levin theorem is discussed. In
particular, consider the following language with respect to a familiar axiomatic
system \\(A\\).
\\[\lang{THEOREM} = \set{(\phi,1^{|\phi|^c})|\phi\text{ has a formal proof of
length}
\le |\phi|^c \text{ in } A}\\]

This is the finite version of Hilbert's Theorem and essentially Godel's
question. But it is easy to see that this language is \NP-complete. The proof
relies on

1.  In most familiar axiomatic system, verification time is polynomial in
    proof length
2.  \\(\SAT \le\_{K} \lang{THEOREM}\\) since satisfying CNF has the assignment of
    variables as proof.

So Godel essentially palpicitated (or raised actually ) the famous question of
\P vs. \NP.


### Berman-Hartmanis Conjecture {#berman-hartmanis-conjecture}

The conjecture is "all NP-complete problems are polynomially isomorphic". By
"polynomially isomorphic", we mean there is a efficient isomorphism \\(\sigma\\)
(and \\(\sigma^{-1}\\)) between the two languages. (Efficiency means polynomial in
the length of input).

The evidence to this conjecture is the following facts:

-   \\(A \le\_{K}^{1} B\\) for all NPC languages \\(A\\) and \\(B\\)
-   If \\(A \le\_{K}^{1} B\\) and \\(B\le\_{K}^{1} A\\), then \\(A\cong\_p B\\).

By \\(\le\_{K}^{1}\\) we mean the karp reduction is injective. Another important
implication is that Berman-Hartmanis Conjecture would implies \\(\P\ne\NP\\),
since for sake of contradiction, consider if \\(\P = \NP\\) then any language in
\\(\NP\\) is trivially NPC. Now consider the "density" of languages. We consider a
language \\(\lang{L}\\) sparse if
\\[\\# L^{\le n} = \\#\set{x\in\set{0,1}^{\le n} : x\in \lang{L}} = n^{O(1)}\\]
and respectively, dense if
\\[\\# L^{\le n} = 2^{n^{O(1)}}.\\]

Clearly \\(\SAT{}\\) is dense. By the assumption, a trivial language like
\\(\set{1^n : n\in \NN}\\) is also NPC. But a dense language cannot be isomorphic to
a sparse languge, since the reduction function \\(\sigma\\) maps a dense language
\\(L^{n}\\) to \\(n^{O(1)}\\) length instance in a sparse language \\(L^\prime\\). But the
possible output number is polynomial in \\(n\\), while the number of preimage
instances is super-polynomial. Clearly such a \\(\sigma\\) does not exist.


### Ladner's Theorem {#ladner-s-theorem}


## Lecture 8: Limitations of Relativization {#lecture-8-limitations-of-relativization}

I think Ladner's theorem must have been proved in last lecture, but I cannot
find it anywhere on my notebook. Anyway, this lecture discusses the famous
Baker-Gill-Solovay Theorem which states that the famous \\(\P\\) vs. \\(\NP\\)
problem is not possible to prove under relativation.


### Oracle Turing Machine {#oracle-turing-machine}

Oracle Turing Machine adds the query power to Turing machine. In particular,
consider an oracle language \\(\lang{O}\\) (any language suffices), a Turing machine
is given an additional query tape and three more states \\(q\_{\text{query}}\\),
\\(q\_{\text{yes}}\\), and \\(q\_{\text{no}}\\). When machine enters query state, the next
state will be yes if the content \\(x\\) on the query tape belongs to language O,
and state no otherwise.

We proceed to define complexity classes with respect to oracle machine. Define
\\(\P^{O}\\) and \\(\NP^{O}\\) to be the set of languages that can be accepted by
(respectively nondeterministic) polynomial time oracle machine. More generally,
we can define \\(\NP^{O[k]}\\) to be the set restricting at most \\(k\\) time access
to the oracle query.

We can define \\(\NP^{\NP} := \mathop{\cup}\_{\lang{L}\in\NP} \NP^{L}\\).

Some facts on such classes:

-   \\(\overline{\SAT{}} \in \P^{\SAT{}}\\)
-   \\(\P^L = \P\\) for all \\(L\in\P\\)
-   \\(\NP^{\NP} = \NP^{3\SAT}\\)


### Cook Reduction {#cook-reduction}

A language \\(L\\) is cook-reducible to \\(L^\prime\\) if there exists a polynomial time
oracle turing machine \\(\TM^{L^\prime}\\) that decides \\(L\\). A fact is that
\\[L \le L^\prime \iff L \le \overline{L^\prime},\\]
since the query result specifically states yes or no.

The status quo of different flavors of reduction is that, in NP-problem related
proofs, Karp reduction and Cook reduction are interchanageable, but there does
not exist an equavalence proof between these two reductions.


### Lowness {#lowness}

A language \\(B\\) is **low for** \\(A\\) if \\(A = A^{B}\\). If a language is low for itself
then we call this language "closed under complement", provided it is powerful
enough to negate boolean results.

Some examples:

-   \\(\P\\) is low for itself
-   \\(\NP\\) is believed not to be low for itself
-   \\(\PSPACE\\) is low for itself
-   \\(\L\\) is low for itself
-   \\(\EXP\\) is not low for itself. This because exponential time turing machine can
    query exponentially long string, and therefore it should be in \\(2\EXP\\). Note
    that \\(\EXP = {\coEXP}\\)


### Baker-Gill-Solovay Theorem {#baker-gill-solovay-theorem}

The theorem can be stated as "there exists language \\(\lang{A}\\), \\(\lang{B}\\) such
that \\(\P^{\lang{A}} = \NP^{\lang{A}}\\) and \\(\P^{\lang{B}} \ne \NP^{\lang{B}}\\).

Proof of Baker-Gill-Solovay theorem.

Construction of language \\(A\\) is easy, just pick a language that is powerful
enough like
\\[A:=\set{\langle\alpha, x, 1^n\rangle | \TM\_\alpha(x) \text{ outputs 1 in }
2^n \text{ steps.}}\\]. It is easy to see that \\(\EXP \subset \P^A\\) and also since
an exponential time deterministic Turing machine can simulate every
non-determinstic step of a polynomial-time non-deterministic Turing machine, we
have \\(\NP^A \subseteq \EXP\\). Also so we have
\\[\EXP \subseteq \P^A \subseteq \NP^A \subseteq \EXP,\\]
which means \\(\P^A = \NP^A\\).

Construction of language \\(B\\) uses diagonalization technique. We define the
language \\(B\\) recursively. Consider a sequence of strictly increasing integers
(resp. set) \\(n\_i\\) and \\(B\_i\\). Define \\(n\_0 = 0\\) and \\(B\_0 = \phi\\), and recursively:

-   \\(n\_{i+1}\\) is larger than \\(n\_i\\) and also larger than all the strings that have
    been queried during construction of \\(B\_1\\), \\(\ldots\\), \\(B\_i\\)
-   Run \\(\TM\_i^{B\_i}(1^{n\_{i+1}})\\) in \\(2^{n\_{i+1}-1}\\) steps. If
    -   It does not halt within \\(2^{n\_{i+1}-1}\\) steps, let \\(B\_{i+1} = B\_i\\);
    -   It accepts, let \\(B\_{i+1} = B\_i\\)
    -   It rejects, let \\(B\_{i+1} = B\_{i} \cup \set{s}\\) where \\(|s| = n\_{i+1}\\) and \\(s\\)
        is not queried when execuring \\(\TM\_i^{B\_i}(1^{n\_{i+1}})\\) (this ensures
        correctness of definition).

Define \\(B = \mathop{\cup}\_{i\in\NN} B\_i\\) and the unitary language \\(U\_B :=
\set{1^n | s:|s| = n\land s\in B}\\), we then claim that \\(U\_B \in \NP^B\\) and
\\(U\_B \not\in \P^B\\).

First a NDTM can simply  guess a string \\(s\\) of input length and query the oracle
of its membership in \\(B\\), outputing whatever the oracle returns.

For a deterministic TM, suppose by contradiction \\(\TM\_i^{B}\\) computes \\(U\_B\\) in
polynomial time. Then choose \\(n\_{i+1}\\) large enough that \\(\TM\_i^{B}\\) terminates
within \\(2^{n\_{i+1}-1}\\) steps. First of all, by the construction of \\(B\setminus
B\_i\\), the only strings inside this set are longer than any query of
\\(\TM\_i^{O}(1^{n\_{i+1}})\\), and are therefore not queried by this machine, so we
have \\(\TM\_i^{B}(1^{n\_{i+1}}) = \TM\_i^{B\_i}(1^{n\_{i+1}})\\). So if

-   \\(\TM\_i^{B}(1^{n\_{i+1}}) = 1\\) \\(\implies\\) \\(\exists s\in B: |s| = n\_{i+1}\\)
    \\(\implies\\) \\(\TM\_i^{B\_i}(1^{n\_{i+1}}) = 0\\) \\(\implies\\) \\(\TM\_i^{B}(1^{n\_{i+1}}) =
      0\\)
-   \\(\TM\_i^{B}(1^{n\_{i+1}}) = 0\\) \\(\implies\\) \\(\not\exists s\in B: |s| = n\_{i+1}\\)
    \\(\implies\\) \\(\TM\_i^{B\_i}(1^{n\_{i+1}}) = 1\\) \\(\lor\\) \\(\TM\_i^{B\_i}(1^{n\_{i+1}})\\)
    does not halt within \\(2^{n\_{i+1}-1}\\) steps.

So we have \\(U\_B \not\in \P^B\\), which concludes the proof.


### Relativization {#relativization}

A proof of \\(A = B\\) or \\(A\ne B\\) relativizes if it is also a proof for \\(A^O = B^O\\)
or \\(A^O\ne B^O\\). Proofs that only uses diagonlization fall into this category.
Baker-Gill-Solovay theorem states that \\(\P\\) vs. \\(\NP\\) is not likely to have such
a simple proof.


### Space Complexity {#space-complexity}

This lecture concludes the introduction of time-complexity. The next topic is
space complexity. First space bounded computation is introduced. As usual, we
need to define complexity classes with respect to space constraint.

Let \\(S:\NN \to \NN\\) and \\(L\subseteq \set{0,1}^\*\\). We say \\(L\in
\mathsf{SPACE}(S(n))\\) if \\(\exists \TM, \forall x\in\set{0,1}^\*\\) \\(M(x) = x\in L\\)
and never uses more than \\(S(|x|)\\) blank cells on its working tapes. Similarly we
can define  \\(\mathsf{NSPACE}\\) with respect to NDTMs.


#### Configuration {#configuration}

Here we introduce the notion of configuration that consists:

-   State
-   Working tape content
-   Head position

It is clear that with these information, we can deduce the next state from the
transfer function. We here assume wlog there is a single initial configurate and
only one accept configuration.


#### Configuration Graph {#configuration-graph}

We can therefore introduce a configuration graph that has \\(2^n\\) nodes where each
node denotes a possible configuration of length \\(n\\). There is one initinal
configuration, one accepting configuration, and one rejecting configuration. Two
nodes are connected with a directed edge if one step computation transfers from
the first configuration to the second.

Notice that
\\[|Q|\times \log(S(n))^k \times S(n)^k = 2^{O(S(n))}\\]

In fact we can design a CNF \\(\phi\_{\TM, x}\\) such that \\(\phi\_{\TM,x}(C,C^\prime)
= 1\\) iff. \\(C\to C^\prime\\) is in the configuration graph of \\(\TM(x)\\). Moreover,
\\(\phi\\) should have size at most \\(O(S(n))\\).


## Pilot Lecture {#pilot-lecture}

Testing whether Prof. Fu is intelligent enough to figure out how to remotely
continue his lectures using Zoom.


### Agenda {#agenda}


#### Expander Graph and Derandomization {#expander-graph-and-derandomization}

PATH is NL complete. UPATH is in Randomized Logspace.
But we can **derandomize** this randomized algorithm to make it possible to run in
a deterministic TM. Prof. Fu plans to use two weeks to finish this. The main
techniques here are algebraic. A little combinatorics technique is still based
on algebra.


#### Interactive proof system. {#interactive-proof-system-dot}

Though might be lengthy, IP will be introduced completely. Some might be
skipped.


#### PCP theorem (very complicated) {#pcp-theorem--very-complicated}

1/3 to 2/5 of the total time will be dedicated to this part.

Two chapters of the book is dedicated to this topic which corresponds to this
part. The first chapter states the two forms of PCP theorem, but no proof. The
latter chapter states the proof. This is considered by Prof. Fu **very hard**.

PCP proof is a testament to the grasp of complexity theory.
Very related to approximate algorithm.


#### Cryptography {#cryptography}

Easy for us cryptography students, he said.
Mainly pseudorandomness, several equaivalent definitions.


### Grading {#grading}

Temporarily not settled. Most likely attendence rate, homework, and paper
reading and sharing (presentation).


## Lecture I {#lecture-i}

Expander and Derandomization
这一章是去随机化的一个例子。

Say we have a randomized algorithm, is there an equivalent determinstic algorithm?
There are relatively very **few** examples in derandomization. This Chapter's
example is rather famous.

So far our proof (of derandomization) has been relying on assumptions
extensively. Say \\(\BPP\\) vs. \\(\P\\) problem. Proving this equivalent is reduced to
other questions not easier
than \\(\P \ne \NP\\) so derandomization is generally hard.

But for specific randomized algorihtm, such derandomization is possible, i.e.
expander graph.


### Synopsis {#synopsis}

1.  Basic Linear Algebra (also fix the symbols, etc.)
2.  Random Walk
3.  Expander Graph
4.  Explicit Construction of Expander Graph
5.  Reingold's Theorem


### Basic Linear Algebra {#basic-linear-algebra}

We use column vector.

Matrix **=** Linear transformation: \\(Q^n\to Q^m\\)

1.  Linearility \\(f(u+v) = f(u) + f(v)\\), \\(f(c\cdot v) = cf(v)\\)
2.  \\(j^{th}\\) column is \\(A\cdot e\_j\\)

Two views of matrix

Dynamic View
: as a linear transform

Static View
: as a basis transform (Au = v, u is A's representation of v)

Or

Algebraically
: how to solve this
    \\[\sum\_i \vec{a\_i}\cdot x\_i = \vec{b}\\]
    good for actually solving the problem (since algebra seems more "tangible"
    than other math). Also known as the column picture.

Geometrically
: intersection of hyperplanes, intuition (also called the row picture)

Equationally
: set of equations


#### Inner product and Projection {#inner-product-and-projection}

We use \\(u^T v\\) to denote inner product. we have \\(\theta = \arccos{u^T v}\\), as a
measure of orthogonality.

We have the **very important** projection matrix \\(A (A^T A)^{-1} A^T\\). In terms of
vectors, we have v's project to u:
\\[\frac{u^T v}{\norm{u}}\cdot \frac{u}{\norm{u}}\\]


#### Orthonormal basis {#orthonormal-basis}

basis + unit length + orthrogonal

Orthogonal matrix's columns forms a orthonormal basis.


#### Cauchy-Schwatz Inequality {#cauchy-schwatz-inequality}

\\[u^T \cdot v \le \norm{u}\norm{v}\\]


#### Fix Point of Linear Transfrom -- Eigenvectors {#fix-point-of-linear-transfrom-eigenvectors}

\\[Av = \lambda v\\]
Which means linear transfrom does not change direction. If eigenvector forms a
basis, then linear transfrom is just "stretching" on each such directions.

A basic fact in linear algebra is that if eigenvalues are distinct then the
eigenvectors are linearly independent. Proof by induction.

Suppose the eigenvector are \\(v\_1\\), \\(\ldots\\), \\(v\_n\\) and eigenvalues are
\\(\lambda\_1\\), \\(\ldots\\), \\(\lambda\_n\\) respectively. If there exists \\(c\_1\\),
\\(\ldots\\), \\(c\_n\\) such that
\\[ \sum\_i c\_i v\_i = 0\\]
then we have by left multiplying \\(A\\)
\\[ \sum\_i \lambda\_i c\_i v\_i = 0\\]

Then by substracting the two equations, we have
\\[ \sum\_{i=1}^{n-1} c\_i (\lambda\_i - \lambda\_{n})v\_i = 0\\]

Inductively, we have
\\[ c\_1 \prod\_{i=1}^{n-1} (\lambda\_1 - \lambda\_i) v\_1 = 0\\]

Which means that \\(c\_1 = 0\\). And then we can conclude that \\(c\_2\\), \\(\ldots\\), \\(c\_n
= 0\\),  concluding the proof.

Let the eigenvectors form a matrix \\(S\\) then we have
\\[ AS = S\Lambda,\\] and therefore for invertivle \\(S\\) we have
\\[A = S\Lambda S^{-1}\\]

We shall sort the eigenvalues by their absolute value as \\(\lambda\_1\\), \\(\ldots\\),
\\(\lambda\_n\\) in descending order.

\\[\abs{\lambda\_1}\ge\abs{\lambda\_2}\ge\ldots\ge\abs{\lambda\_n}\\]

We call \\(\rho(A) = \abs{\lambda\_1}\\) the spectral radius. (But since in later
discussion we always have \\(\lambda\_1 = 1\\) this is not so important in this
chapter.)


#### Schur's Lemma {#schur-s-lemma}

For each matrix \\(A\\) there exists unitary matrix \\(U\\) and triangular matrix \\(T\\)
such that
\\[T = U^T A U\\]

This lemma implies spectral theorem.


#### Table of Property Juxtoposition {#table-of-property-juxtoposition}

Symmetric / Hermitian
Orthogonal / Unitary

Properties of Hermitian matrix:

-   \\(x^T A x\\) is real since \\((x^T A x)^T = x^T A^T x = x^T A x\\)
-   Eigenvalues must be real since \\(Av = \lambda v\\), \\(v^T Av = v^T \lambda v\\) so
    \\(\lambda \in\RR\\).
-   Eigenvectors of different eigenvalues are orthogonal.
    Say \\(A u = \lambda u\\) and \\(A v = \lambda^\prime v\\) and \\(\lambda \ne
      \lambda^\prime\\).

    Then

    \begin{align\*}
    v^T A u &= v^t \lambda u \\\\
    (A^Tv)^T u &= \lambda v^t u\\\\
    (\lambda^\prime u)^T u &= \lambda v^t u\\\\
    (\lambda - \lambda^\prime) (u^T v)&=0
    \end{align\*}

    By this fact Hermitian matrix with distinct eigenvalues can be diagonalized
    since
    \\[AU = U\Lambda\\]
    \\[U^{T}AU = \Lambda\\]

Spectrual Decomposition: \\(A = \sum\_i \lambda\_i u\_i u^T\_i\\)

We skip SVD because **this is not an AI course**.


#### Rayleigh Quotient {#rayleigh-quotient}

A is Hermitian and rayleigh quotient is defined as
\\[R(A,x):= \frac{x^T A x}{x^Tx} =
\frac{\sum\_i \lambda\_i\norm{u\_ix}^2}{\sum\_i \norm{u\_ix}^2}\\]
where \\(x\ne 0\\)

And therefore this can be upperbounded by \\(\lambda\_1\\) and \\(\lambda\_i\\) if \\(x\\) is
orthogonal to the subspace span by \\(u\_1\\), \\(\ldots\\), \\(u\_{i-1}\\)


#### Norm {#norm}

Norm is a map \\(\FF^n\to\RR^{\ge 0}\\) such that 3 properties are satisfied:

-   \\(\norm{v} = 0 \implies v = 0\\)
-   \\(\norm{c\cdot v} = c \cdot \norm{v}\\)
-   \\(\norm{u + v} \le \norm{u} + \norm{v}\\)

Matrix norm: the amplification ability of matrix

\\(\norm{A} = \max\_{v\ne 0} \frac{\norm{Ax}}{\norm{x}}\\)

We can use different norms in this equation / definition.


### Random Walk {#random-walk}

Reviewing of last year's lecture on random walk. From spectrum graph theory's
point of view.

Graph is the central object in combinatorics. Moreover, graph has matrix
representation. Undirected graph maps to symmetric adjecency matrix -- Neat.

We study undirected graph in this chapter. We allow self-loop and parallel edges
in undirected graph.

Reachability matrix: if \\(j\to i\\) is an edge we let \\(M\_{ij} = 1\\).

Random Walk Matrix: normalize each **column** so that they add up to \\(\mathbf 1\\).
So they model uniformly choose a neighbor at random at node \\(j\\) for column \\(j\\).
We usually use **d-normal** graph which means the number of neighbors are equal at
every vertex.

Random walk: put a pebble randomly, and then randomly walk. So the distribution
after k step random walk is
\\[ A^k \mathbf{p}\\]
where \\(\mathbf p\\) is the initial distribution.

Example: n-layer digraph, each layer has d nodes. Layer 1 is only connected to
layer 2, 2 to 3 and so on. Random walk on from one layer in this graph **does not
converge**. Special case -- n = 2 -&gt; bipartite graph.


### Introduction to Spectrual Graph Theory {#introduction-to-spectrual-graph-theory}

For a undirectional d-regular graph \\(G\\) consider its random walk matrix \\(A\\).

We have \\(A\one = \one\\) since \\(A^T = A\\), each row is a distribution.
So we acquired a trivial eigenvector,
eigenvale pair. Consider the facts:

1.  1 is an eigenvalue of A and its associated eigenvector is the stationary
    distribution vector \\(\one\\). In other words \\(A\one = \one\\).

2.  All eigenvalues have absolute values \\(\le 1\\).
    Suppose \\(v\\) is an eigenvector for \\(A\\), then let \\(v\_i\\) be the component with
    largest absolute value (this is common to the following two facts). Consider
    \\(A\_i^T v = \lambda v\_i\\). Since \\(A\_i\\) only has \\(1/d\\) and \\(0\\) component, the
    \\(\abs{A\_i^T v}\\) is bounded by \\(v\_i\\).

3.  G is disconnected if and only if 1 is an eigenvalue of multiplicity \\(\ge 2\\).
    From left to right: uniform distribution over either of the two subgraphs.

    From right to left: Consider the component \\(v\_i\\), we have any node connected
    with \\(i\\) must also have component equal to \\(v\_i\\). Then by the two
    eigenvectors begin distinct, we can prove the graph is disconnected.

4.  If G is connected, G is bipartite if and only if -1 is an eigenvalue of A.
    From left to right: all one in nodes in \\(G\_1\\) and all negative one in nodes
    in \\(G\_2\\).

    From right to left: consider \\(v\_i\\). Any node connected to \\(v\_i\\) must be
    \\(-v\_i\\), and \\(-v\_i\\) to \\(v\_i\\). The graph is connected, so our analysis can be
    applied to any node on this graph. Therefore the graph must be bipartite.


### Rate of Convergence {#rate-of-convergence}

For a regular graph \\(G\\) with random walk matrix \\(A\\), we define **rate of
convergence**

\\[\lambda\_G:= \max\_p{\frac{\norm{Ap-\one}}{\norm{p-\one}}}=
\max\_{v\perp\one}\frac{\norm{Av}}{\norm{v}},\\]
where \\(p\\) is a probability distribution.

From left to right: trivial

From right to left: \\(\alpha v + \one = p\\) where \\(p\\) is a probability
distribution and \\(\alpha\\) is small enough.

By definition \\(\norm{Av}\le \lambda\_G \norm{v}\\) for all \\(v\perp \one\\).


## Lecture II {#lecture-ii}

Rate of convergence: \\(\lambda\_G\\) the smaller, the faster random walk will
converge to uniformly random distribution.

Lemma: \\(\lambda\_G = |\lambda\_2|\\)

Define \\(\gamma\_G = 1-\lambda\_G\\) spectral expansion


### Lemma of \\(l\\) step random walk {#lemma-of-l-step-random-walk}

\\[\frac{\norm{A^l p - \one}}{\norm{p-\one}} \le \lambda\_G^l \norm{p-\one}
\le \lambda\_G^l\\]

The first inequality follows by the definition of rate of convergence. While the
second one follows from:

\begin{align\*}
\norm{p-\one}^2 &= p^Tp -2p^T\one + \one^T\one \\\\
 &\le 1 - 2/n + 1/n\\\\
 &\le 1
\end{align\*}


### Noticible Bound on Spectral Expansion {#noticible-bound-on-spectral-expansion}

IMPORTANT: technique -- make a path from u to v that relies on the bound.

Lemma: If \\(G\\) is an n-vertex, d-regular grpah with self loop at each node then
\\(\gamma\_G \ge 1/(12n^2)\\).

Proof: We only have to prove that \\(\lambda\_G^2 \le 1 - 1/(6n^2)\\).
By definition, let \\(u\\) be the normalized \\(v\_2\\) eigenvector, and \\(v = Au\\). Then
our object is equivalent to proving \\(\norm{v}^2 \le 1 - 1/(6n^2)\\)

Change the form of \\(1 - \norm{v}^2\\) a bit to get substraction terms.

\begin{align\*}
1 - \norm{v}^2 &= u^T u - 2 (Au)^T v + v^T v \\\\
&= \sum\_{i,j}(A\_{i,j} (u\_i\cdot u\_i - 2u\_i\cdot v\_j + v\_j\cdot v\_j)) \\\\
&= \sum\_{i,j}(A\_{i,j} (u\_i - v\_j)^2)
\end{align\*}

Now comes the most important technique: we break lower bound this sum term by a
**path** from some \\(i\\) to \\(j\\). First we argue for the biggest \\(u\_i\\) and smallest
\\(u\_j\\) we must have \\(u\_i - u\_j \ge 1/\sqrt{n}\\) since \\(\bf u\\) is normalized.

Consider a shortest path \\(i (i\_0)\to i\_1\to \ldots \to i\_k \to j (i\_{k+1})\\) in \\(G\\), we get
by interpolating \\(v\\) terms

\begin{align\*}
1/\sqrt{n} \le (u\_i - u\_j) &\le \sum\_{j=0}^k |u\_{i\_k} - v\_{i\_k}| + |v\_{i\_k} - u\_{i\_{k+1}}| \\\\
&\le \sqrt{\sum\_{j=0}^k |u\_{i\_k} - v\_{i\_k}|^2 + |v\_{i\_k} - u\_{i\_{k+1}}|^2} \cdot \sqrt{2D} \\\\
\end{align\*}

where \\(D\\) is the diameter of the graph. Here we use a technique of "first shift
to v then shift to the next u" technique. In this way, since all difference
terms corresponds to edges in \\(G\\), we have
\\[\sum\_{i,j}(A\_{i,j} (u\_i - v\_j)^2) \ge \frac{1}{2dDn}.\\]

By another bound on the diameter of graph: \\((d+1)D/3 \le n\\) we get \\(D \le
3n/(d+1)\\). This means \\(1 - \norm{v}^2 \ge \frac{1}{6n^2}\\), which concludes the proof.


### Algorithm from This Lemma {#algorithm-from-this-lemma}

Connectivity on graph (undirected).

Since we have shown on such **n-vertex, d-regular, self-loop** graph, \\(\gamma\_G
\ge 1/(12n^2)\\), we have now starting from any point \\(s\\), the distribution after
\\(l = 24n^2\log n\\) steps satisfies that
\\[\norm{A^l p - \one}\le (1-\frac{1}{12n^2})^{12n^2 \cdot 2\log n} \le
\frac{1}{n^2}.\\]

Then using the bound \\(\norm{x}\_{\infty} \le \norm{x}\_2\\) we get
\\[\Pr[(A^lp)\_t=1] \ge \frac{1}{n}-\frac{1}{n^2}\ge \frac{1}{2n}\\]
for big enough \\(n\\). Therefore by repeating \\(2n^2\\) times, the failure probability
is negligible (\\(1/2^n\\)).

So far we proved using this algorithm that \\(\lang{UPATH} \in \RL\\), (and
subsequently, in \\(\NL\\))
but how can we show \\(\lang{UPATH} \in \L\\) as well?


### Expander Graph {#expander-graph}

Expander graphs, defined by Pinsker in 1973, are **sparse** and well connected. They
behave **approximately** like complete graphs.

Sparsity should be understood in an asymptotic sense.

Sparsity can be defined by limiting the degree of every node.


#### Definitions {#definitions}

Well-connectedness can be characterized in a number of manners.

1.  Algebraically, expanders are graphs whose second largest eigenvalue is bounded

away from 1 by a constant.

1.  Combinatorially, expanders are highly connected. Every set of vertices of an

expander has a large boundary geometrically.

1.  Probabilistically, expanders are graphs in which a random walk converges to the

stationary distribution quickly.

Perhaps the one based on random walk serves as a starting point to understanding
this definition  the best. If random walk converges to uniform distribution is
fast, then its well-connected. This corresponds to \\(\lambda\_G\\) is small enough
according to our lemma.

Combinartorially, this means an arbitrary set of nodes have many edges connected
to outer nodes. (Inter connection is limited.)

In this chapter we prove the equivalence of the three definitions.


#### Algebraic Property {#algebraic-property}

We want to prove \\(\lambda\_G = O(1)\\). Note that the previous lemma is not good
enough.

Suppose \\(d \in\NN\\) and \\(\lambda\_G \in(0, 1)\\) are constants.

A d-regular graph G with n vertices is an \\((n, d, \lambda)\\)-graph
if \\(\lambda\_G\le \lambda\\).

\\(\set{G\_n}\_{n\in\NN}\\) is a \\((d,\lambda)\\)-expander graph family if \\(G\_n\\) is an
\\((n,d,\lambda)\\)-graph for all \\(n\in\NN\\).


#### Probabilistic Property {#probabilistic-property}

In an expander graph, random walk converges to uniform distribution in
logarithmic time.
\\[ \norm{A^{2\log\_{1/\lambda}{n}} p -\one} < \lambda^{2\log\_{1/\lambda}{n}} = 1/n^2\\]

Note that this means that after logarithmic steps, the probability that reaching
any node from any node is positive. And this means that
**the diameter of an expander graph is logarithmic**.


#### Combinatorial Property {#combinatorial-property}

Suppose \\(G = (V,E)\\) is an n-vertex, d-regular graph, and \\(S\\) be a set of
vertices no more than \\(n/2\\).

-   Let \\(\bar{S}\\) be the complement of \\(S\\)
-   Let \\(E(S,T)\\) be the subset of edges \\(i\to j\\) s.t. \\(i\in S\\), \\(j\in T\\)
-   Let \\(\partial S = E(S, \bar{S})\\)

The expansion constant \\(h\_G\\) of \\(G\\) is defined as:
\\[ h\_G = \min\_{|S|\le n/2} \frac{|\partial S|}{|S|}\\]

For constant \\(\rho > 0\\), an n-vertex, d-regular graph \\(G\\) is an
\\(n,d,\rho\\)-edge expander if \\(h\_G / d \ge \rho\\)

Perhaps \\(h\_G / d \in (0,1)\\) is a more natural definition. the bigger this value
is, the  better the graph is connected (well-connected).


## Lecture III {#lecture-iii}

Expander Graph:

-   Algebraic Property
-   Combinatorial Property
-   Prabablistic Property

We actually need a family of expander graphs. It is desireable to have their
degree uniform and spectral gap the same (a constant strictly less than 1).


### Existence of Expander {#existence-of-expander}

Theorem: Let \\(\epsilon > 0\\). There exists \\(d = d(\epsilon)\\) and \\(N\in \NN\\) such
that for every \\(n > N\\) there exists an (\\(n\\), \\(d\\), \\(1/2 - \epsilon\\))-edge
expander.

Proof of this theorem is skipped. Using Probabilistic method seems to be the way
to prove it.


### Equivalence Between Definitions {#equivalence-between-definitions}

Theorem. Let \\(G = (V, E)\\) be finite, connected, d-regular graph. Then
\\[\frac{\gamma\_{G}}{2}\le \frac{h\_{G}}{d} \le \sqrt{2\gamma\_{G}}.\\]
Very good thoerem proving the equivalence.

For sake of competence incompetence, let's reproduce the proof here.

Proof. First we prove the first inequality. Consider the set \\(S\\) that has less
than \\(n/2\\) vertices such that
\\[h\_{G} = \frac{|\partial{S}|}{|S|}.\\]

Now consider the indicator vector \\(\one\_{S}\\), we construct a vector

\begin{equation\*}
x = |\bar S| \one\_{S}  + |S| \one\_{\bar{S}}
\end{equation\*}

Notice that this vector is orthogonal to \\(v\_{1} = \one\\). This means that

\begin{align\*}
\frac{x^{T} A x}{x^{T} x} &\le \lambda\_{G} \\\\
\frac{x^{T}x - x^{T} A x}{x^{T} x} & \ge \gamma\_{G}.
\end{align\*}

Notice that

\begin{align\*}
x^{T} A x &= \frac{1}{d}(|S|^{2}\cdot E(S,S)- |S||\bar{S}| \cdot 2E(S,\bar{S})+
  |\bar{S}|^{2} \cdot E(\bar{S},\bar{S})) \\\\
 &= \frac{1}{d}(|\bar{S}|^{2}(d|S|-|\partial{S}|)-2|S||\bar{S}||\partial{S}|+
  |\bar{S}|^{2}(d|S|-|\partial{S}|)) \\\\
 &= \frac{1}{d}(d|S||\bar{S}|n - n^{2}|\partial{S}|) \\\\
 &= \frac{1}{d}(d|S||\bar{S}|n - n^{2} h\_{G} |S|)
\end{align\*}

And

\begin{align\*}
x^{T}x &= |S||\bar{S}|^{2} + |\bar{S}||S|^{2} \\\\
 &= n |S| |\bar{S}|
\end{align\*}

And therefore we have

\begin{align\*}
\gamma\_{G} &\le 1 - \frac{x^{T} A x}{x^{T} x}  \\\\
  &=  1 - \frac{n|S||\bar{S}| - \frac{h\_{G}}{d} n^{2}|S| }{n |S| |\bar{S}|} \\\\
  &= \frac{h\_{G}}{d} \frac{n}{\bar{S}} \\\\
  &\le 2 \frac{h\_{G}}{d}
\end{align\*}

Now we prove the second part: \\(\frac{h\_{G}}{d} \le \sqrt{2\gamma\_{G}}\\)

Once again, we start by considering vectors that can connect spectrum to
conbinatorial property of the graph. This time we consider the eigenvector \\(v\\)
that correspond to \\(\lambda\_{G}\\). Let \\(v = u+w\\) where \\(u\\) (resp. \\(w\\)) only has
positive (resp. negative) components of \\(v\\). Wlog we assume non-zero components
of \\(u\\) is less than \\(n/2\\) and
\\[u\_{1} \ge u\_{2} \ge \ldots \ge u\_{n/2} = u\_{n/2+1} = \ldots u\_{n}.\\]

Now consider the term
\\[\sum\_{i,j}A\_{i,j}|u\_{i}^{2} - u\_{j}^{2}|,\\]
We can use the property of \\(A\\) being symmetric and regular,
and \\(u\_{i} = 0\\) for \\(i\ge n/2\\) to
simplify the term as

\begin{align\*}
\sum\_{i,j}A\_{i,j} (u\_{i}^{2} - u\_{j}^{2})
&=\sum\_{i\le n/2}2/d\sum\_{j\in\partial{\set{i}}} (u\_{i}^{2} - u\_{j}^{2}) \\\\
&=\sum\_{i\le n/2}2/d\sum\_{j\in\partial{\set{i}}} \sum\_{k=i}^{j-1} (u\_{k}^{2} - u\_{k+1}^{2}) \\\\
&=2/d \sum\_{k=1}^{n/2} \partial{[k]} (u\_{k}^{2} - u\_{k+1}^{2}).
\end{align\*}

Now we can use the definition of \\(h\_{G}\\) to relate this term with \\(h\_{G}\\).

\begin{align\*}
\sum\_{i,j}A\_{i,j} (u\_{i}^{2} - u\_{j}^{2})
&\ge \frac{2}{d} \sum\_{k=1}^{n/2} h\_{G} k (u\_{k}^{2} - u\_{k+1}^{2})\\\\
&= \frac{2h\_{G}}{d} \norm{u}^{2}.
\end{align\*}

Using Cauchy-Schwatz Inequality, we have
\\[\sum\_{i,j}A\_{i,j}|u\_{i}+u\_{j}|^{2}\cdot
\sum\_{i,j}A\_{i,j}|u\_{i}-u\_{j}|^{2} \ge
(\sum\_{i,j}A\_{i,j}|u\_{i}^{2} - u\_{j}^{2}|)^{2}.\\]

Now lets upper bound the left hand side. First

\begin{align\*}
\sum\_{i,j} A\_{i,j} |u\_{i} - u\_{j}|^{2} &=
\sum\_{i,j} A\_{i,j} (u\_{i}^{2} - 2u\_{i}u\_{j} + u\_{j}^{2}) \\\\
&= 2\norm{u}^{2} - 2u^{T}Au.
\end{align\*}

And

\begin{align\*}
u^{T} A u &\ge u^{T} A u + u^{T} A w\\\\
&= u^{T}Av\\\\
&= u^{T}\lambda v\\\\
&= \lambda \norm{u}^{2}.
\end{align\*}

So we get

\begin{align\*}
\sum\_{i,j} A\_{i,j} |u\_{i} - u\_{j}|^{2} &\le
2(1-\lambda\_{G})\norm{u}^{2} \\\\
&= 2 \gamma\_{G} \norm{u}^{2}.
\end{align\*}

For the other part \\(\sum\_{i,j} A\_{i,j} |u\_{i} + u\_{j}|^{2} \\)
We can simply upperbound it to \\(4\norm{u}^{2}\\).

Altogether these implies

\begin{align\*}
(2 \gamma\_{G} \norm{u}^{2}) \cdot (4\norm{u}^{2})
&\ge (\frac{2h\_{G}}{d} \norm{u}^{2})^{2}\\\\
\sqrt{2\gamma\_{G}} &\ge \frac{h\_{G}}{d}.
\end{align\*}

This completes the proof.


### Convergence in Entropy {#convergence-in-entropy}

Recall the definition of Renyi entropy:
\\[H\_{\alpha}(X) := \frac{1}{1-\alpha}\log\sum\_{x}\Pr[X=x]^{\alpha}.\\]

We argue that in an expander graph, one-step random walk does not decresae
collision entropy.

The proof is rather simple, following the normal directional decomposition
formula. Consider one-step random walk from an initial distribution \\(p\\) on a
(\\(n\\), \\(d\\), \\(\lambda\\))-expander graph. Decompose \\(p\\) into
\\(p = \one + w\\) where \\(w\\) is orthogonal to \\(\one\\). Then

\begin{align\*}
\norm{Ap} &= \norm{A(\one + w)}\\\\
 &= \norm{\one} + \norm{Aw} \\\\
 &\le \norm{\one} + \norm{\lambda w} \\\\
 &\le \norm{\one} + \norm{w} \\\\
 &= \norm{p}
\end{align\*}

And that means that \\(H\_{2}(Ap) \ge H\_{2}(p)\\) meaning collision is more unlikely
after one-step random walk.


### Expander Mixing Lemma {#expander-mixing-lemma}

Very famous result. Roughly speaking, it means that in an expander graph, vertex
density can be estimated using edge density.

Let \\(G=(V,E)\\) be an (\\(n\\), \\(d\\), \\(\lambda\\))-expander graph. Let \\(S\\), \\(T\\)
\\(\subseteq\\)  \\(V\\) be two vertex sets. We have
\\[\abs{ \abs{E(S,T)} - \frac{d}{n}|S||T| } < \lambda d \sqrt{|S||T|}.\\]
In particular, it implies
\\[\abs{ \frac{\abs{E(S,T)}}{n^{2}} - \frac{|S|}{n}\frac{|T|}{n} } < \lambda.\\]

Proof. We once again uses spectral property of the graph to prove this result.
Let \\(\one\_{S}\\), \\(\one\_{T}\\) be the indicator vectors.

Consider the eigen decomposition of \\(\one\_{S}\\) (resp. \\(\one\_{T}\\)) as
\\(\sum\_{i} \alpha\_{i} v\_{i}\\) (resp. \\(\beta\_{i}\\)). We have
\\(\alpha\_{1} = \frac{|S|}{\sqrt{n}}\\) (resp. \\(\beta\_{i} = \frac{|T|}{\sqrt{n}}\\)).

Consider

\begin{align\*}
E(S,T)/d &= \one\_{S}^{T} A \one\_{T} \\\\
 &= \sum\_{i}\lambda\_{i}\alpha\_{i}\beta\_{i}\\\\
 &= \frac{|S||T|}{n} + \sum\_{i=2}\lambda\_{i}\alpha\_{i}\beta\_{i}\\\\
\end{align\*}

So we have

\begin{align\*}
E(S,T) - \frac{d}{n}|S||T| &= \sum\_{i=2}\lambda\_{i}\alpha\_{i}\beta\_{i} \\\\
|E(S,T) - \frac{d}{n}|S||T|| &\le \sum\_{i=1}\lambda |\alpha\_{i}||\beta\_{i}| \\\\
 &\le \lambda \norm{\alpha}\norm{\beta}\\\\
 &= \lambda \norm{\one\_{S}}\norm{\one\_{T}} \\\\
 &= \lambda \sqrt{|S||T|}
\end{align\*}


### Application of Expander Graph {#application-of-expander-graph}

Error reduction in randomized algorithm.

From \\(t(n)r(n)\\) to \\(r(n) + O(t(n))\approx r(n) + dt(n)\\).

The key observation is that a t-step random walk in an expander graph looks like
t  vertices sampled uniformly and independently.

Consider an (\\(2^{r(n)}\\), \\(d\\), \\(\lambda\\))-expander graph.
The **intuition** is to replace random choice on vertice with one-step random walk
on this graph.

\\(K\_{n}\\) is perfect from the viewpoint of random walk. Because one step random
walk directly yields independent uniform distribution over all vertices.

Let \\(J\_{n} = [\one,\one,\ldots,\one]\\) be the random walk matrix for \\(K\_{n}\\) with
self loops.


### Decomposition for Random Walk on Expander {#decomposition-for-random-walk-on-expander}

Lemma. Suppose G is an (\\(n\\), \\(d\\), \\(\lambda\\))-expander and
A is its random walk matrix. Then
\\(A = \gamma J\_{n} + \lambda E\\) for some E such that \\(\norm{E} \le 1\\).

Proof. Let \\(E = \frac{1}{\lambda} (A - \gamma J\_{n})\\), consider \\(v\\) be any
vector. Let \\(\alpha = \sum\_{i}v\_{i}\\), then we can decompose \\(v = \alpha \one +
w\\) where \\(w\perp \one\\).

\begin{align\*}
Ev &= E(\alpha \one + w) \\\\
 &= \frac{1}{\lambda}(A - \gamma J\_{n})(\alpha \one + w) \\\\
 &= \frac{1}{\lambda}(\alpha \one + Aw - \gamma \alpha \one) \\\\
 &= \alpha \one + \frac{1}{lambda} Aw
\end{align\*}

Observe that \\(w\\) is perpendicular to \\(\one\\), this implies

\begin{align\*}
\norm{Ev} &\le \norm{\alpha \one + \frac{1}{\lambda} \lambda w } \\\\
 &= \norm{v}
\end{align\*}

This completes the proof.


## Lecture IV {#lecture-iv}

In this lecture we continue on thoerems on expander graph and started on
explicit construction of expander graph.


### Expander Random Walk Theorem {#expander-random-walk-theorem}

\\(B\\) is a strict subset of \\([n]\\). B can be understood as a bad random number set.
This theorem states that using random walk as random source, the probability of
\\(k\\) repetition all fails has a exponentially decreasing upper bound.

Theorem. Let \\(G = (V,E)\\) be an (\\(n\\), \\(d\\), \\(\lambda\\))-expander graph, and let
\\(B\subsetneq [n]\\) be a set of vertices. Let \\(|S| = \beta n\\), \\(\beta \in (0,1)\\).
Let \\(X\_{1}\\) be a random variable denoting the uniform distribution on \\([n]\\) and
let \\(X\_{k}\\) be a random variable denoting a \\(k-1\\) step random walk from \\(X\_{1}\\).
Then

\begin{equation\*}
\\
\Pr[\mathop{\land}\_{i=1}^k X\_k\in B] \le (\lambda + \gamma \sqrt{\beta})^{k-1}.
\end{equation\*}

Proof. We use \\(B\_i\\) to denote the event that after \\(i-1\\) steps of random walk,
the result is in \\(B\\).  Define distribution vector \\(p\_i\\) as

\begin{equation\*}
\\
p\_i := \frac{BA}{\Pr[B\_i|B\_{i-1}\ldots B\_{1}]}\frac{BA}{\Pr[B\_{i-1}|B\_{i-2}\ldots B\_1]}
\ldots \frac{B\one}{\Pr[B\_1]},
\end{equation\*}

Where \\(B\\) is the diagonal matrix with \\(\beta n\\) entries. \\(p\_i\\) means the
distribution of \\(i\\) step random walks conditioned on \\(B\_1B\_2\ldots B\_i\\).

We therefore get

\begin{equation\*}
\\
\Pr[B\_1B\_2\ldots B\_k] p\_i = (BA)^{k-1} B\one
\end{equation\*}

From the relation between l1 norm and l2 norm we can get

\begin{align\*}
\\
\Pr[B\_1B\_2\ldots B\_k] &= \norm{\Pr[B\_1B\_2\ldots B\_k] p\_k}\_1 \\\\
&= \norm{(BA)^{k-1} B\one}\_1 \\\\
&\le \sqrt{n} \norm{(BA)^{k-1} B\one}.
\end{align\*}

Using the decomposition lemma from last lecture, we have \\(A = \gamma J\_n +
\lambda E\\) for some  \\(\norm{E} < 1\\). So we have

\begin{align\*}
\\
\norm{BA} &= \norm{B (\gamma J\_n + \lambda E)} \\\\
 &= \norm{\gamma B J\_n + \lambda BE} \\\\
 &\le \gamma\norm{B J\_n} + \lambda \norm{BE}.
\end{align\*}

Now consider \\(\norm{v}=1\\). Let \\(\alpha = \sum\_{i} v\_i\\), then we have \\(v =
\alpha \one + w\\) where \\(w \perp \one\\).

\begin{align\*}
\\
\norm{B J\_n v} &= \norm{B J\_n \alpha\one} \\\\
 &= \alpha \norm{B \one}\\\\
 &= \alpha \frac{\sqrt{\beta}}{\sqrt{n}} \\\\
 &\le \sqrt{\beta}
\end{align\*}

And by multiplicative property of matrix norm, we have

\begin{align\*}
\\
\norm{BE} &\le \norm{B} \norm{E} \\\\
 &\le 1
\end{align\*}

So together we get \\(\norm{BA} \le (\gamma \sqrt{\beta} + \lambda)\\). Since
\\(\norm{B\one} = \sqrt{\frac{\beta}{n}} \le \frac{1}{\sqrt{n}}\\), we get

\begin{equation\*}
\\
\Pr[B\_1B\_2\ldots B\_k] \le \frac{1}{\sqrt{n}} (\sqrt{\beta}\gamma + \lambda)^{k-1}.
\end{equation\*}

And that completes the proof.

Actually the proof can be modified a bit to facilitate better understanding of
the error reduction procedure of \\(\BPP\\). In particular, subsequent \\(B\_i\\) and
\\(B\_{i+1}\\) does not need to be adjacent. Consider the event that \\(B\_1\\),
\\(B\_3\\), \\(B\_4\\), \\(\ldots\\), \\(B\_{k+1}\\) happens. We can modify the equation by
applying two step random walk after \\(B \one\\). From the fact that \\(\norm{A}\le
1\\), we can still use the same upper bound.


### Randomness-Saving Error Reduction {#randomness-saving-error-reduction}

The above theorem almost directly corresponds to error reduction procedure for
randomized algorithms. In particular, we can save the random bits from \\(O(k\cdot
r(n))\\) to \\(O(r(n) + kO(\log d)\\), where \\(d\\) is the degree of some
appropriate expander graph and \\(k\\) is the time of repeatition.


#### RP {#rp}

Recall that a randomized TM for \\(L\in\RP\\) never error when accepting and has
error probability at most \\(1/3\\) when rejecting. So the standard error
reduction procedure is to repeat the algorithm \\(k\\) times on independent
randomness to get \\(1/3^k\\) error probability, and it takes \\(k\cdot r(n)\\) random
bits.

Using expander graph, we can do much better. Let \\(n = |x|\\) and \\(G\_n\\) be an
(\\(2^{r(n)}\\), d, \\(\lambda\\))-expander graph. Using the previous theorem, we
can first use \\(r(n)\\) random bits to sample a uniform distribution over all
vertices (whose bit-representation is every possible random choice of the TM on
\\(n\\)-bit input), and subsequently use \\(k\log(d)\\) bits to do k-step  random
walk. Let \\(B :|B|\le 1/3 2^{r(n)}\\) be the set of randomness on which \\(M\\)
fails, then the probability of all k trials fail is at most \\((\sqrt{\beta}
(1 - \lambda) + \lambda)^{k-1} \le (\frac{\gamma+1}{2})^{k-1}\\), which is also
exponentially small.


#### BPP {#bpp}

The case for \\(\BPP\\) is more tricky since the turing machine can error with at
most \\(1/3\\) probability at whatever output. The standard practice in this case
is do majority voting on repeatition results. In the stardard case when independent
randomness is used we use Chernoff bound to bound fail probability. Using
expander graph, however, we need to modify the previous theorem (in a trivial
way) to facilitate non-adjacent failure.

Consider \\(n = |x|\\) and a \\((2^{r(n)}, d, \lambda)\\)-expander graph. We can
once again do \\(k\\) step random walk on this graph using \\(r(n) + k \log(d)\\)
random bits. The catch here is this procedure fails when \\(\frac{k+1}{2}\\) trials
fail, which by inspecting the previous proof more carefully, is at most
\\((\sqrt{\beta}\gamma + \lambda)^{k+1/2}\\). We then use a union bound to include
all possible cases of failure, which is
\\(\binom{k}{k+1/2}+\binom{k}{k+3/2}+\ldots + \binom{k}{k} < 2^{k}\\), making the
failure probability at most

\begin{equation\*}
2^k \cdot (\sqrt{\beta}\gamma + \lambda)^{k/2} =
 (2 \cdot \sqrt{\sqrt{\beta}\gamma + \lambda})^k,
\end{equation\*}

which can be made exponentially small by choosing appropriate \\(\beta\\) (recall
\\(\beta\\) is tunable through stardard error reduction procedure).


### Explicit Construction of Expander Graph Family {#explicit-construction-of-expander-graph-family}

Typically we model vertices on expander graph as random choice, which makes its
number exponentially large on polynomial time machines. So the algorithm to
construct this graph may not always be efficient. We just a program that on
input the graph index, vertice node index, and its neighbor index, output the
neighbor's node index.

In particular, to quote Prof. Fu's slides:

-   In some applications expander graphs are small.
    -   An expander family \\(\set{G\_{n}}\_{n\in\NN}\\) is mildly explicit if there is
        a P-time algorithm that outputs the random walk matrix of \\(G\_n\\) whenever
        the input is \\(1^n\\).
-   In some other applications expander graphs are large.
    -   An expander family \\(\set{G\_{n}}\_{n\in\NN}\\) is strongly explicit if there
        is a P-time algorithm that on input \\(n, v, i\\) outputs the index of the
        i-th neighbor of v.


#### Graph Products {#graph-products}

We will use several graph products to explicitly construct expander graph.

<!--list-separator-->

-  Path Product

    The path product of \\(G, G^{\prime}\\) is another graph defined by
    \\(A^{\prime}A\\) where \\(A, A^{\prime}\\) are the respective random walk matrices.
    Its degree is \\(dd^{\prime}\\). Its spectral gap is at most \\(\lambda
    \lambda^{\prime}\\), and equality is achieved when the eigenvectors corresponding
    to spectral gap are parallel. In particular, we have \\(\lambda\_{G^n} =
    \lambda\_{G\_n}^n\\).

    Path product can increase graph connectivity, but at a cost of higher degree.

<!--list-separator-->

-  Tensor Product

    The tensor product of \\(G, G^{\prime}\\), denoted \\(G \otimes G^{\prime}\\) is a
    graph (\\(V\times V^{\prime}, E \times E^{\prime}\\)). In particular, it means
    that vertices in \\(G \otimes G^{\prime}\\) is (u, v) where \\(u\in V\\) and
    \\(u^{\prime} \in G^{\prime}\\), and \\((u,v) \to (w,z)\\) is an edge if \\((u,w) \in
    E\\) and \\((v,z) \in E^{\prime}\\). In terms of matrix, we can write the resulting
    graph's random walk matrix as

    \begin{equation\*}
    A\_{G\otimes G^{\prime}} =
    \begin{bmatrix}
    a\_{1,1} A^{\prime} & a\_{1,2} A^{\prime} & \ldots & a\_{1,n} A^{\prime} \\\\
    a\_{2,1} A^{\prime} & a\_{2,2} A^{\prime} & \ldots & a\_{2,n} A^{\prime} \\\\
    \vdots & \vdots & \ddots & \vdots \\\\
    a\_{n,1} A^{\prime} & a\_{n,2} A^{\prime} & \ldots & a\_{n,n} A^{\prime} \\\\
    \end{bmatrix}
    \end{equation\*}

    There are a few points to note:

    -   There is no restriction on the dimension or degree of the graph
    -   From graph's point of view, shifting order produce isomorphic graphs
    -   The resulting graph has \\(nn^{\prime}\\) nodes and \\(d d^{\prime}\\)-degree.

    Since
    \\[(A\otimes A^{\prime})\cdot (v \otimes v^{\prime}) = Av \otimes A^{\prime}
    v^{\prime}\\],
    and the eigenvectors of \\(A \otimes A^{\prime}\\) has the form \\(v\_1 \otimes
    v\_2\\) where \\(v\_1\\) (resp. \\(v\_2\\)) is the eigenvector for \\(A\\) (resp.
    \\(A^{\prime}\\)). So it follows that
    \\(\lambda\_{G\otimes G^{\prime}} =
    \max{\lambda, \lambda^{\prime}}\\).

<!--list-separator-->

-  Rotation Map

    In this type of operation, we describe the connectivity details of a random walk
    matrix \\(A\\) by a \\(nd\times nd\\) adjacency matrix. Vertice \\((u,i)\\) is connected
    to \\((v,j)\\) iff. v is u's ith neighbor and u is v's jth neighbor. This matrix
    is denoted as \\(\hat A\\).

<!--list-separator-->

-  Zig-Zag Product

    Consider two graphs \\(G\\) of \\(n\\) vertices and \\(D\\) regularity, and \\(H\\) of
    \\(D\\) vertices and \\(d\\) regularity. The zig-zag product of G and H, denoted by
    \\(G \circ H\\) is defined by

    \begin{equation\*}
    G \circ H := (I\_n \otimes B) \hat{A} (I\_n \otimes B).
    \end{equation\*}

    The intuition here is that we combine three step of walk (from the path
    product). First do a random walk on \\(H\\) (the tensor product is with a graph
    with only self-loop on which random walk does nothing), then from the vertex
    labelling in \\(H\\) in this step, we can determine an edge in \\(G\\) through the
    rotation matrix, and finally one more step on \\(H\\). Using the parallel walk
    view of tensor product might be helpful here.

    <a id="org2f4f87c"></a>

    <asset/zig-zag.eps>

    There is a lemma regarding zig-zag product.

    Lemma. \\((I\_n \otimes J\_D) \hat{A} (I\_n \otimes J\_D) = A \otimes J\_D\\)

    From the random walk intuition, left hand side corresponds to first one step
    random walk on \\(J\_D\\) and then rotation map on \\(A\\) and finally one more step
    on \\(J\_D\\). Since one step random walk on \\(J\_D\\) essentially randomly chooses a
    neighbor in \\(A\\), and any steps of random walk on \\(J\_D\\) is equivalent to one
    step random walk on \\(J\_D\\), this is equivalent to independently random walk on
    \\(A\\) and \\(J\_D\\) for one step.

    In detail, \\((I\_n \otimes J\_D) \hat{A} (I\_n \otimes J\_D)\_{(u,i),(v,j)} =
    \frac{1}{D}\frac{1}{D}\\) for \\(\hat{A}\_{(u,i),(v,j)} = 1\\) and that is the same
    with \\(A \otimes J\_D\\).


## Lecture V {#lecture-v}

Continuing on the explicit construction of expander graph. It is not until almost a week later before I finally settle down to organize these unsolicitated notes. Prof. Fu used a somewhat simpler construction in the proof of Reingold theorem. I will stick to his version in this note.


### Review on Expander Graph {#review-on-expander-graph}

Two types of explicit graphs: strongly explicit (neighbor is efficiently computable), mildly explicit (whole graph is efficiently constructable)

For a random algorithm that uses \\(r(n)\\) bits, we need a graph with \\(2^r\\) nodes.

-   \\(r = O (\log n)\\) we can compute the graph directly (explicit or mildly explicit)
-   \\(r = \omega (\log n)\\) (e.g. \\(r = \poly (n) \\)) we cannot compute the graph directly since it is too big. But for random walk, we only need to randomly choose a neighbor.
    The syntax is \\((n, v, i) \mapsto u\\) where \\(u\\) is the ith neighbor of \\(v\\) in \\(G\_n\\). In our setting, v's encoding is polynomial length, \\(i < d\\) is a constant, and n's binary representation is polynomial. So compared to the graph's size, this input is log-length.

    So the algorithm we want is **polylog** in the size of the graph, which is why this is called **strong**.


### Graph Products Review {#graph-products-review}

1.  Path Product: \\(\lambda\_{G^k} = \lambda\_G^k\\)
2.  Tensor Product: important in linear algebra and quantum computation. \\(\lambda\_{G \otimes G^{\prime} = \max(\lambda\_G, \lambda\_{G^{\prime}})}\\).
3.  Rotation Matrix: the rotation matrix \\(\hat A\\) is an adjacent matrix \\(nD \times nD\\). \\(\hat{A}\_{(v,j), (u,i)} = 1\\) iff. v is u's ith neighbor and u is v's jth neighbor.
    The good thing about rotation matrix is that this map is deterministic and invertible. This property will be useful in the construction of expander. (It enables backtracking.)
4.  Zig-Zag Product: Zig-Zag product of G and H is defined by \\((I\_n \zigz B) \hat{A} (I\_n \zigz B)\\).


### More on Zig-Zag Product {#more-on-zig-zag-product}

Lemma. \\(\lambda\_{G \zigz H} \le \lambda\_G + 2\lambda\_H\\) and \\(\gamma\_{G \zigz H} \ge \gamma\_G \gamma\_H^2\\).

Uses Decomposition lemma, triangle inequality on matrix norm and properties on the specturm of tensor product.

Proof (informal). Let \\(M\\) (resp. \\(A\\), \\(B\\)) be the random walk matrix of \\(G \zigz H\\) (resp. \\(G\\), \\(H\\)), then by definition we have \\(M = (I\_n \otimes B) \hat{A} (I\_n \otimes B)\\). Using decomposition lemma to decompose \\(B = \gamma\_H J\_D + \lambda\_H E\\) for some \\(\norm{E} < 1\\), we can expand the term into

\begin{align\*}
M &= (\gamma\_H I\_n \otimes J\_D + \lambda\_H I\_n \otimes E) \hat{A} (\gamma\_H I\_n \otimes J\_D + \lambda\_H I\_n \otimes E) \\\\
 &= \gamma\_H^2 A \otimes J\_D + \text{rest}.
\end{align\*}

We thus get \\(\lambda\_M \le \gamma\_H^2 \lambda\_G + (1 - \gamma\_H^2)\\). This implies that \\(\gamma\_{G \zigz H} \ge \gamma\_G \gamma\_H^2\\), proving the second part of the thoerem. For the first part, we further relex the inequality, to \\(\lambda\_M \le (1 - \lambda\_H)^2 \lambda\_G + 1 - (1 - \lambda\_H)^2 \le \lambda\_G + 2\lambda\_H\\), completing the proof.

Comment on Zig-Zag Product:

1.  Typically \\(D \gg d\\), \\(d\\) is the degree of the resulting expander graph. In Arora's book, it is noted that this kind of graph operation (also replacement product) is used mainly to **drastically** reduce graph degree without deteriating connectivity too much.
2.  A t-step random walk thus uses \\(t \log d\\) rather than \\(t \log D\\) random bits.
3.  If \\(\lambda\_G\\), \\(\lambda\_H\\) are too big, there is a different bound in the 2000 RVW paper.
    **O. Reingold, S. Vadhan, and A. Wigderson. Entropy Waves, the Zig-Zag Graph Product, and New Constant Degree Expanders and Extractors. FOCS, 2000.**


### Expander Construction I {#expander-construction-i}

Idea: use path product and zig-zag product to produce an expander graph family.

|        | Size | Degree | Expansion |
|--------|------|--------|-----------|
| Path   | --   | up     | UP        |
| Tensor | up   | up     | down      |
| ZigZag | up   | DOWN   | down      |

What we want is constant degree. Maybe we can use path product to get good expansion and zig-zag product to bring back degree.

Let \\(H\\) be a (\\(D^4\\), \\(D\\), \\(1/8\\))-grpah constructed by brute force (maybe proved to exist using probabilistic method, where we will find a appropriate constant \\(D\\)). Define

\begin{align\*}
G\_1 &= H^2 \\\\
G\_{k+1} &= G\_k^2 \zigz H
\end{align\*}

Fact. \\(G\_k\\) is a (\\(D^{4k}\\), \\(D^2\\), \\(1/2\\))-graph

Proof. Inductively, using previous lemmas, we get that \\(\lambda\_{G\_{k+1}} \le \frac{1}{4} + 2 \frac{1}{8} = \frac{1}{2}\\). For the base case, it follows trivially that \\(\lambda\_{H^2} < \frac{1}{2}\\).

The problem is how to interpolate between \\(D^4, D^8, \ldots\\) ? It seems there is a facile solution.

The solution is indeed very **cheesy**, if you would allow me to use such language. Notice how our construction constructed, for some constant \\(c\\), expander graphs with nodes \\(c^1, c^2, c^3, \ldots\\). So for an input \\(n^{\prime}\\), we can find such a \\(n = c^i\\) for some power \\(i\\) that \\(\frac{n}{c} < n^{\prime} < n\\). Now if we **contract** \\(k\\) \\(e\\)-large vertice sets that are disjoint, we can actually show that resulting graph will have edge-expansion factor \\(\rho\\) reduced at most to \\(\frac{\rho}{2e}\\) (a very loose bound) and degree increased to \\(d e\\) where \\(d\\) is the original regularity. This means by fixing a proper \\(e\\) we can interpolate between the graphs we caonstructed to get a bona fide expander family.

The time it takes to random walk on construction 1 is poly in graph size, so it is not strongly explicit. The space requirement is polylog, though.

To get such result, we can analyze the construction of such graph. To access a neighbor in \\(G\_k\\), one needs to perform two walks in \\(G\_{k-1}\\) and two (the slides showed one but I think in zig-zag product you need to walk two steps in \\(H\\)) walks in \\(H\\), meaning that \\(t\_k = 2 t\_{k-1} + O(1)\\). Unfolding the recursive expression, we get that \\(t\_k = 2^{O(k)} = \poly(|G\_k|\\), meaning this graph is only mildly explicit.


### Replacement Product {#replacement-product}

Consider the graph \\(G, H\\) as in zig-zag product, we define replacement product between \\(G, H\\) by

\begin{equation\*}
M = \frac{1}{2} \hat{A} + \frac{1}{2} (I\_n \otimes B).
\end{equation\*}

The intuition behind replacement product is very simple: if random walk on \\(G\\) is too expensive, we can use a smaller expander graph to generate edge label for it. So at each step of random walk in \\(G \repl H\\), with \\(1/2\\) prob. we take one step random walk in \\(H\\), or else, using the vertice label inside the \\(H\\) "cloud" as edge lebel in \\(G\\) to do a rotation map. We shall show some not-so-bad algebraic properties of spectral gap.


#### Algebraic Properties {#algebraic-properties}

Lemma. \\(\gamma\_{G \repl H} \ge \frac{\gamma\_G \gamma\_H^2}{24}\\)

Proof (informal). We use a little trick here. First notice from basic inequality \\( (1+x)^n > 1+nx\\) it suffices to prove \\(\lambda\_{(G \repl H)^3 \le 1 - \frac{\gamma\_G \gamma\_H^2}{8} }\\). This can be proved by decomposing \\(H\\), since \\(\lambda\_{(G \repl H)^3} \le \frac{\gamma\_H^2}{8} (1 - \gamma\_G) + (1 - \frac{\gamma\_H^2}{8}) = 1 = \frac{\gamma\_G \gamma\_H^2}{8}\\). Completing our proof.


### Expander Construction II {#expander-construction-ii}

There exists a strongly explicit (\\(4\\), \\(\lambda\\))-expander family for \\(\lambda<1\\).

The construction is as follows. Let \\(H\\) be a (\\((2d)^{100}\\), \\(d\\), \\(0.01\\))-expander graph, \\(G\_1\\) be a (\\((2d)^{100}\\), \\(2d\\), \\(0.5\\))-expander graph, and \\(G\_2\\) be a (\\((2d)^{200}\\), \\(2d\\), \\(0.5\\))-expander graph. We then define for \\(k > 2\\),

\begin{equation\*}
G\_k = (G\_{\ceil{\frac{k-1}{2}}} \otimes G\_{\floor{\frac{k-1}{2}}})^{50} \repl H.
\end{equation\*}

It is easy to show through induction that \\(G\_k\\) is a expander graph.

Fact. \\(G\_k\\) is a (\\((2k)^{100k}\\), \\(2d\\), \\(0.98\\))-expander graph.

Another good property is that every induction reduces the problem size by half. This means that the time to do one-step walk in \\(G\_k\\) is \\(t\_k = \poly(k) = \polylog (|G\_k|)\\). This means construction II is actually strongly explicit.

Prof. Fu commented that the "strongness" is achieved by a much much faster (double exponential in \\(\log k\\)) growth in graph size, introduced by the tensor product.


### Reingold's Theorem {#reingold-s-theorem}

Fun fact about the German language: Rain + Gold = Reingold

Theorem. \\(\lang{UPATH} \in \L\\)

What we know already is that \\(\lang{UPATH} \in \RL\\). The theorem does derandomization.

Connectivity in expander graph can be done in **logspace** since

1.  the diameter is log in its size
2.  for a regular graph, we only need to store graph label in the DFS stack, whose length is \\(O(\log n)\\). (I think backtracking can be cheesed by traversing from the starting point all over again since all history is stored in the stack).

This is the starting point of Reingold's idea.

But the input is arbitrary. We must first convert the input graph in logspace, to an expander graph. The converted graph (of which we call \\(G^{\prime}\\)) is poly-sized and therefore cannot be stored on working tape at once.

We use Construction I in Reingold's algorithm. But conversion of \\(G\\) and construction of \\(G^{\prime}\\) must be done "on-the-fly".

The algorithm must come in different versions, since I find the one during the lecture essentially used construction I, whereas in Arora's book, the algorithm used construction II. Nevertheless, the ideas should be similar. In this note, I will stick to Prof. Fu's algorithm. We start by choosing an appropriate constant \\(D\\) and find a (\\(D^4\\), \\(D\\), \\(\frac{1}{4}\\))-expander graph. We set a counter to \\(10 \log n\\) where \\(n\\) is the input length, and enumerate all random walks in \\(G\_k\\) from \\(s\_k\\) to \\(t\_k\\). \\(G\_k\\) is constructed inductively like in construction I except in the base case we let \\(G\_0\\) be the "regulated" input graph. The vertice convertion from \\(G\_{k-1}\\) to \\(G\_k\\) is done by putting arbitarty \\(i\in[D^{4}]\\) (say all zero) paddings at back, since vertices in \\(G\_k\\) has the form \\((u, i)\\) where \\(u \in G\_{k-1}\\) and \\(i \in [D^4]\\). Since \\(H\\) is connected, \\(s\\) and \\(t\\) are connected iff. \\(s\_k\\) and \\(t\_k\\) do.

The number \\(10 \log n\\) is chosen since the original spectral expansion \\(\gamma\\) is at least \\(\frac{1}{12n^2}\\). By each induction step, we can increase \\(\gamma\\) by at least \\(\frac{5}{4}\\). This means by \\(O(\log n)\\) steps, every connected component in \\(G\\) would be an expander. Up to now, we can use the connectivity algorithm for expander graph to get output. (I did not verify this number personally, but you can essentially choose a large enough constant to ensure that.)

One tricky part is to show the algorithm indeed use logspace. To do one step walk in \\(G\_k\\), we need to perform first one-step walk on \\(H\\), rotation map in \\(G\_{k-1}\\), and finally another walk in \\(H\\). Since the recursion depth in \\(O(\log n)\\), a trivial recursive algorithm uses logspace to perform a rotation map in \\(G\_{10 \log n}\\). This roughly concludes the proof. (One convinent feature about this construction is that during DFS, when backtracking is needed, we can actually derive the previous node \\(u\\) from current node \\(v\\) and the edge label \\(w\\) in the stack, since the mapping of rotation map is symmetrical.)


### On RL vs. L {#on-rl-vs-dot-l}

The problem \\(\RL = \L\\) is open, the best we know is that \\(\RL \subseteq \L^{3/2}\\). This result relies on pseudorandom generator, which sounds like a bit messy.


## Lecture VI {#lecture-vi}

Interactive Proof System. Still a lot of math involved, but we might not plunge right in as in previous chapter.

Some Zero-Knowledge related topics might not be covered in this semester, due to time limit.

Some glimpse of interactive proof.

1.  Definition of \\(\NP\\) based on certificates: certificates are proofs.
2.  OTM: Oracle's output is the proof
3.  Cook Reduction: \\(A \le B\\), where \\(B\\) is the prover
4.  PH: OTM-based definition

So computer science folks think this paradigm of prover / verifier is very useful. Interactive proof finds important application in crypto and approximation algorithms. PCP theorem's proof also uses interactive proof.

On a philosophical view: a proof is created to be (efficiently) verified.

It was not until 1985 that the idea of computation through interaction was formally studied by two groups.

-   Laszlo Babai, with a complexity theoretical motivation;
-   Shafi Goldwasser, Silvio Micali and Charles Rackoff (who later plunged into political business, missing the Turing award), with a cryptographic

Syntax:

Prover
: try to convince verifier some assertion is true.

Verifier
: **Probabilistic** turing machine, try to find the truth value of this assertion.

They communicate through dialogue.


### Synopsis {#synopsis}

MIP = NEXP might not be covered. All other topics will be covered. Note that a recent result showed that \\(\class{MIP}^{\*} = \class{RE}\\).


### Basic Principle {#basic-principle}

Verifier's job must be easy (i.e. time complexity is polynomial). Prover's power can be unbounded, but the answer must be short. Since the verifier's query also counts as one step, it cannot ask too many questions.


### Deterministic Verifier {#deterministic-verifier}

Note that one query, one answer count as two rounds. \\(\class{dIP}\\)

We say that a language \\(L\\) has a k-round deterministic proof system if there is a TM \\(V\\)
that on input \\(x, a\_1, \ldots, a\_k\\) runs in \\(poly(|x|)\\) time, and can have a \\(k |x|\\)-round
interaction with any TM \\(P\\) such that the following statements are valid

Completeness
: \\(x \in L \implies \exists P: \set{0,1}^{\*} \to \set{0,1}^{\*} \\), \\(out\_V(P,V) = 1\\),

Soundness
: \\(x \not\in L \implies \forall P: \set{0,1}^{\*} \to \set{0,1}^{\*}\\), \\(out\_V(P,V) = 0\\).

The class \\(\class{dIP}\\) captures all such languages for deterministic verifiers. Unfortunately, we have the following fact.

Fact. \\(\class{dIP} = \NP\\)

So we will only be interested in probablistic verifiers.
如果是确定性的算法，那么问的问题都是傻问题；如果投硬币，才可能问聪明的问题


### Interactive Proof with Private Coins {#interactive-proof-with-private-coins}

The STOC 1985 Paper: **The Knowledge Complexity of Interactive Proofs** has been rejected three times before finally accepted.


#### Private Coin -- an Introduction {#private-coin-an-introduction}

Marla has one red sock and one green sock.

How can he convince Arthur, who is color blind, of the fact that the socks are of different color?

Arthur writes "1" and "2" on two socks. First let Marla sees the order, and then he secretly shuffles the socks with probability \\(1/2\\). If Marla has advantage in telling whether they have been shuffled, Arthur can be convinced whether the two socks are of the same color.


#### Private Coins Model {#private-coins-model}

Verifier geneates an \\(l\\)-bits random number \\(r\sample\set{0,1}^l\\). The verifier knows \\(r\\) but the prover cannot see \\(r\\).

\begin{align\*}
a\_1 = f(x,r), &a\_3 = f(x, r, a\_1, a\_2), \ldots \\\\
a\_2 = g(x, a\_1), &a\_4 = g(x, a\_1, a\_2, a\_3), \ldots
\end{align\*}

Both the interaction and the output can be viewed as random variable over \\(r\\).


#### \\(\IP\\) --- Interactive Proofs with Private Coins {#ip-interactive-proofs-with-private-coins}

We can formulate \\(\IP[k(n)]\\) as interactive proof with \\(k(|x|)\\) rounds.

Suppose \\(k\\) is a polynomial. A language \\(L\\) is in \\(\IP[k(n)]\\) if there's a P-time PTM \\(V\\) that can have a \\(k(|x|)\\)-round interaction with any TM \\(P\\) and renders valid the following.

Completeness
: \\(x \in L \implies \exists P: \set{0,1}^{\*} \to \set{0,1}^{\*} \\), \\(\Pr\_r[out\_V(P,V) = 1] \ge 2/3\\),

Soundness
: \\(x \not\in L \implies \forall P: \set{0,1}^{\*} \to \set{0,1}^{\*}\\), \\(\Pr\_r[out\_V(P,V) = 0] \le 1/3\\).

The class \\(\IP\\) is defined by \\(\cup\_{c\ge 1} \IP[n^c]\\)

On a closer look, we may find that the prover is a \\(\BPP\\) machine, whereas the verifier can be a \\(\BPP\\) machine.

Fact. We may assume prover in the definition of \\(\IP\\) is in \\(\PSPACE\\).

The optimal prover may enumerate over

1.  The random choice of verifer
2.  Possible answers

whose total length is polynomial. It can use counting to find out which answer is optimal (in the sense that it produces the most convincing answer).

Corollary. In \\(\IP\\)'s definition, we can only consider the optimal prover.

Corollary. \\(\IP \subseteq \PSPACE\\), the converse direction will be covered later in this chapter (i.e. the celebrated **PCP** theorem).


#### Robustness of Definition {#robustness-of-definition}

Using standard repetition technique, one can reduce error probability to \\(2^{1n^s}\\). In the case of \\(\IP\\) (unbounded prover) parallel and sequential repetition are the same.

Fact. Allowing prover to use a private coin does not change \\(\IP\\), since we can find a deterministic prover from a probablistic prover.


#### Perfect Completeness {#perfect-completeness}

1.  \\(\IP\\) with perfect completeness = \\(\IP\\)
2.  \\(\IP\\) with perfect soundness = \\(\NP\\)

Proof of 1. any problem in \\(\IP\\) can be karp reduced to \\(\lang{TQBF}\\) which has a sumcheck IP protocol that has perfect completeness.

Proof of 2. We can view the random string and answers to \\(V\\) as certificate. Since soundness is perfect, this fits the definition of \\(\NP\\).


#### Graph Non-Isomorphism {#graph-non-isomorphism}

\\(\lang{GI}\\) is not known to be in \\(\P\\). The best algorithm is \\(2^{\polylog(n)}\\). \\(G\_0\\) and \\(G\_1\\) are isomorphic iff. there exists \\(\pi\\) such that \\(\pi(G\_0 = G\_1\\).

Protocol for GNI:

-   V: choose \\(r\sample\set{0,1}\\), and generate a random permutation graph \\(H\\) of \\(G\_r\\). Send \\(H\\) to \\(P\\).
-   P: identify the origin of \\(H\\) and reply with the answer.
-   V: accept iff. the answer is correct.

Completeness is perfect, soundness error is \\(1/2\\).


#### Quadratic Non-Residuosity {#quadratic-non-residuosity}

\\(\lang{QR} = \set{(a,p): \exists b, b^2 = a \pmod{p}}\\)

\\(\lang{QNR}\\) is not known to be in \\(\NP\\) or not.

Protocol for QNR:

-   V: pick \\(r < p\\) and \\(i \in \set{0,1}\\) randomly. If \\(i = 0\\) then send \\(r^2 \mod p\\) to P, else send \\(a r^2 \mod p\\) to P.
-   P: identify which is the case and answer with \\(i^{\prime}\\).
-   V: accept iff. \\(i = i^{\prime}\\).

Completeness is perfect, soundness error is \\(1/2\\).


### Summary {#summary}

One of the greatest achievements in complexity theory is that \\(\IP = \PSPACE\\).


## Lecture VII {#lecture-vii}

We continue on interactive proof system with private coins, and start working on interactive proof system with public coins.


### Interactive Proof System for Permanent {#interactive-proof-system-for-permanent}

Recall that permanent is \\(\\#\P\\)-complete.

We design an interactive proof system for perm(A) using arithmetic method

Recall the formula for permanent

\begin{equation\*}
\func{perm}(A) = \sum\_i a\_{1,i} \func{perm}(A\_{1,i})
\end{equation\*}

where \\(A\_{1,i}\\) is the \\((n-1)\times (n-1)\\) submatrix from deleting the first row and \\(i\\)th column from \\(A\\). This potentially allows us to reduce the problem of size \\(n\\) to that of size \\(n-1\\).

The idea behind this protocol is much reminiscent to the semi-honest to malicious transition in the BGW protocol (or the other direction). Notice that we can encode the matrices compactly: Using Vandermont matrix and Gaussian elimination, we can get a \\((n-1)\times (n-1)\\)-matrix of \\((n-1)\\)-degree polynomials \\(D\_A(x)\\) such that \\(D\_A(i) = A\_{1,i}\\) for \\(i \in [n]\\). The permanent for \\(D\_A\\) is a polynomial of degree at most \\(2(n-1)\\), which is very compact. The prover can send it as a proof. Though the prover can cheat by setting the target number \\(t\\) and the polynomial \\(p\\) to be such that

\begin{equation\*}
\sum\_i A\_{1,i} p(i) = t
\end{equation\*}

The number root of \\(p - \func{perm}(D\_A)\\) will be at most \\(2n - 2\\), and the verifier can choose a random number from a large enough field \\(\ZZ\_{q}\\), and then let the prover prove that \\(\func{perm}(D\_A(q)) = p(q)\\), which with high enough probability, is false. And thus we can use a union bound to show that an unfaithful prover's success probability is small even when we are reduced to the base case, where the verifier can verify himself anyway.

So by choosing the modulus \\(q \ge n^4\\), we have

\begin{equation\*}
\sum\_{i = 1}^{n-1} \frac{i^2}{q} \le \frac{n^3}{q} \le \frac{1}{n} \le \frac{1}{3}.
\end{equation\*}

And that concludes the proof system, since completeness is perfect.


### Interactive Proof System with Public Coins {#interactive-proof-system-with-public-coins}

The idea of public coin proof system is brought up fairly earily. In Papadimitriou's 1983 paper, he said
"We can formulate a decision problem under uncertainty as a new sort of game, in
which one opponent is \`disinterested' and plays at random, while the other tries to pick
a strategy which maximizes the probability of winning --- a \`game against Nature'."

His paper included a set of ATM-like defintions.

But it is Babai that formalized the concept in the way as we known of today.

Public coin can be viewed as a special case of private coin. In private coin, the problem the verifier asks is a function of the private coin. In public coin, the coin is included in the message (or considered public). What the verifier does is essentially just coin-tossing (since the prover can simulate whatever the verifier does). Only after the final round will the verifier decides accept or reject from the previous interaction.

Notions (in public coin interactive proof system):

Arther
: verifier (or nature), the one who toss coins

Merlin
: prover

According to definition, we have for polynomial \\(k : \NN \to \NN\\)

\begin{equation\*}
\AM[k(n)] \subseteq \IP[k(n)].
\end{equation\*}


### Notations {#notations}

\\(\MA\\), \\(\MA\\), \\(\class{AMA}\\), \\(\ldots\\)
But as the collapse theorem shows, it suffices to consider only \\(\AM\\) and \\(\MA\\).


### Collapse Theorem {#collapse-theorem}

If \\(k(n) \ge 2\\), we have

\begin{equation\*}
\AM[k(n) + 1] = \AM[k(n)].
\end{equation\*}

We shall prove the special case when \\(k(n)\\) is a constant.

Lemma. \\(\MA \subseteq \AM\\)

Suppose \\(L \in \MA\\). This means \\(\forall x \in L\\), \\(\exists V\\) such that

\begin{equation\*}
x \in L \iff \exists a \forall q V(x, q, a) = 1.
\end{equation\*}

(Recall that from Goldwasser-Sisper theorem, we may assume completeness is perfect). Then we can get

\begin{equation\*}
x \in L \implies \forall q \exists a V(x, q, a) = 1.
\end{equation\*}

Now we need to prove the converse direction to complete the proof. Suppose we have \\(\forall q \exists a V(x,q,a) = 1\\), recall that we may assume wlog error probability is less than \\(\frac{1}{2^n}\\). Then for \\(q \in \set{0,1}^{m}\\) and \\(a \in \set{0,1}^n\\), we have there exists an \\(a\\) such that \\(V\\) accepts with probability greater than \\(\frac{2^{m-n}}{2^m} = 2^{-n}\\), and that means \\(x\in L\\).

Or we can use the method provided on the slides, showing by relaxing by a factor \\(2^{|a|}\\) from union bound, we are still able to achieve \\(1/3\\) error probability.

So by definition, we have \\(\AM \subseteq \class{MAM} \subseteq \class{AMM} \subseteq \AM\\), indicating \\(\class{MAM} = \AM\\), and similarly \\(\AM = \class{AMA}\\).

Notice that our proof only showed that "collapsing" holds when \\(k\\) is a constant. Actually it also holds when \\(k\\) is a function of \\(n\\).

Babai and Moran showed in 1988 that \\(\AM[k(n)] = \AM[k(n)/2]\\) for \\(k(n) > 2\\).


### Perfect Completeness {#perfect-completeness}

\\(\AM\\) has perfect completeness.

Proof. Goldwasser-Sipser Theorem + Shamir Theorem.
Though they are skipped in this lecture, we will learn how to prove this result in later lectures.

Corollary. \\(\AM \subseteq \Pi\_2^p\\)

This is a natural result from the perfect completeness of \\(\AM\\). Since

\begin{align\*}
x \in L &\implies \forall q \exists a V(x,a,q) = 1 \\\\
x \not\in L &\implies \exists q \forall a V(x,a,q) = 0.
\end{align\*}

We thus have

\begin{equation\*}
x \in L \iff \forall q \exists a V(x,a,q) = 1,
\end{equation\*}

which is a \\(\Pi^p\_2\\) type definition.

Theorem. If \\(\coNP \subseteq \AM\\), then \\(\PH = \AM\\)

Proof (informal). From \\(\NP \subseteq \MA^+ = \MA\\) and the assumption \\(\coNP \subseteq \AM\\), we get \\(\PH \subseteq \AM\\) by induction.

As for the details, I think I have come up with two different (but similar) routes to this thoerem.

Proof 1. Consider a \\(\Sigma\_2\SAT\\) formula \\(\Psi\\) such that

\begin{equation\*}
\Psi \iff \exists u\_1 \forall u\_2 \phi(u\_1, u\_2).
\end{equation\*}

From the assumption \\(\coNP \subseteq \AM\\) we have the \\(\coNP\\) formula \\(g(u\_1) = \forall u\_2 \phi(u\_1, u\_2)\\) is equivalent to \\(\Pr\_q [\exists a, V(g(u\_1), q, a) = 1] \ge \frac{2}{3}\\). Then using error reduction and union bound, we have \\(\Pr\_q [\exists u\_1, a, V(g(u\_1), q, a) = 1] \ge \frac{2}{3}\\), which implies that \\(\Sigma\_2 \subseteq \AM\\). Similar to \\(\BPP\\), \\(\AM\\) is closed under complement, and that implies that \\(\Pi\_2 \subseteq \AM\\), which further implies \\(\Pi\_2 = \Sigma\_2 = \AM\\). The theorem thus follows.

Proof 2. We use induction in this proof. Assuming \\(\Sigma\_i \subseteq \AM\\), we show that \\(\Sigma\_{i+1} \subseteq \AM\\).

Consider the OTM-based defintion: \\(\Sigma\_{i+1} = \NP^{\Sigma\_i \SAT}\\). From the induction assumption, we can replace every oracle call by a two round interaction with some prover. We may also let the prover send at the very beginning a certificate, so that the verifier accepts iff. N accepts. So \\(\Sigma\_{i+1} \in \AM\\).

As for the base case, consider in the previous proof we showed that \\(\Sigma\_2 \subseteq \AM\\). This concludes the proof.

Corollary. If \\(\lang{GI}\\) is \\(\NP\\)-complete, then \\(\PH = \AM\\).

Proof (informal). If \\(\lang{GI}\\) is \\(\NP\\)-complete, then \\(\lang{GNI}\\) is \\(\coNP\\)-complete. We will show that \\(\lang{GNI}\in\AM\\), hence \\(\coNP \subseteq \AM\\). Together with the previous theorem, this means the polynomial hierarchy collapses to \\(\AM\\).

From \\(\NP \subseteq \MA \subseteq \AM\\) we can interpret as \\(\AM\\) and \\(\MA\\) are randomized analogues of \\(\NP\\).

-   In \\(\AM\\) the randomness is announced first
-   In \\(\MA\\) the randomness comes afterwards


### Set Lower Bound Protocol {#set-lower-bound-protocol}

In this section we show that for a set \\(S\\) that

1.  membership can be efficiently certified
2.  size is either \\(\ge K\\) or \\(\le \frac{K}{2}\\) for some constant \\(K\\)

we can construct a public-coin proof system that accepts when set is big and rejects with good possibility when set is small. The system uses pairwise independent hash function and the probabilistic method as techniques.


#### Pairwise Independent Hash Function {#pairwise-independent-hash-function}

Let \\(H\_{n,k}\\) be a collection of hash functions from \\(\set{0,1}^n\\) to \\(\set{0,1}^k\\). We call this collection pairwise independent if

-   For each \\(x \in \set{0,1}^n\\) and each \\(y \in \set{0,1}^k\\),

\begin{equation\*}
\Pr\_{h\sample H\_{n,k}}[h(x) = y] = \frac{1}{2^k}
\end{equation\*}

-   For all \\(x, x^{\prime}\\) with \\(x \ne x^{\prime}\\) and for all \\(y, y^{\prime}\\),

\begin{equation\*}
\Pr\_{h\sample H\_{n,k}}[h(x) = y \land h(x^{\prime}) = y^{\prime}] = \frac{1}{2^{2k}}.
\end{equation\*}


#### Efficient Construction of Hash Function {#efficient-construction-of-hash-function}

We can use finite-field operation to cut down output length.

In particular, we can constuct PIHF \\(H\_{n,n}\\) from \\(GF(2^n)\\) by simply picking two field elements and letting \\(h\_{a,b} = ax + b\\). If what we want is \\(H\_{n,k}\\) with \\(n > k\\), we can cut the output by \\(n-k\\) bits; otherwise, we start with \\(H\_{k, k}\\) and pad zeros to the input. It is trivial to show that the pairwise independence property still holds.


#### Application of PIHF {#application-of-pihf}

1.  Sipser used these functions to prove \\(\BPP \in \Pi\_4 \cap \Sigma\_4\\). (Although I recall that we can actually prover \\(\BPP \in \Pi\_2 \cap \Sigma\_2\\) using this method.)
2.  Stockmeyer applied them to set lower bound for the first time.
3.  Babai exploited them in the study of Arthur-Merlin protocol.


#### Set Lower Bound Protocol {#set-lower-bound-protocol}

Suppose \\(S\\) is a set whose membership can be certified. The certificate is checked by the verifier.

The set lower bound protocol is a public bound protocol. For a set \\(S\\) and a constant \\(K\\). If

-   \\(|S| \ge K\\), verifier will accept with high probability,
-   \\(|S| \le \frac{K}{2}\\), verifier will reject with high probability.


#### Motivation {#motivation}

Assuming \\(S\subseteq \set{0,1}^m\\), \\(2^{k-2} \le K \le 2^{k-1}\\), we argue that for a set of \\(\kappa = O(k)\\) hash functions, the mapped space \\(h\_1(S) \cup \ldots h\_{\kappa}(S)\\) is able to cover the whole space \\(\set{0,1}^k\\) if \\(|S| \ge K\\).

Consider any \\(y \in \set{0,1}^k\\), we have \\(\Pr\_h[h(x) = y] = \frac{1}{2^k}\\). So

\begin{equation\*}
\Pr\_h[y \in h(S)] \ge \sum\_{x\in S} \Pr\_h[y = h(x)] - \sum\_{x, x^{\prime} \in S} \Pr[y = h(x) \land y = h(x^{\prime})] \ge \frac{K}{2^k} - \frac{K^2}{2^{2k}} \ge \frac{1}{10}.
\end{equation\*}

So by setting \\(\kappa > \frac{k}{\log(10/9)}\\) we can get that

\begin{equation\*}
\Pr\_{h\_1,\ldots,h\_{\kappa}}[\exists y y\not\in h\_1(S) \cup h\_2(S) \cup \ldots \cup h\_{\kappa}(S)] < 1.
\end{equation\*}

And that means there exists a set of hash functions such that the whole space is covered.

On the other hand, if \\(|S| \le \frac{K}{2\kappa}\\), then

\begin{equation\*}
\sum\_{i=1}^{\kappa} |h\_i(S)| \le 2^{k-2}.
\end{equation\*}


#### The Protocol {#the-protocol}

We first transform the problem into \\(S^l \ge K^l\\) or \\(S^l \le \frac{K^l}{2^l}\\) for some proper \\(l = O(\log k)\\) to fit the previous result, and then

1.  Merlin first sends a group of hash functions \\(h\_1\\), \\(h\_2\\), \\(\ldots\\), \\(h\_{\kappa}\\) to Arthur
2.  Arthur randomly picks \\(y \sample \set{0,1}^k\\) and sends to Merlin
3.  Merlin sends back (\\(i\\), \\(x\\), \\(\pi\\)) such that \\(h\_i(x) = y\\) and \\(\pi\\) proves \\(x\in S\\).

After that, Arthur accepts iff. the test passes.


#### Proof of \\(\lang{GNI} \in \AM\\) {#proof-of-lang-gni-in-am}

Observe that the set \\(\set{(H, \pi)}\\) where \\(H\\) is isomorphic to \\(G\_0\\) or \\(G\_1\\) is a membership-verifiable set. Then we can apply the previous set lower bound protocol to show \\(\lang{GNI} \in \AM\\).


### Boppana-Hastad-Zachos Theorem {#boppana-hastad-zachos-theorem}

Thoerem. If \\(\lang{GI}\\) is \\(\NP\\)-complete, then \\(\Sigma\_2 = \Pi\_2\\).

Proof. We can use the previous theorem, since \\(\lang{GI}\\) is \\(\NP\\)-complete implies that \\(\lang{GNI}\\) is \\(\coNP\\)-complete, and thus \\(\coNP \subseteq \AM\\).


## Lecture VIII {#lecture-viii}

We discuss public coin versus private coin in this lecture. It is possible that \\(\IP\\) and \\(\AM\\) are not so different. Id est, random questions are good questions.


### Goldwasser-Sipser Theorem {#goldwasser-sipser-theorem}

Thoerem. \\(\IP[k(n) \subseteq \AM[k(n) + 2]\\)

This implies for constant round protocol, private coin is essentially public coin.

The proof is somewhat complicated. But its kernel is set lower bound protocol. We thus skip this proof.

Together with Babai theorem, we have for all constant round interaction proof is included in \\(\AM\\).


### Public-Coin versus Private-Coin {#public-coin-versus-private-coin}

We shall see from \\(\IP =\PSPACE\\) that \\(\AM = \IP\\) is unlikely.


### Programme Checking {#programme-checking}

Checking a program is not testing or verification. Checking is to check what is the probability that the program is correct for some input.

To quote words from Blum and Kannan: "Checking is concerned with the simpler task of verifying that a given program returns a correct answer on a given input rather than on all inputs. Checking is not as good as verification, but it is easier to do. It is important to note that unlike testing and verification, checking is done each time a program is run."

As Prof. Fu mentioned, in this lecture and the same lecture last year, as interesting as program checking sounds, it is somewhat not favoured in the complexity literature, and existing papers on this subject is not too abundant. It is nevertheless a good exercise to show how can we use interactive proof.


#### Definition of Programme Checking {#definition-of-programme-checking}

A checker for a task T is a P-time probabilistic OTM C that, given a claimed program P for T and an input x, the following statements are valid:

-   If \\(\forall y, P(y) = T(y)\\), then \\(\Pr[C^P(x) \text{ accepts } P(x)] \ge \frac{2}{3}\\).
-   If \\(P(x) \ne T(x)\\), then \\(\Pr[C^P(x) \text{ rejects } P(x)] < \frac{1}{3}\\).

The checker C may apply P to a number of randomly chosen inputs before making a decision. So even if \\(P(x) = T(x)\\), the checker may still reject \\(P(x)\\).


#### Checker for Graph Non-Isomorphism {#checker-for-graph-non-isomorphism}

If \\(P(G\_0, G\_1)\\) is a program for \\(\lang{GNI}\\) such that if \\(G\_0 \not\cong G\_1\\) it returns "yes", and otherwise it returns "no", we can design a checker for this program in the following manner.

On input \\(G\_0, G\_1\\), our checker \\(C^P\\) works as follows:

1.  Query \\(P(G\_0, G\_1\\)
2.  If it returns "yes", then ask \\(\P\\) to provide a \\(\AM\\) proof that prove such statement.
3.  If it returns "no", we verify its answer in this way. Choose a vertex \\(v\_1^0 \in G\_0\\) and \\(v\_1^1 \in G\_1\\), and replace \\(v\_1^0\\) and \\(v\_1^1\\) with \\(K\_{n+1}\\) at each two graphs. Then checker then query \\(P\\) on the replaced, \\(2n\\) vertice graphs. If the answer is "no", then delete \\(v\_1^0\\) and \\(v\_1^1\\) and repeat this process to find the next mapping in the reduced graph. If the answer is "yes", then try again on \\(v\_2^1\\), \\(v\_3^1\\), and so on, until the permutation is found. Otherwise, \\(P\\) rejects.

It is clear that completeness is perfect, and from the soundness of \\(\lang{GNI}\\)'s AM proof, the error probability can be made \\(2^{-k}\\) by \\(k\\)-time repetition.

At this point, the slide page 80 points out that "if \\(L\\) has an interactive proof system where the prover can be efficiently implemented using \\(L\\) as an oracle, then \\(L\\) has a checker." If the query result is \\(x\in L\\), then we can ask the program to prove this statement. However, in the converse case, i.e. \\(x \not\in L\\), I have absolute no idea how to ensure 'soundness'. Maybe this slide is skipped for the complexity of its proof.

There is a theorem that states \\(\lang{GI}\\), \\(\\#\SAT\_D\\), and \\(\lang{TQBF}\\) have checkers.


#### Checker for Linear Function {#checker-for-linear-function}

Linear function has the nice property that the problem on any input \\(x\\) can be reduced to solving the problem on a sequence of random inputs. We call this property **random self-reducibility**.


#### Lipton Theorem {#lipton-theorem}

Theorem. There is a randomized algorithm that, given an oracle that computes the permanent on \\(1 - \frac{1}{3n}\\) fraction of the \\(n \times n\\) matrices on \\(GF(p)\\), can compute the permanents of all matrices on \\(GF(p)\\) correctly with high probability.

The idea is once again reduce the problem on one instance to that on other instances. Let

\begin{equation\*}
B(x) = A + xR
\end{equation\*}

where \\(R\\) is a random matrix. When \\(x \ne 0\\) the matrix \\(B\\) is uniformly random, so we can actually query the oracle on \\(n+1\\) distinct, non-zero field elements, to get \\(n+1\\) evaluations, and finally by interpolation, get the evaluation on \\(x = 0\\). The key observation (somewhat reminiscent to arithmetization method) is that the permanent of \\(B(x)\\) is a \\(n\\)-degree polynomial.

Using union bound, we get the error probability is at most \\(\frac{1}{3}\\), which is already good enough.

At last, the slide claim that Lipton's algorithm implies a checker for the permanent problem. I have confused myself here a bit. In previous examples, we have used interactive proof system where checker acts as verifier (Arthur) and program acts like prover (Merlin). Permanent has an Interactive Proof system, why bother to use a checker algorithm when we can just ask the program to provide a proof?


### \\(\IP = \PSPACE\\) {#ip-pspace}

In this chapter, we state and prove the celebrated result \\(\IP = \PSPACE\\). Notice that from \\(\IP \subseteq \PSPACE\\) and \\(\lang{TQBF}\\) being a \\(\PSPACE\\)-complete problem, all we have to prove is that \\(\lang{TQBF}\\) has an interactive proof system.

We start by showing a slightly weaker version, namely, \\(\\#\bar{\SAT}\_D \in \IP\\).


#### Arithmetization {#arithmetization}

We can "upscale" a Boolean formula using arithmetization. Namely, for a 3CNF formula \\(\phi = \phi\_1 \land \phi\_2 \land \ldots \land \phi\_m\\) with \\(n\\) literals, we can use the following law to convert this formula into a \\(n\\)-variate, at most \\(3m\\)-degree polynomial over \\(GF(q)\\) by recursively apply the following laws:

-   \\(x\_i \to X\_i\\)
-   \\(\neg \phi \to 1 - \Phi\\)
-   \\(\phi\_1 \land \phi\_2 \to \Phi\_1 \cdot \Phi\_2\\)

Using De-Morgan's law we can also handel disjunction. The transformation above satisfies that

\begin{equation\*}
\Phi(b\_1, b\_2, \ldots, b\_n) = \phi(b\_1, b\_2, \ldots, b\_n).
\end{equation\*}

And therefore for the counting property, it holds that

\begin{equation\*}
\sum\_{b\_1 = 0}^1\sum\_{b\_2 = 0}^1 \ldots \sum\_{b\_n = 0}^1 \Phi(b\_1, b\_2, \ldots, b\_n) = \sum\_{b\_1 = 0}^1\sum\_{b\_2 = 0}^1 \ldots \sum\_{b\_n = 0}^1 \phi(b\_1, b\_2, \ldots, b\_n).
\end{equation\*}

Let \\(p\_{\phi}(X\_1, X\_2, \ldots, X\_n) = \prod\_{j=1}^m p\_{\phi\_j}(X\_1, X\_2, \ldots, X\_n)\\) be the arithmetization of \\(\phi\\). Although the transformation can be done in polynomial time, opening up the brackets would take exponential time (since the expression size is exponential).


#### Sumcheck Protocol {#sumcheck-protocol}

Suppose \\(g(X\_1, X\_2, \ldots, X\_n)\\) is an \\(d\\)-degree polynomial, \\(K\\) is an integer. We want to prove that

\begin{equation\*}
\sum\_{X\_1 = 0}^1 \sum\_{X\_2 = 0}^1 \ldots \sum\_{X\_n = 0}^1 g(X\_1, X\_2, \ldots, X\_n) = K.
\end{equation\*}

We do so by using the permanent proof like methods. The prover can send to the verifier a polynomial \\(h(X\_1)\\) that is supposed to be \\(\sum\_{X\_2 = 0}^1 \ldots \sum\_{X\_n = 0}^1 g(X\_1, X\_2, \ldots, X\_n)\\). Notice that \\(h(x\_{1})\\) is compact. After this, the verifier

-   aborts if \\(h(0) + h(1) \ne K\\)
-   picks a random field element \\(q\\) and asks the prover to prove

\begin{equation\*}
\sum\_{X\_2 = 0}^1 \ldots \sum\_{X\_n = 0}^1 g(q, X\_2, \ldots, X\_n) = h(q).
\end{equation\*}

In the base case when \\(n = 1\\), the prover simply computes \\(g(0) + g(1)\\), compares it to \\(K\\) and set the result accordingly.

Fact. The above protocol has

1.  perfect completeness,
2.  Soundness error \\(\le 1 - (1 - \frac{d}{p})^d\\).

The completeness is straightforward. For soundness, observe that in the base case, the prover has perfect soundness. For \\(n\\)-variable formula, consider the case when \\(K\ne\sum\_{X\_1, X\_2, \ldots, X\_n g(X\_1, X\_2, \ldots, X\_n)}\\). The verifier will

-   always reject if \\(h(X)\\) is correct
-   choose a \\(q\\) that satisfies \\(h(q) \ne \sum\_{X\_2,\ldots,X\_n}g(q, X\_2, \ldots, X\_n)\\) since there are at most \\(d\\) roots of \\(h(q) - \sum\_{X\_2,\ldots,X\_n}g(q, X\_2, \ldots, X\_n)\\).
-   from the induction assumption, the probability that verifier rejects is greater than \\((1 - \frac{d}{q}) (1 - \frac{d}{q})^{n-1} = (1- \frac{d}{q})^n\\).

Using sumcheck protocol, we can prove \\(\\#\SAT\_D \in \IP\\).


#### Arithmetization for \\(\lang{TQBF}\\) {#arithmetization-for-lang-tqbf}

Recall our goal is to prove \\(\TQBF \in \IP\\). So it is natural to consider how to extend the sumcheck protocol to quantified formulas. One possible way is to replace every existential quantifiers with summation and every forall quantifiers with multipliation. The obvious problem here is that with multiplication, the degree will grow exponentially fast. When the degree is too high, sumcheck will not work.

Fortunately, we have a linearization technique.


## Lecture IV {#lecture-iv}

We start by picking up the leftovers in the Interactive proof chapter, then start with PCP theorem chapter. I actually find in this lecture that in an interactive proof system, the prover's ability can be **unbounded**, although \\(\PSPACE\\) would suffice. That is, in the definition of \\(\IP\\), there is no restriction on prover's ability, meaning they can be non-uniform or unbounded.


### Interactive Proof System {#interactive-proof-system}

Arithmetization: from boolean formula to arithmetic formula. The variables at value \\(\set{0,1}\\) is the same. The advantage of such method is bigger field for better verificaiton process.

The sumcheck protocol for \\(\class{TQBF}\\) is actually a modification over the simplified interactive interactive proof system for \\(\\#\SAT\_D\\). The improvement here is that since there are existential and universal quantifiers, we need some tools to bring down the arithmetic polynomial degree. The idea is to use **linearization**. Since we are only interested in the truth value of the \\(\class{TQBF}\\) formula \\(\psi\\), we can limit the equality to \\(0, 1\\). This allows us to use the following arithmetization operators:

-   \\(\exists\_{x\_i}  p \to 1 - (1 - p\_0)(1 - p\_1)\\)
-   \\(\forall\_{x\_i} p \to p\_0 p\_1\\)
-   \\(L\_{x\_i} p \to x\_i p\_1 + (1 - x\_i) p\_0\\)

Together with usual tools for converting \\(x\_1 \land x\_2\\) to \\(X\_1 \cdot X\_2\\) and \\(\neg x\_1\\) to \\(1 - X\_1\\), we can maintain the following invariant (very informal):

-   After existential or universal operator, the formula is true iff. the polynomial equals to one
-   After linearization operation, the new polynomial is equal to the previous polynomial on \\(0,1\\).

So the prover and verifier both convert the formula

\begin{equation\*}
\psi = \exists x\_1 \forall x\_2 \exists \ldots \exists x\_n \phi(x\_1, x\_2, \ldots, x\_n)
\end{equation\*}

to formula  over some finite field \\(\FF\\):

\begin{align\*}
p\_{\psi} = &\exists\_{X\_1}L\_{X\_1} \\\\
 & \forall\_{X\_2} L\_{X\_1} L\_{X\_2} \\\\
 & \vdots \\\\
 & \forall\_{X\_{n-1}} L\_{X\_1} L\_{X\_2} \ldots L\_{X\_{n-1}} \\\\
 & \exists\_{X\_n} L\_{X\_1} L\_{X\_2} \ldots L\_{X\_n} \\\\
 & p\_{\phi}(X\_1,X\_2,\ldots, X\_n).
\end{align\*}

The prover and verifier proceeds in \\(n^2\\) rounds. In the first round, the prover sends a polynomial \\(s\_1(X\_1)\\) to the verifier, who then verifies that \\(1 - (1 - s(0))(1 - s(1)) = 1\\), and rejects otherwise. Then the verifier samples \\(r\_1 \sample \FF\\) and asks the prover to prove the linearization operation is performed correctly.

This is done by letting the prover to send another polynomial \\(s\_2(X\_1)\\) that is meant to be the "openup" of the expression from right to left, up to \\(\forall\_{X\_2}\\). Perhaps this process is better understood when interpreting the operations as operators. The prover sends another polynomial that is \\(p\_{\phi}\\) processed up to the \\(\forall\_{X\_2}\\) operator, which will now be a univariate polynomial of degree at most \\(d\\). The verifier then verifies that \\(r\_1\cdot s\_2(1) + (1 - r\_1) \cdot s\_2(0) = s\_1(r\_1)\\). After this, the verifier chooses \\(r\_3\sample \FF\\).

Notice that in order to prove the operator \\(\forall\_{X\_2}\\) is computed correctly, the "preimage" polynomial is now a bivariate polynomial (in \\(X\_1\\) and \\(X\_2\\)). But this is not a problem, since what we want to prove is that  this process produces a polynomial in \\(X\_1\\) that evaluates to \\(s\_2(r\_3\\) when \\(X\_1 = r\_3\\). So the verifier sends to the prover the polynomial **partially** assigned with \\(X\_1 = r\_3\\). The prover then verifies the polynomial \\(s\_3\\) satisfies that \\(s\_3(0)\cdot s\_3(1) = s\_2(r\_3\\). If this is indeed the case, the prover proceeds to sample \\(r\_4 \sample \FF\\) and asks the prover to prove operator \\(L\_{X\_1}\\) is computed correctly. Note that this step will incur a new assignment to \\(X\_1\\).

So The process proceeds inductively as such. In the final step, the prover can verify that without any operators, the polynomial-sized polynomial evaluates indeed to the target value defined by previous interactions. In this step, the verifier has perfect soundness and completeness.

Completeness is perfect. For soundness, using a union bound on the event that in some interaction step, the verifier chooses a random field element such that the false polynomial equals to the true polynomial, we conclude that soundness error is at most \\(\frac{O(n^2 d)}{q}\\). Thus by setting \\(q\\) large enough, we can get small soundness error.


### PCP Theorem {#pcp-theorem}

[PCP Theorem is] the most important result in complexity theory since Cook's Theorem.


#### Proof Approaches {#proof-approaches}

There are mainly two proofs of PCP theorem.

1.  1992 Algebraic approach
2.  2006 Combinatorial approach (also the one this book)


#### Views {#views}

Two ways to view PCP theorem:

-   It is a result about locally testable proof systems. Thus further specifying interactive proof.
-   It is a result about hardness of approximation.


#### Synopsis {#synopsis}

1.  Approximation Algorithm
2.  Two Views of PCP Theorem
3.  Equivalence of the Two Views
4.  Inapproximability
5.  Efficient Conversion of NP Certificate to PCP Proof
6.  Proof of PCP Theorem
7.  Historical Remark


### Approximation Algorithms {#approximation-algorithms}

Ever since the discovery of PCP theorem, there has been a surge in the proof of inapproxibility of optimization algorithms.

We can characterize the performance of approximation algorithm in the following way. Suppose \\(A\\) is an approximation algorithm for a maximum function \\(f\\), then we \\(A\\) is a \\(\rho\\)-apprximation (\\(\rho:\NN \to (0,1)\\)) for \\(f\\) if it satisfies for all \\(x\\),

\begin{equation\*}
\frac{A(x)}{f(x)} \le \rho(|x|).
\end{equation\*}

Similarly, we can define \\(\rho\\)-approximation for a minimum function \\(g\\) as

\begin{equation\*}
\frac{g(x)}{A(x)} \le \rho(|x|).
\end{equation\*}

There are some classifications of problems with respect to the approximation feasibility.


#### Fully Polynomial Time Approxmiation Scheme (FPTAS) {#fully-polynomial-time-approxmiation-scheme--fptas}

A good example is the subset-sum problem. There is a dynamic programming algorithm that runs in exponential time, but for any \\(\epsilon\\), we have an \\((1 - \epsilon)\\)-approximation algorithm that runs in \\(O((1 - \frac{1}{\epsilon}) \cdot n^2)\\) time. It is called "fully" approximatable probably because the inverse of approximation factor only appears as a multiplicative factor.


#### Polynomial Time Approximation Scheme (PTAS) {#polynomial-time-approximation-scheme--ptas}

Knapsack problem has a similar dynamic programming algorithm (although not good enough). For any \\(\epsilon\\), one can design a \\((1 - \epsilon)\\)-approximation scheme that runs in time \\(O((1 - \frac{1}{\epsilon}) n^{\frac{1}{\epsilon}}\\).

We say that KnapSack has a PTAS.


#### Max-3SAT {#max-3sat}

A simple algorithm for Max-3SAT can achieve \\(\frac{1}{2}\\) approximation factor. Simply choose every variable assignment that has better satisfying clauses in each step. We will get in the end at least half of all the satisfying clauses. So a greedy algorithm achieves approximation factor \\(\frac{1}{2}\\). We say that \\(\lang{Max-3SAT} \in \class{APX}\\).

There is some definition that \\( \class{FPTAS} \subseteq \class{PTAS} \subseteq \class{APX} \subseteq \class{OPT} \\). And under assumption that \\(\P\ne\NP\\) the containments are strict.


#### Max-IS and Min-VC {#max-is-and-min-vc}

By definition, in a \\(m\\) vertex graph, \\(\lang{Min-VC}\\) + \\(\lang{Max-IS}\\) = m.

A simple approximation algorithm for \\(lang{Min-VC}\\) is to pick a remaining edge, include its two vertices, and extend to cover all adjacent edges, and repeat. Its apprxomiation factor is \\(\frac{1}{2}\\).

We will see evidence that refutes the following questions

-   Is \\(\lang{Min-VC}\\) in \\(\class{PTAS}\\)?
-   Is \\(\lang{Max-IS}\\) in \\(\class{APX}\\)?


### Two Views {#two-views}

\\(\class{MIP} = \class{NEXP}\\) can be viewed as "nondeterminism can be
traded with interaction and randomness".

Suppose \\(L \in \NP\\) and \\(x\\) is an input string. The prover
provides a proof of polynomial length, the verifier simply samples a
random location and then asks the value on that location.

In PCP's language, restict query syntax and randomness resources. More
specifically, for a language \\(L\\) and \\(q, r : \NN \to \NN\\), we say
that \\(L\\) has an (\\(q(n)\\), \\(r(n)\\))-PCP verifier if a \\(\P\\)-time
verifier \\(V\\) exists such that

Efficiency
: The verifier is given access to a proof \\(\pi\\) of
    length \\(\le q(n) 2^{r(n)}\\), may toss at most \\(r(n)\\) coins and
    make at most \\(q(n)\\) non-adaptive queries. Altogether, it runs in
    polynomial time.

Completeness
: If \\(x\in L\\), then \\(\exists \pi:, \Pr\_r[V^{\pi}(x)
      = 1] = 1\\).

Soundness
: If \\(x \not\in L\\), then \\(\forall \pi,
      \Pr\_r[V^{\pi}(x) = 1] \le \frac{1}{2}\\).

In this definition, there are several points to note.

1.  It suffices to consider proof length \\(\le q 2^r\\).

    This is simply due to at most this much locations may be queried.

2.  \\(\class{PCP}(q, r) \subseteq \class{NTIME}(q 2^{O( r)})\\)

    This is due to we can first guess a proof and then simulate the interaction by counting all accepting \\(r\\)'s and make a choice from counting results.

There are some results, some are trivial, some are not so trivial and will be proved in this chapter

-   \\(\PCP(0, \log) = \P\\)
-   \\(\PCP(0, \poly) = \NP\\)
-   \\(\PCP(\log, \poly) = \NP\\)
-   \\(\PCP(\poly, \poly) = \NEXP\\)
-   \\(\PCP(\log, \log) = \NP\\)
-   \\(\PCP(\log, \log) = \NP\\)


### The PCP Theorem {#the-pcp-theorem}

When people say **the PCP theorem**, they are refering to \\(\PCP(\log, 1) = \NP\\).

In order to make us familiar with the syntax of PCP proofs (and also to stress that they are in sharp contrast to NP certificates), a simple example is given to show that \\(\lang{GNI} \in \PCP(\poly, 1)\\). I think this protocol is just a modification of the previous private coin interactive proof system for \\(\lang{GNI}\\) adapted to the PCP syntax.


## Lecture X {#lecture-x}

In this lecture, we learn the other form of PCP theorem --- the hardness of  approximation. In addition, we prove the equivalence between the two forms.


### The PCP is Optimal {#the-pcp-is-optimal}

This statement is kindof like the hierarchy theorem, in the sense that if we choose \\(r = o(\log(n))\\) and \\(q = o(\log(n))\\), then \\(\PCP \\) will collapse to (actually be a strict subset of) \\(\NP\\). On the other hand, we have the result that \\(\PCP(\poly, 1) = \NEXP\\). So our result is somewhat tight in this sense.

First let's prove that if \\(\NP \subseteq \PCP(o(\log), o(\log))\\), then \\(\P =  \NP\\). Suppose this is indeed the case, on input some \\(x\\), the verifier can enumerate over all possible random coins and query answers to find out whether \\(x\in L\\) (for some predetermined \\(L\\)) or not. The total time it takes will be polynomial.

The other result is not proved during the lecture.


### Hardness of Approximation {#hardness-of-approximation}

\begin{theorem}[The PCP theorem (hardness of approximation)]
There \\(\exists \rho < 1\\) such that for every \\(L \in \NP\\) there is a P-time computable function \\(f : L \to 3\SAT\\) such that
\begin{align\*}
x\in L &\implies \func{val}(f(x)) = 1 \\\\
x\not\in L & \implies \func{val}(f(x)) < \rho.
\end{align\*}
\end{theorem}

Notice that \\(\rho\\) is a constant strictly less than one. So we can let \\(L = 3\SAT\\) and do "local error amplification" through this method. Even if in the original formula \\(x\\), only one clause is unsatisfiable, the converted formula \\(f(x)\\) will have at least \\((1 - \rho)\\) portion unsatisfiable.

The syntax of this theorem resembles much of CL theorem. But on a closer inspection of the proof of CL theorem, one will see that for input \\(x \not\in L\\), it can be the case that \\(\func{val} = \frac{m-1}{m}\\) (we adhere to all the computation process, only changing the output from \\(0\\) to \\(1\\)). So this theorem cannot be proved using CL theorem alone.

To notice that this flavor of PCP theorem implies the hardness of approximation, we can view the mapping function \\(f\\) in the theorem as a reduction from any language \\(L\in \NP\\) to a **promise** version of \\(\text{Max-3SAT}\\). If we have a P-time algorithm that gives a &rho;-approximation of Max-3SAT, then we can effectively determine any \\(L\in\NP\\), indicating \\(\P = \NP\\).

Another way to phrase this theorem is that &rho;-approximaiton algorithm for Max-3SAT is \NP-hard.


### Equivalence of Two Forms {#equivalence-of-two-forms}

We have to prove the equivalence of the two forms. In order to do this, we introduce a third form, which is a generalization of the hardness of approximation form.


#### qCSP Problem --- a generalization to 3SAT {#qcsp-problem-a-generalization-to-3sat}

If \\(q\\) is a natural number, then a qCSP instance \\(\phi\\) with \\(n\\) variables is a collection of constraints \\(\phi\_1, \ldots, \phi\_m : \set{0,1}^n \to \set{0,1}\\) such that for each \\(i \in [m]\\) the function \\(\phi\_i\\) depends on \\(q\\) of its input locations.

We call \\(q\\) the arity of \\(\phi\\), and \\(m\\) the size of \\(\phi\\).

An assignment \\(u \in \set{0,1}^n\\) satisfies a constraint \\(\phi\_i\\) if \\(\phi\_i(u) = 1\\) Let

\begin{equation\*}
\func{val}(\phi) = \max\_u \\{ \frac{\sum\_{i=1}^m\phi\_i(u)}{m}\\}.
\end{equation\*}

We say that \\(\phi\\) is satisfiable if \\(\func{val}(\phi) = 1\\).

qCSP is a generalization of 3SAT.

From this definition we can make a couple of observations:

1.  We may suppose \\( n \le qm \\) since abundant literals can be deleted
2.  Every formula \\(\phi\\) can be described using \\(O(m q 2^q \log (n) \\) bits
3.  The simple greedy algorithm for Max-3SAT can be generalized to Max-qCSP and the approximation factor is \\(\frac{1}{2^q}\\).

While the first two observations are very obvious, I have yet find even how to generalize this algorithm. Maybe I will find this solution tomorrow.


#### GapCSP {#gapcsp}

Suppose \\(q \in \NN\\) and \\(\rho \le 1\\), we let &rho;-GAPqCSP be the problem that determines a qCSP instance &phi; whether

1.  satisfies that \\(\func{val}(\phi) = 1\\) or
2.  \\(\func{val}(\phi) < \rho\\).

We may say that &rho;-GAPqCAP is \NP-hard if for every \\(L \in \NP\\) there exists a P-time function \\(f\\) that satisfies

\begin{align\*}
x \in L &\implies \func{val}(f(x)) = 1, \\\\
x \not\in L &\implies \func{val}(f(x)) < \rho.
\end{align\*}

The intermediate form of PCP theorem states that there exists some \\(\rho \in (0,1)\\) such that &rho;-GAPqCSP is \NP-hard. Notice that the second formulation directly implies this one.


#### Equivalence Proof {#equivalence-proof}

First we prove "suppose \\(\NP = \PCP(\log, 1)\\)", there exists some \\(\rho\\) such that &rho;-GAPqCSP is \NP-hard.

Observe that we can "unwrap" the randomness of verifier since there is only logarithmatic many bits. So given any \\(L \in \NP\\) and \\(x\\), we can first construct the \PCP verifier \\(V\\) and then using CL theorem, construct a Boolean formula \\(\phi\_i(q) = V(x,q;r=i)\\) such that \\(\phi\_i : \set{0,1}^q \to \set{0,1}\\). By adding all \\(2^{O(\log)}\\) constraints we can obtain the formula \\(\phi\\). Completeness guarantees that when \\(x \in L\\) we have \\(\func{val}(\phi) = 1\\) while soundness guarantees that when \\(x \not\in L\\), we have \\(\func{val}(\phi) \le \frac{1}{2}\\).

And then we prove the opposite direction. Suppose there exists some &rho; such that &rho;-GAPqCSP is \NP-hard, we want to prove \\(\NP = \PCP(\log, 1)\\).

This is also very intuitive. For any \\(L \in \NP\\), the verifier can first convert it into an qCSP instance &phi;, and then randomly choose an index \\(i \sample [m]\\), finds out what \\(q\\) literals \\(\phi\_i\\) depends on, and query the prover about that \\(q\\)-bits in the assignment. Completeness is guaranteed since if \\(x \in L\\), \\(f(x)\\) is satisfiable. While soundness error is at most \\(\rho\\), since for any answer the verifier gives, at most \\(\rho\\)-portion is satisfied, so the verifier will be caught with \\(1 - \rho\\) probability.

While the argument is the same to that on the slides and on the textbook, I find it a bit dubious. The randomness \\(i\\) must be private otherwise there is no soundness. So how can we argue the query \\(q\\) does not leak \\(i\\)?

Perhaps the definition of \\(\PCP\\) already guarantees that the proof &pi; is "committed". The format is \\(V^{\pi}(x, r)\\) after all.

Finally we prove the equivalence between the last two views.

The hardness of approximating 3SAT directly implies the existence of some &rho;-GAPqCSP instance. So we have to prove the converse direction. We can write some q-literal constraint function \\(\phi\_i\\) as the conjunction of at most \\(2^q\\) clauses. If \\(\phi\_i\\) is not satisfied, then at least one of the clauses is not satisfied. So we simply reduced the approximation factor from \\(1 - \rho\\) to \\(1 - \frac{\rho}{2^q}\\).


## Lecture XI {#lecture-xi}

Onward to the proof of PCP !

But actually, we will only be concluding the difference between approximating \\(\minvc\\) and \\(\maxis\\) and introducing Fourier Transform over the finite field \\(GF(2^n)\\).


### Inapproximability {#inapproximability}

\minvc and \maxis are very different from an approximation point of view, as stated by this theorem.

\begin{theorem}
\\(\exists \rho < 1\\) s.t. \\(\rho\\)-approximation to \\(\minvc\\) is \\(\NP\\)-hard. \\(\forall \rho < 1\\), \\(\rho\\)-approximation to \\(\maxis\\) is \\(\NP\\)-hard.
\end{theorem}

\paragraph{Proof} This theorem relies on the reduction from \\(3\SAT\\) to \\(\maxis\\). First of all, the PCP theorem states that there exists \\(\rho\_0\\) such that \\(\rho\_0\\)Gap\\(3\SAT\\) is \NP-hard. Using the reduction, we conclude that \\(\frac{\rho\_0}{7}\\)-approximation for \\(\maxis\\) is also \NP-hard. Suppose we have an \\(\frac{6}{7-\rho}\\)-approximation algorithm for \minvc (&rho; = \\(\frac{\rho\_0}{7}\\)), then on this specific graph graph, since \\(|IS| < \frac{n}{7}\\), we have an

\begin{align\*}
\frac{n - IS}{n - \rho IS} &= \frac{ \frac{n}{IS} - 1}{ \frac{n}{IS} - \rho} \\\\
 &\ge \frac{6}{7 - \rho} \\\\
 &= \frac{6}{7 - \frac{6}{7 - \rho\_0}} \\\\
 &= \frac{42 - 6\rho\_0}{42 - 7\rho\_0} \\\\
 &\ge \frac{42\rho\_0 - 7\rho\_0^2}{42 - 7\rho\_0} \\\\
 &= \rho\_0.
\end{align\*}

This conclude the first part of the proof. For the second part, we use a "performance amplification" idea to prove that even if we have a small \\(\rho^{\prime}\\)-approximation algorithm for \maxis, then we can find \\(\rho\\)-approximation as well.

First of all, for a graph \\(G\\) with maximum-sized independent set \\(IS\\), observe that there exists a constant \\(k \in \NN\\) such that \\(\rho\_0 \binom{ \abs{IS} }{k} \ge \binom{\rho  \abs{IS} }{k}\\). In order to see this, let \\(k = \frac{\log \rho}{\log \rho\_0}\\), then \\( \rho\_0 \binom{ \abs{IS} }{k} \approx (\rho  \abs{IS} )^k \approx \binom{\rho  \abs{IS} }{k}\\).

Define a new graph \\(G^k\\) such that its every vertice is a \\(k\\)-subset of \\(G\\) and two nodes \\(S\_1\\) and \\(S\_2\\) are disconnected iff. \\(S\_1 \cap S\_2\\) forms an independent set of \\(G\\). Now we apply the \\(\rho\_0\\)-approximation algorithm to \\(G^k\\), and we claim that from its output, we can collect an independent set of \\(G\\) of size at least \\(\rho \abs{IS}\\).

The output of \\(\rho\_0\\)-approximation algorithm is at least \\(\rho\_0 \binom{\abs{IS}}{k} \ge \binom{\rho \abs{IS}}{k}\\) nodes. This implies there must be a \\(\rho\\)-portion of the independent set \\(IS\\) that can be extracted. This concludes the proof.


### Fourier Transform over \\(GF(2^{n})\\) {#fourier-transform-over-gf--2-n}

In this section we shall see that the three concepts are essentially the same:

-   Linear functions \\(\set{f : \bit^n \to \bit | f(x) + f(y) = f(x + y)}\\)
-   Fourier basis \\(\chi\_S(x)  = \mathop{\xor}\_{i \in S} x\_i\\)
-   Walsh-Hadamard codewords


#### Isomorphism {#isomorphism}

To simplify notations, we consider an isomorphic group \\(\set{\pm 1}\\) of \\(GF(2)\\). In that group, XOR operation is replaced with multiplication, \\(0\\) maps to \\(+1\\), and \\(1\\) maps to \\(-1\\).


#### Hilbert Space {#hilbert-space}

We call a linear space defined with inner product a **Hilbert Space**. In particular, we want to study the \\(2^n\\)-dimensional Hilbert space \\(\RR^{\set{\pm 1}^n}\\). Three operations are defined over this space:

Addition
: \\((f + g) (x) = f(x) + g(x)\\)

Scalar Multiplication
: \\((cf)(x) = c f(x)\\)

Expectation Inner Product
: \\( f \circ g = \expsub{x \in \set{\pm 1}^n }{f(x)g(x)}\\)

The standard orthogonal basis for this space is \\(\set{ e\_x }\_{x \in \set{\pm 1}^n}\\). We shall see that fourier basis are also a set of good orthogonal basis for this space.


#### Fourier Basis {#fourier-basis}

We define **Fourier Basis** \\(\set { \chi\_{\alpha} = \prod\_{i \in \alpha} x\_i : \alpha \subseteq [n]}\\). There are three properties about this basis:

Linearity
: \\(\forall \alpha \subseteq [n]\\), \\(\forall x, y \in \set{\pm 1}^n\\), \\(\chi\_{\alpha}(x)\chi\_{\alpha}(y) = \chi\_{\alpha}(x \cdot y)\\)

Unity
: \\(\forall \alpha \subseteq [n]\\), \\(\chi\_{\alpha} \cdot \chi\_{\alpha} = 1\\)

Orthogonal
: \\(\forall \alpha, \beta\\), \\(\alpha \ne \beta\\), \\(\chi\_{\alpha} \circ \chi\_{\beta} = 0\\)

The first property can be proved using \\( \chi\_{\alpha} (x) \chi\_{\alpha}(y) =  (\prod\_{i \in \alpha} x\_i \prod\_{i \in \alpha} y\_i = \prod\_{i \in \alpha} x\_i y\_i = \chi\_{\alpha} (x \cdot y)\\).

The second property can be proved using the first property. Since \\(\chi\_{\alpha} \circ \chi\_{\alpha} = \expsub{x}{\chi\_{\alpha}(x) \chi\_{\alpha}(x) = \expsub{x}{\bf 1}} = 1\\).

The third property is commonly refered to as "random subsum principle". It can be explained in the following way. WLOG, we can assume there exists a set \\(\gamma = \alpha \setminus \beta \ne \emptyset\\). Fixing any assignment local to &beta; and summing over all other assignments, we would get changes only at \\(\chi\_{\alpha}\\). And the result would be zero, since the number of odd sums and even sums are equal. So by summing over all possible assignments local to \\(\gamma\\), we can prove this principle.


#### Other Properties {#other-properties}

Let \\(f = \hat{f}\_{\alpha} \chi\_{\alpha}\\), then we have \\(\hat{f}\_{\alpha} = f \circ \chi\_{\alpha}\\) and \\(f \circ f = \sum\_{\alpha} \hat{f}\_{\alpha}^2\\).


#### More on Linearity {#more-on-linearity}

Suppose some function \\(f : \set{\pm 1}^n \to \set{\pm 1}\\) is "partially linear", i.e.

\begin{equation\*}
\Pr\_{x, y} [f(x) f(y) = f(x \cdot y)] \ge \frac{1}{2} + \epsilon,
\end{equation\*}

the next theorem states that the largest fourier coefficient of \\(f\\) is larger than \\(\epsilon\\).

\paragraph{Proof}. Since \\(f\\) is binary, we have

\begin{align\*}
\expsub{x, y}{f(x)f(y) f(x\cdot y)} \ge 2 \epsilon.
\end{align\*}

Then by expanding the left term, we get

\begin{align\*}
\expsub{x, y}{f(x)f(y) f(x\cdot y)} &= \expsub{x, y}{\sum\_{\alpha} \hat{f}\_{\alpha} \chi\_{\alpha}(x) \sum\_{\beta} \hat{f}\_{\beta} \chi\_{\beta}(y) \sum\_{\gamma} \hat{f}\_{\gamma} \chi\_{\gamma}(x \cdot y)} \\\\
&= \expsub{x,y}{\sum\_{\alpha, \beta, \gamma} \hat{f}\_{\alpha} \hat{f}\_{\beta} \hat{f}\_{\gamma} \chi\_{\alpha}(x) \chi\_{\beta}(y) \chi\_{\gamma}(x) \chi\_{\gamma}(y) )} \\\\
&= \sum\_{\alpha, \beta, \gamma} \hat{f}\_{\alpha} \hat{f}\_{\beta} \hat{f}\_{\gamma} \expsub{x}{\chi\_{\alpha}(x)\chi\_{\gamma}(x)} \expsub{y}{\chi\_{\beta}(y) \chi\_{\gamma}(y)} \\\\
&= \sum\_{\alpha} \hat{f}\_{\alpha}^3 \\\\
&\le \max\_{\alpha}{\hat{f}\_{\alpha}} \sum\_{\alpha}{\hat{f}\_{\alpha}^2} \\\\
&= \max\_{\alpha}{\hat{f}\_{\alpha}}.
\end{align\*}

Thus this concludes this theorem.

Notice that the converse might not hold.

```python
import itertools
lst = list(itertools.product([-1, 1], repeat=6))

def maj(x):
    return (1/2 * x[0] + 1/2 * x[1] + 1/2 * x[2] - 1/2 * x[0] * x[1] * x[2])

def pred(x):
    a = maj(x[0:4]) * maj(x[3:6])
    y = [x[i] * x[i+3] for i in range(3)]
    b = maj(y)
    if a == b:
        return 1
    else:
        return 0

cnt = 0
for x in lst:
    if pred(x) == 1:
        cnt += 1

return cnt, cnt / len(lst)
```


#### Closeness {#closeness}

For two functions \\(f\\), \\(g\\), we call \\(f\\) is \\(\rho\\)-close to \\(g\\), if \\(\Pr\_x [f(x) = g(x)] > \rho\\). Notice that if we restrict our attentions to \\(f, g: \set{\pm 1}^n \to \set{\pm 1}\\), then it is equivalent to \\(\expsub{x}{f(x)g(x)} = f \circ g> 1 - 2\rho\\). If we set \\(\rho = \frac{1}{2} + \epsilon\\), this would be much clearer. We can further make further observations:

-   If \\(\Pr\_{x, y}[f(x) f(y) = f(x \cdot y)] \ge \frac{1}{2} + \epsilon\\), then \\(f\\) is \\(2\epsilon\\)-close to \\(\chi\_{\alpha}\\), where \\(\hat{f}\_{\alpha}\\) is \\(f\\)'s largest Fourier coefficient.
-   If \\(f, g : \set{\pm 1}^n \to \set{\pm 1}\\), and \\(f \circ g \ge 2 \epsilon\\), then we have \\(f\\) and \\(g\\) coincides at \\(\frac{1}{2} + \epsilon\\) portion of the input domain.


### Efficient Conversion of \\(\NP\\) Certificates to \\(\PCP\\) Proof {#efficient-conversion-of-np-certificates-to-pcp-proof}

In this section we prove that \\(\NP \subseteq \PCP(\poly, 1)\\). This is a weaker version of **the** PCP theorem, but its certificate conversion technique makes a good use of the error-amplification capability of Walsh-Hadamard code, and is in nature very useful even in the big proof. So we will study it in this section.


#### Walsh-Hadamard Code {#walsh-hadamard-code}

We first define the Walsh-Hadamard function \\(\func{WH}(u) : x \mapsto u \cdot x\\). This function encodes \\(n\\)-bit strings into a linear function.

We say \\(f\\) is a Walsh-Hadamard codeword if \\(f = \func{WH}(u)\\) for some \\(u\\). Since a linear function's evaluation can be written as \\(f(x) = \sum\_i f(e\_i) x\_i\\), we conclude that linear functions are exactly Walsh-Hadamard codewords.


#### Local Testing {#local-testing}

The goal of local testing is to verify whether \\(f\\) is a linear function with **constant** query complexity. For \\(\delta < \frac{1}{2}\\), we define an \\((1 - \delta)\\)-linearity test such that if a function \\(f\\) is not \\((1 - \delta)\\)-close to some linear function, then the test rejects with probability \\(\ge \frac{1}{2}\\).

The test is as follows. Randomly sample \\(x, y\\) and rejects if \\(f(x)f(y) \ne f(x\cdot y)\\). Repeat this process for \\(\frac{1}{\delta}\\) times, and if all tests pass, accept the input.

The error probability of this algorithm is \\(( 1 - \delta )^{\frac{1}{\delta}} \approx \frac{1}{e} < \frac{1}{2}\\).


#### Local Decoding {#local-decoding}

The goal of local decoding is to evaluate \\(f\\) even if we only have a lossy source.

Suppose \\(f\\) is \\((1 - \delta)\\)-close (for some \\( \delta < \frac{1}{4}\\)) to some linear function \\(g\\), then we can evaluate \\(g(x)\\) by samplying \\(x^{\prime}\\) at random and output \\(f(x \cdot x^{\prime}) f(x^{\prime})\\). Using a union bound we conclude the error probability is at most \\(1 - 2\delta\\).


#### \\(\NP \subseteq \PCP(\poly, 1) \\) {#np-subseteq-pcp--poly-1}

At this point I realized it is absolutely unnecessary and a waste of time reproducing all the fine details already wonderfully presented in the textbook and slides, so I will be brief in this section.

The proof is in three steps, plus a prequisite reduction to \\(\lang{CKT}\mbox{-}\SAT\\). Notice that using arithmetization, we can use a quadratic equation of the form \\(A \cdot (u \otimes u) = b\\) to prove the satisfiability of a Boolean circuit.

So our \\(\PCP\\) verifier \\(V^{\pi }(x) \\) (\\(\pi = (f, g)\\)) proceeds in the following three steps:

1.  Perform a \\(1 - \delta\\) linearity test on \\(f, g\\)
2.  Sample \\(x, y \sample \bit^n\\)  and test \\(f (x) f(y) = g(x \otimes y)\\)
3.  Sample \\(r \sample \bit^m\\) and test \\(g(r^T A) = r^T b\\)

The first step ensures \\(f, g\\) are indeed WH codewords (say, they encode \\(w\\) and \\(u\\)). The second step verifiers \\(u = w \otimes w\\). In this step, what we actually do is to verify \\( (w \otimes w) \circ (x \otimes y) = u \circ (x\otimes y)\\). If \\(u \ne w \otimes w\\), there will be half of the position that this equality will not hold, hence the soundness is \\(\frac{1}{2}\\). The third step uses a good randomization (hashing) technique. If once again \\( A u \ne b\\), by selecting a random \\(r\\), \\(Pr\_r [r^T (Au + b) = 0]  = \frac{1}{2}\\). Hence the soundness error.


## Lecture XII {#lecture-xii}

In this lecture Prof. Fu started by reviewing the proof of "reduced \\(\PCP\\) theroem". After that, he began introducing several prequisitives to the actual proof of **the** \\(\PCP\\) theorem.


### Local Testing / Decoding of WH Codeword {#local-testing-decoding-of-wh-codeword}

Recall that with constant random queries, we can perform linearity testing and decoding of Walsh-Hadamard codewords. In particular,

-   \\(\forall \delta \in (0,1)\\), we can reject any codeword \\(f\\) that is not \\(1 - \delta\\)-close to some linear function with probability at least \\(\frac{1}{2}\\), by making \\(\frac{1}{\delta}\\) pairwise-independent queries to \\(f\\).
-   \\(\forall \delta \in (0, \frac{1}{2})\\), and \\(\forall x \in \bit^n\\),  if some codeword \\(f\\) is \\(1 - \delta\\)-close to some linear function \\(\hat{f}\\), we can decode \\(\hat{f}(x)\\) with probability at least \\(1 - 2\delta\\), by sampling a random \\(x^{\prime}\\), query \\(f(x^{\prime})\\) and \\(f(x + x^{\prime})\\), and finally output \\(f(x^{\prime}) + f(x^{\prime} + x)\\).


### Quadratic Equation in GF2 {#quadratic-equation-in-gf2}

The satisfiability problem of quadratic boolean equations is \\(\NP\\)-complete. This can be proved by reducing the \\(\NP\\)-complete problem \\(\cktsat\\) to \\(\quadeq\\). We can introduce a variable for every wire on the circuit, and then translate the circuit gate-by-gate:

-   \\(z = \neg x \to ZZ + XX = 1\\)
-   \\(z = x \land y \to ZZ + XY = 0\\)
-   \\(z = x \lor y \to ZZ = 1 - (1 - X)(1- Y) \iff ZZ + XX + YY + XY = 0\\)

It is trivial that the translation is in polynomial time (even in logspace), and the equation is satisfiable if and only if the circuit is satisfiable.


### Prequisitives to PCP {#prequisitives-to-pcp}

The basic idea of \\(\PCP\\) proof is very simple: gap amplification through random walk. But in order to "reduce" the problem into graph objects, we need to fiddle with the CSP instances a bit.


#### CSP {#csp}

We generalize qCSP to non-binary alphabet (w.l.o.g we denote as \\([W]\\)) as \\(q\CSP\_W\\). And then define the promise version of CSP as \\(\rho\\)-GAP \\(q\CSP\\).

Our goal therefore translates to proving the \\(\NP\\)-hardness of \\(\rho\\)-GAP \\(q\CSP\\) problem for some constant \\(q\\) and \\(\rho\\).


#### CL-Reduction {#cl-reduction}

We will be working on CSP instances iteratively, so it is nice to bound the size growth during this process. Let \\(f\\) be a function mapping \\(\CSP\\) instances into \\(\CSP\\) instances. We call \\(f\\) a Constant-Linear blowup reduction if the following two conditions hold:

-   \\(x\\) is satisfiable iff. \\(f(x)\\) is.
-   \\(\exists C, W\\) that only depends on the arity and alphabet size of \\(x\\), and \\(f(x)\\) is over a new alphabet \\([W]\\) and has no more than \\(C m\\) constraints (where \\(m\\) is the number of constraints in \\(x\\)).


#### Main Lemma {#main-lemma}

\begin{lemma}
There exist constants \\(q\_0 \ge 3\\) \\(\epsilon\_0 > 0\\) and CL-reduction \\(f\\) such that for
every \\(q\_0\CSP\\) instance \\(\varphi\\) and every \\(\epsilon < \epsilon\_0\\) \\(f(\varphi)\\) is a \\(q\_0\CSP\\) instance satisfying
\begin{equation\*}
\func{val}(\varphi) < 1 - \epsilon \implies \func{val}(f(\varphi)) < 1 - 2 \epsilon.
\end{equation\*}
\end{lemma}

To see that this lemma implies the PCP theorem, we can prove the \\(\NP\\)-hardness of \\(\epsilon\_0\\)-GAP \\(q\_0\CSP\\) by applying the lemma \\(\log m\\) times. So this lemma will be the main objective of the following three lectures.

As we will see, the proof of this lemma proceeds in three steps:

1.  Reduce \\(q\_0\CSP\\) instance to \\(2\CSP\_W\\) instance which is "nice"
2.  Amplify the error of \\(2\CSP\_W\\) instance by introducing a larger alphabet \\(2\CSP\_{W^{\prime}}\\)
3.  Reduce the alphabet size back to \\(2\\) and increase the arity back to \\(q\_0\\)


## Lecture XIII {#lecture-xiii}

Today, we focus on Step 1 in the proof of PCP theorem.

I must say Prof. Fu's decision that we should not proceed beyond the prequisitives of Lemma 2 is indeed wise.

Lemma 2 intuitively uses path product's effect to amplify gap.


### Definition of Nice {#definition-of-nice}

For any \\(2\CSP\_W\\) instance \\(\varphi\\), we define its constraint graph \\(G\_{\varphi}\\) by introducing \\(n\\) vertices, and an edge between every two literals in an constraint.
A \\(2\CSP\_W\\) instance \\(\varphi\\) is called "nice" if

1.  There is a constant \\(d\\) such that \\(G\_{\varphi}\\) is a (\\(d\\), \\(0.9\\))-expander.
2.  At every vertex half of the edges are self-loops. (Note that we allow parallel edges and self-loops.)


### Lemma on Connectivity {#lemma-on-connectivity}

Let \\(G\\) be a \\(d\\)-regular graph with \\(n\\) vertices. Let \\(S\\) be a subset of its vertices and \\(T\\) be its compliment, we have

\begin{equation\*}
\abs{ E(S, \bar{S}) } \ge (1 - \lambda\_G) \frac{d \abs{S} \abs{\bar{S}}}{n}.
\end{equation\*}

This can be proved by defining \\(x\\) such that \\( x\_i = \abs{S} \\) where \\(i \in T\\) and \\( x\_i = \abs{T}\\) where \\(i \in S\\). It is clear that \\(x \perp \one\\) so we can bound \\(x^T A x\\) from Rayleigh quotient.

The proof proceeds by considering the value \\(\sum\_{i, j} A\_{i, j} (x\_i - x\_j)^2\\). By definition, only those indices like \\(i \in S\\) and \\(j \in T\\) will be summed. So the value equals to \\(\frac{2 \abs{ E(S, T) } n^2}{d}\\). But we can also expand this equation and get \\(2 \norm{x}^2 - 2 x^T A x\\). So we have

\begin{align\*}
\frac{2 \abs{ E(S, T) } n^2}{d} &= 2 \norm{x}^2 - 2x^T A x \\\\
\frac{2 \abs{ E(S, T) } n^2}{d} &= 2 (\abs{S} \cdot \abs{T}) n  - 2x^T A x \\\\
\frac{2 \abs{ E(S, T) } n^2}{d} &\ge 2 (\abs{S} \cdot \abs{T}) n  - 2 (\lambda\_G) (\abs{S} \cdot \abs{T}) n \\\\
\abs{ E(S, T) } &\ge (1 - \lambda\_G) \frac{d \abs{S} \abs{T}}{n}.
\end{align\*}


### Corollary on Random Edge {#corollary-on-random-edge}

Suppose \\(G\\) is an expander, we can bound the probability that a random edge will be inside a subset \\(S : \abs{S} \le \frac{n}{2}\\) by \\( \frac{\abs{S}}{n} (\frac{1}{2} + \frac{\lambda\_G}{2})\\). If we consider the path-product graph \\(G^l\\), then the result will be \\( \frac{\abs{S}}{n} (\frac{1}{2} + \frac{\lambda\_G^l}{2})\\), which also corresponds to random length \\(l\\) paths in \\(G\\).

The proof is very simple. Since we are on a \\(d\\)-regular graph, randomly choosing an edge is equivalent to randomly choose a vertex and then do one-step random walk. So we have

\begin{equation\*}
\frac{\abs{S}}{n} = \Pr\_{u, v \sample E}[ u \in S \land v \in S] + \Pr\_{u, v \sample E} [u \in S \land v \in T].
\end{equation\*}

Where the latter one is bounded by \\(\frac{\abs{S}}{n} (\frac{1}{2} - \frac{\lambda\_G}{2} )\\), thus proving this corollary.


### Transfigured Instances {#transfigured-instances}

Since I think it is a waste of time to produce all the fine details which are already well-explained in the textbook and slides, I will only explain my understanding of key components in this proof.

First we reduce the arity to \\(2\\), by enlarging the alphabet to \\(2^{q\_0}\\). Now the new assignments can be understood as a \\(q\_0\\)-long bit vector. We then introduce \\(m q\_0\\) constraints, labelled as \\(\varphi\_{i, j}\\) that checks \\(y\_i\\) satisfies the original constraint \\(\varphi\_i\\) and the \\(j^{th}\\) variable in \\(\varphi\_i\\) agrees with the assignment in \\(y\_i\\). The size of such constraint is at most \\(2^{q\_0 + 1}\\).

We would also like to analyze the gap changes through these steps. At this step, since we expand the constraints by \\(q\_0\\) times, it holds that the gap deteriorates by at most \\(\frac{1}{q\_0}\\).

Then we want to make the constraint graph regular. We do so by first finding a family of (\\(d - 1\\), \\(0.9\\))-expander graph family, and replacing every degree-\\(k\\) by \\(G\_k\\). We then adds identity constraint to every internal edges, and add one external edge to every new nodes. It is straight forward to argue that the new graph is \\(d\\)-degree and there are \\(2m\\) nodes.

At this step, we need to use the expander property to analyze the gap loss. In particular, for any assignment to the "node cluster" that corresponds to some original variable \\(x\_i\\), we define its **plurality** value as \\(w\_i\\). Then let \\(t\_i\\) to be the number of nodes in that cluster that disagrees with \\(w\_i\\). It is clear that  \\(\sum\_i t\_i \le 2m - \frac{2m}{W}\\). The intuition is when \\(\sum\_i t\_i\\) is small enough, then violated external edges will be large enough, whereas otherwise, the expander property will ensure that the violated internal edges will be large enough.

In particular, consider the case \\(\sum\_i t\_i \ge \frac{\epsilon m }{4}\\). Let \\(S\_i\\) be the set of nodes  that agrees with \\(w\_i\\) and \\(\bar{S\_i}\\) its compliment in that cluster, and define \\(\abs{S\_i } + \abs{ \bar{S\_i} } = k \\). By the expander property, we know that \\(\abs{ E(S\_i , \bar{S\_i}) } \ge (1 - \lambda\_G) \frac{(d - 1) \abs{S\_i} \abs{\bar{S\_i}} }{k}\\). By definition, we have \\(\frac{\abs{S\_i}}{k} \ge \frac{1}{W}\\). So altogether we have

\begin{equation\*}
\sum\_i \abs{ E(S\_i , \bar{S\_i}) } \ge 0.1 \frac{(d - 1) t\_i}{W} \ge \frac{\epsilon}{100dW} dm.
\end{equation\*}

On the other hand, if we have \\(\sum\_i t\_i < \frac{\epsilon m}{4}\\) then we can lower bound the violated constraints like this. Suppose all edges have the assignment \\(w\_i\\), then at least \\(\epsilon m\\) external edges are violated. By changing at most \\(\sum\_i t\_i\\) terms, at most \\(2 \sum\_i t\_i < \frac{\epsilon m}{2}\\) constrained are altered. Thus we still have at least \\(\frac{\epsilon m }{2} \\) violated constraints, which suffices, since \\(\frac{\epsilon m }{2 } > \frac{\epsilon}{100 dW} dm\\).

Finally, we need to equip this graph with enough self-loops and make it an expander. We do so by adding \\(2d\\) self-loops at every node and embedding a (\\(n\\), \\(d\\), \\(0.1\\))-expander graph on top. The violated constraints will deterate by at most \\(4\\), and the spectral gap is at most \\(0.1 \cdot \frac{1}{4} + \frac{3}{4} < 0.9\\).

Notice that all the gap worsening factors only depend on \\(W\\) and \\(d\\), which depends on the arity \\(q\_0\\) and is a constant respctively. So regradless of the expression, we can conclude that any loss of this step only depends on the arity \\(q\_0\\) (which as we put together all three pieces, will be a constant).


## Lecture XIV {#lecture-xiv}

We cover gap amplification lemma (i.e. Step 2 of the PCP proof) in this lecture. The essense of it seems to be probabilistic method.


### Basic Idea {#basic-idea}

By performing a \\(t\\)-step random walk on the constraint graph, and taking the conjunction of all the constraint edges, we can get roughly the same effect of taking \\(t\\) random edges, and the gap can surely be amplified. But in this way we are increasing the arity. In order to keep the arity at \\(2\\), Dinur's idea is to increase the alphabet by letting a single variable representing the assignment of all \\(d^t\\) old variables (forming a circle / cluster around one variable). But in order to check the old constraints as well as consistency, we need to introduce new constraints, and some probabilistic methods of analyzing the gap amplifaciton effect.


### Details {#details}

Consider a \\(2\CSP\_W\\) instance \\(\varphi\\) and its constraint graph \\(G\_{\varphi}\\). We identify each variable / node by \\(x\_i\\) and constraint / edge \\(\varphi\_j(u, v)\\). We then introduce \\(X\_i\\) as the assignment of circle of nodes of radius \\(t + \sqrt{t}\\) from the node \\(x\_i\\), with its alphabet \\(W^{d^{5t}}\\) (its a sufficiently large number).

As for the constraints, for each length \\(2t + 1\\) path \\(p\\), we
place an constraint \\(C\_p\\) of the form \\(\land\_{j \in [t - \sqrt{t},
t + \sqrt{t}] } C\_p^j\\) where \\(C\_p^j\\) is the constraint
corresponding to the \\(j^{th}\\) edge on the path, and wht \\(x\_j\\)
replaced with \\(X\_1\\)'s claim on \\(x\_j\\) and \\(x\_{j+1}\\) with
\\(X\_{2t+2}\\)'s claim.


## Lecture XV {#lecture-xv}

In this lecture we will finish Step 3 of the PCP proof. It is reletively easy to follow.


### Threshold Result by Hastad's 3-Bit \\(\PCP\\) Theorem {#threshold-result-by-hastad-s-3-bit-pcp-theorem}

This is called "threshold" result because there exists an \\(\frac{7}{8}\\)-approximation algorithm for \\(\maxsat\\). Actually I get a little bit confused at this problem, but then I realized the textbook already had explanations. First of all, by randomly selecting all literals, we can get an algorithm that with overwhelming probability outputs an assignment that satisfies at least a \\(\frac{7}{8}\\)-portion of the clauses. We can derandomize it in the following ways:

The first way is to observe that since \\(\expect{\func{val}(\varphi(x))} = \frac{7m}{8}\\), we have

\begin{equation\*}
\expect{\func{val}(\varphi(x))} = \frac{1}{2} \expect{\func{val}(\varphi(x| x\_1 = 0))} + \frac{1}{2} \expect{\func{val}(\varphi(x| x\_1 = 1))}
\end{equation\*}

and by checking the clause length, we can compute in polynomial time the condictional expectations, we can conclude that we can iteratively find such an assignment that satisfies at least a \\(\frac{7}{8}\\) portion of the clauses.

The second way is by using \\(3\\)-wise independent hash function. By considering a larger field \\(GF(2^l)\\) where \\(l = \ceil{ \log (n) }\\), we can define the hash function \\(f\_{a,b,c}(x) = ax^2 + bx + c\\), and then by the property of Vandermont matrix, we have the sequence \\(f(0)\\), \\(f(1)\\), \\(\ldots\\), \\(f(n - 1)\\) is three-wise independent, and that suffices for the purpose of the distribution over assignment. The expectation claim still works, but since we are working on a polynomial sized sample space, we can do an exhausive search to find such an assignment.

Actually I find this version by scribes from some Oded Goldreich's student. Here is the [lecture website](http://www.wisdom.weizmann.ac.il/~oded/rnd-sum.html).


### Final Examination {#final-examination}

All scores are B+? If higher scores are desired, you should give a presentation on Chapter 22.6 and Chapter 22.7. The topic is the proof of Hastad theorem and 22.6 is mandetory.


## Lecture XVI {#lecture-xvi}

What will we cover in this lecture? Cryptography!

Cryptography from a computational complexity perspective, and a strong focus on pseudorandomness.


### Introduction {#introduction}

Modern cryptography is based on computational complexity is a commonly acknowledged fact.

One-way function is the foundation of modern cryptography.


### Computationally Secure Encryption {#computationally-secure-encryption}

Syntax: A pair of algorithms \\(\enc\\), \\(\dec\\). The key is considered as an index to the two algorithms. In this syntax, \\(\enc\_k\\) must be injective to ensure correctness.


#### Shannon's Perfect Secrecy {#shannon-s-perfect-secrecy}

For any two length-equal plaintext, the distributions of their ciphertexts under uniformly random key are identical.

One-time pad is one example of perfectly secure encryption.

That key length must be longer than message length (i.e. Shannon theorem) is implied by a later lemma.


#### Negligible Functions {#negligible-functions}

A function \\(\epsilon : \NN \to [0,1]\\) is negligible if

\begin{equation\*}
\forall c \exists N \forall n \ge N \epsilon(n) < \frac{1}{n^c}.
\end{equation\*}

A function is negligible if it goes to 0 faster than any inverse of polynomial functions.


#### Computationally Secure Encryption Scheme {#computationally-secure-encryption-scheme}

An encryption scheme (\\(\enc\\), \\(\dec\\)) is computationally secure if for any \\(\P\\)-time PTM \\(A\\) there is a negligible function \\(\epsilon\\) such that

\begin{equation\*}
\abs{ \Pr\_{x \sample \bit^{m}, k \sample \bit^n}[ A(\enc\_{k}(x)) = (i, b) \land x\_i = b] - \frac{1}{2} } \le \epsilon(n).
\end{equation\*}


#### Conditions on the Existence of Computationally Secure Encryption {#conditions-on-the-existence-of-computationally-secure-encryption}

Suppose \\(\P = \NP\\)

So in conclusion, we must assume \\(\P \ne \NP\\) in cryptography. In fact, we need the existence of OWF in cryptography, which is stronger than \\(\P \ne \NP\\).


### Pseudorandom Generator {#pseudorandom-generator}

We need to shorten keys. This is done by replacing statistical randomness with computational ones.

Although **computational** only makes sense if we consider time-resource constrained adversaries.

Syntax: Let \\(G: \bit^{\*} \to \bit^{\*}\\) and \\(l : \NN \to \NN\\) be \\(\P\\)-computable such that \\(l(n) > n\\) for all \\(n\\) for all \\(n\\) and \\(\abs{G(x)} = l(|x|)\\) for all \\(x \in \bit^{\*}\\).

\\(G\\) is a computationally secure PRG of stretch \\(l(n)\\) if for every \\(\P\\)-time PTM \\(A\\) there exists a negligible function \\(\epsilon : \NN \to [0,1]\\) such that

\begin{equation\*}
\abs{ \Pr[A(G(U\_n)) = 1] - \Pr[A(U\_{l(n)}) = 1] } \le \epsilon(n).
\end{equation\*}

Prior to Yao's notion of PRG, there is another unpredictability notion. Let \\(G\\) and \\(l\\) be as defined above, then we have for all \\(\P\\)-ime PTM \\(B\\) there is a negligible \\(\epsilon\\) such that

\begin{equation\*}
\abs{ \Pr\_{x \sample \bit^n, y := G(x), i \sample [l(n)]} [B(1^n, y\_1, \ldots, y\_{i-1}) = y\_i] - \frac{1}{2}} \le \epsilon(n).
\end{equation\*}

The two notions are equivalent.


### Application: Derandomization {#application-derandomization}

If PRG exists, then we can construct subexponential deterministic algorithms for problems in \\(\BPP\\).


### Pseudorandom Function {#pseudorandom-function}

A random function mapping \\(n\\)-bits to \\(n\\)-bits takes \\(n
2^n\\)-bits to describe, and are often very inefficient to compute. We
want to find a subset of these functions, so that it has the effect
that when randomly picking one from this subset, it has in some sense
the same effect as randomly picking from all mapping functions.

Since the description of a bona fide random function is very large, we
have to use oracle Turing machine to capture the indistinguishability
by computationally-confined distinguishers.

The equivalence between PRG and PRF: the GGM tree.


### PRF Applications {#prf-applications}

1.  CPA Secure encryption
2.  Message authentication code: \\(x \mapsto f\_k(x)\\)
3.  Lower Bound for Machine Learning
    Roughly speaking, PRF is not learnable but this does not seem like a useful result.


## Lecture XVII {#lecture-xvii}

We try to finish the cryptography chapter this lecture.


### One-Way Function {#one-way-function}

It seems like OWF takes its definition from that of the unpredictability of PRG.
But I think there are still some major differences.

We then try to prove the equivalence between PRG and OWF.


#### Existence of OWF implies \\(\P \ne \NP\\) {#existence-of-owf-implies-p-ne-np}

The language \\(\set{ (l, u, y) | \exists x. f(x) = y \land l \le x \le u } \in \NP\\). So if we assume \\(\P = \NP\\) then this language is in \\(P\\), which implies we can invert \\(f\\) using binary search.

The existence of OWF implies \\(\P = \NP\\) implies that to actually prove one-wayness is going to be very hard. Cryptography can only rely on conjectures.


#### OWF implies PRG {#owf-implies-prg}

Two theorems.

1.  OWP implies PRG with polynomial stretch [Yao82]
2.  OWF implies PRG with polynomial stretch [HILL99]

Since the second theorem has very involved proof, we will only prove the first theorem.
Let \\(G(x,r ) = f(x), r, x^T r\\) where \\(f\\) is a one-way permutation.


#### Goldreich Levin Theorem {#goldreich-levin-theorem}

The text book uses a three stage proof, each corresponding to increasingly weaker additional assumptions, for pedagogical purpose.

\paragraph{Case 1.} The algorithm \\(A\\) can return \\(x^T r\\) for all \\(x\\), \\(r\\). Then we can find \\(x\\) by making \\(n\\) invocations.


### Application: Tossing Coin Over Phone {#application-tossing-coin-over-phone}

1.  Alice samples \\(x, r \sample \bit^n\\) and sends \\(f(x), r\\) to Bob, where \\(f\\) is an OWP.
2.  Bob sends \\(b \sample \bit\\) to Alice
3.  Alice sends \\(x\\) to Bob
4.  Both agree on \\(x^T r \oplus b\\)


### Zero Knowledge Proof {#zero-knowledge-proof}

A zero-knowledge proof system for any \\(L \in \NP\\)

Completeness
: prover can convince verifier for all \\(x \in L\\)

Soundness
: verifier can reject prover for all \\(x \not \in L\\)

Perfect Zero Knowledge
: There for all \\(\P\\)-time PTM verifier \\(P^{\*}\\), exists an expected \\(\P\\)-time PTM \\(S^{\*}\\) (the simulator) that for any \\(x \in L\\) and its certificate, the following holds

\begin{equation\*}
\func{out}\_{V^{\*}}( P(x, u), V^{\*}(x) ) \equiv S^{\*}(x).
\end{equation\*}


## Lecture XVIII {#lecture-xviii}

This lecture we want to focus on proof complexity.

The goal of proof complexity is to prove lower bounds on proof size for
tautologies in various proof systems.

The most famous lower bound problem is \\(\P\\) vs. \\(\NP\\), but it is **too hard**.

So we want to consider lower bound in some restricted models, e.g. proof
complexity, circuit lower bound, decision tree, etc.

To study proof complexity of a system one takes a look at a **special** problem
instance.


### Synopsis {#synopsis}

1.  Examples
2.  Propositional calculus and resolution


### Examples {#examples}

There are many examples in the textbook, although Prof. Fu will only introduce
one example.

In AI and formal verification, we often need to check if a proposition is a
tautology. These problems are \\(\coNP\\)-hard, so they are not believed to have
short proofs. (Because most axiomic systems include propositional logic)

\paragraph{The Example} Suppose \\(A\\) is an \\(n \times n\\) integer matrix and
\\(b\\) is an \\(n\\)-dimensional integer vector.

We want to find a **integer** solution \\(a\\). We can find the solution set which
we denote \\(\mathcal{H}\\) as it is a Hilbert set, and it has well quasi-order as
we define \\(a\_1 \le a\_2\\) iff. \\(\forall i \in [n] a\_1(i) \le a\_2[n]\\).

So with regard to \\(A, b\\) we can define its \\(\mathcal{H}\\) set and its finite.

\begin{lemma}
\\(\norm{m}\_1 \le (1 + n \norm{A}\_{\infty} + n \norm{b}\_{\infty})^{r+1}\\) where \\(r\\) is the rank of \\(A\\).
\end{lemma}

With this lemma, we know the set \\(\mathcal{H}\\) is polynomial-sized.


### Propositional Calculus and Resolution {#propositional-calculus-and-resolution}

命题演算 is propositional calculus.

Our goal is given a propositional clause \\(\phi\\), to prove it is a tautology.
The idea is to prove \\(\neg \phi\\) is a contradiction. So we make it a CNF
\\(\psi\\).


#### Resolution {#resolution}

Suppose \\(\varphi = C\_1 \land C\_2 \land \ldots \land C\_m\\), by resolution we
mean to extend a sequence \\(C\_1 \land \ldots \land C\_m \land C\_{m+1} \land
C\_{j-1}\\) to \\(C\_1 \land \ldots \land C\_m \land C\_{m+1} \land C\_{j-1} \land
C\_j\\). Where \\(C\_j\\) is \\(C^{\prime} \lor C^{\prime\prime}\\) and

Resolution is both sound and complete, and its length is at most \\(2^{O(n)}\\).


#### Pigeon Hole Problem {#pigeon-hole-problem}

雀（鹊）巢原理，啊，我这里有一杯咖啡。 --- Prof. Fu

We restrict our attention to the pigeonhole problem.


### Conclusion {#conclusion}

This lecture concludes the year-long lectures.

Part I of this textbook introduces classical results on Turing machine.

In part II, people focus on more specific compuational models, trying to prove
some lower bound results, e.g. circuit complexity, communication complexity,
algebaric complexity (an extension to circuit complexity), proof complexity,
etc.

Part III of this textbook mainly focuses on pseudorandomness, although
it is rather hard to make further progress. _Rick From 2023 says that
he witnessed some progress in the UOWHF construction in this year's
Eurocrypt by Xinyu Mao, so he would say that certain progress is still
possible. So I guess don't lose hope_

Complexity knowledge in the lectures should serve as aids to further
investigate theoretical problems in other branches in computer
science.

The exam lecture should be 90min long.

[^fn:1]: I remember Prof. Fu mentioned that this technique is typically
    used to prove certain abilities can be "scaled up", i.e. the
    ability to solve small scale problems can be used to "bootstrap"
    bigger problems. Or in the other direction, small impossibilities
    can be proved using bigger ones.
[^fn:2]: I think diagonalization reveals the inherent limit of a finite
    machine, and to construct a machine/language is just a way to
    reveal the contradiction.
[^fn:3]: This is a naive idea, more polished result should be available,
    but I think reducing the number of tape is a bit meticulous.
