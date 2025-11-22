<img align="left" src="img/icon-readme.png">

# @xamidi/luk-pmproofs ([repository](https://github.com/xamidi/luk-pmproofs))

Variant of [metamath/mmsolitaire/pmproofs](https://us.metamath.org/mmsolitaire/pmproofs.txt) of the [Metamath Solitaire project](https://us.metamath.org/mmsolitaire/mms.html) which uses alternative axioms

|    | Infix notation      | Polish notation |
|:-- |:------------------- |:--------------- |
| L1 | (ψ→φ)→((φ→χ)→(ψ→χ)) | `CCpqCCqrCpr`   |
| L2 | (¬ψ→ψ)→ψ            | `CCNppp`        |
| L3 | ψ→(¬ψ→φ)            | `CpCNpq`        |

from “[Łukasiewicz (L₁)-system](https://www.jstage.jst.go.jp/article/pjab1945/41/6/41_6_436/_pdf)”.

##### Contributions

Please create [an issue](https://github.com/xamidi/luk-pmproofs/issues) or [a pull request](https://github.com/xamidi/luk-pmproofs/pulls) in case you find a shorter proof.

##### Direct Links

- [L-pmproofs.txt](https://xamidi.github.io/luk-pmproofs/L-pmproofs.txt)
- [L-pmproofs-nowrap.txt](https://xamidi.github.io/luk-pmproofs/L-pmproofs-nowrap.txt)
- [L-pm.txt](https://xamidi.github.io/luk-pmproofs/L-pm.txt)
- [L-pm-compact.txt](https://xamidi.github.io/luk-pmproofs/L-pm-compact.txt)

##### Basics

L1–L3 are three axioms by Jan Łukasiewicz (which are also [tautologies](https://en.wikipedia.org/wiki/Tautology_%28logic%29)) from which every propositional theorem can be [derived](https://en.wikipedia.org/wiki/Formal_proof) using [modus ponens](https://en.wikipedia.org/wiki/Modus_ponens) and [substitution](https://en.wikipedia.org/wiki/Substitution_%28logic%29). The proof database focuses on 196 theorems, i.e. the ones named `*1.2 Taut`, `*1.3 Add`, …, `*5.75`, `Meredith's axiom`, `Peirce's axiom`, and `biass`. The last three of those are not actually from [Principia Mathematica](https://en.wikipedia.org/wiki/Principia_Mathematica) but were later added as part of the Metamath Solitaire project.

Sequences like `DD132` in the database are D-proofs. Rule D stands for [condensed detachment](https://en.wikipedia.org/wiki/Condensed_detachment), which is the only rule of inference used here. It combines modus ponens with most general [unification](https://en.wikipedia.org/wiki/Unification_%28computer_science%29). D-proofs can be parsed into Hilbert-style proofs with the tool [**pmGenerator**](https://github.com/xamidi/pmGenerator) based on L1–L3 (i.e. `CCpqCCqrCpr,CCNppp,CpCNpq` in *normal Polish notation*) like:

    pmGenerator -c -n -s CCpqCCqrCpr,CCNppp,CpCNpq --parse DD132 -u

The above command prints:

    [0] DD132:
        1. (¬0→0)→0  (2)
        2. 0→(¬0→0)  (3)
        3. (0→(¬0→0))→(((¬0→0)→0)→(0→0))  (1)
        4. ((¬0→0)→0)→(0→0)  (D):2,3
        5. 0→0  (D):1,4

Here, propositional variables in formulas are simply natural numbers, but you could rephrase this proof as:

|  |Proposition|Reason|
|:-|:-|:-|
|1.|(¬ψ→ψ)→ψ|L2|
|2.|ψ→(¬ψ→ψ)|L3|
|3.|(ψ→(¬ψ→ψ))→(((¬ψ→ψ)→ψ)→(ψ→ψ))|L1|
|4.|((¬ψ→ψ)→ψ)→(ψ→ψ)|(MP):2,3|
|5.|ψ→ψ|(MP):1,4|

In this formula-based representation, most of the proofs in the database grow very large. They will split to join common parts, which can be avoided by adding <code>&nbsp;-j -1</code> to the command mentioned above.
