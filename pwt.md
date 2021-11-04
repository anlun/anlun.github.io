---
layout: none
title: Artifact 56 for Evaluation for POPL'22
---

# Artifact 56 for Evaluation for POPL'22

There are two artifacts for this work, the Coq formalization and the tool PwTer. Each is described in turn.

#### Quick links
- Browse the development at GitHub: [online](https://github.com/weakmemory/pwt)
- Browse the PwTer source code at GitHub: [online](https://github.com/graymalkin/pomsets-with-predicate-transformers)
- VirtualBox image: [online](https://podkopaev.net/popl22-pwt-artifact.html)


## Pomsets w/ Transformers (a Coq formalization)

This artifact contains Coq code supplementing the paper _Leaky Semicolon: Compositional Semantic Dependencies for Relaxed-Memory Concurrency_ by 
Alan Jeffrey, James Riely, Mark Batty, Simon Cooksey, Ilya Kaysin, and Anton Podkopaev.


### Getting started
The artifact consists of Coq formalization and proofs about _Pomsets w/ Transformers_.
There are two ways to evaluate the artifact:
- by using a virtual machine (VM) prepared by us;
- by using your own Coq setup via `opam`.
Below, we provide guidance for both approaches.
*We propose to start with building the project by following our instructions and then take a look at the main definitions and lemmas.*

### Using the Virtual Machine 
You need to get a [VirtualBox](https://www.virtualbox.org/) (tested w/ version 6.1.26) on your system and import the VM
`pwt.ova`. Please, note the following:
- The VM should be provided with at least 8GB of RAM.
- The VM is better to be provided with 4 CPUs (but 2 CPUs should be enough).
- The VM is a Ubuntu 18.04 with `coq`, `coqide`, `vim` and `emacs` being set-up.
- Username and password are both `vagrant`.

The Coq code can be found in the folder `/home/vagrant/artifact`. To compile it,
you need to run `cd /home/vagrant/artifact && make -j4` in a terminal.
The same but pre-compiled code is located in the folder `/home/vagrant/artifact_compiled`.

There is a CoqIDE shortcut on the desktop, which could be used to explore the development.

### Using your own Coq setup with opam
All required dependencies can be installed via package manager [`opam` (version >= 2.0)](https://opam.ocaml.org/)
by running `./configure` from the project's root folder.
It installs:
- [Coq 8.13](https://coq.inria.fr)
- [Hahn library](https://github.com/vafeiadis/hahn) (`coq-hahn`)
- [Intermediate Memory Model](https://github.com/weakmemory/imm) (`coq-imm.1.4`)

The compilation and installation of `coq-imm.1.4` may take a lot of time (> 40 min).

After that, you may build the project by running `make -j4` from the project's root folder.

## Checking the artifact's code
After the project is compiled, you may want to check how the main definitions and results in Coq are related to the ones in the paper.

| Paper                                  | Description                                              | Coq file            | Coq statements                                                     |
| ---                                    | ---                                                      | ---                 | ---                                                                |
| §4.1                                   | definitions of statements _S_ and expressions _M_        | `Language.v`        | `Expr.t` and `Stmt.t`                                              |
| §4.3, Def. 4.2                         | a definition of predicate transformers                   | `PredTransformer.v` | `Record predTransformer`                                           |
| §4.3, Def. 4.4; §A.3, Def. A.2 | a definition of pomsets with predicate transformers; a definition of complete pomsets | `Pomset.v`          | `Record pomset`, `Record wf` <br /> (well-formedness predicate), and `Record complete` |
| §4.3, Fig. 1 and <br /> §9.4, Def. 9.6 | the PwT semantics extended to allow if-closure           | `Semantics.v`       | `Inductive Semantics`                                              |
| ---                                    | ---                                                      | ---                 | ---                                                                |
| §4.3, Lemma 4.5a                       | `skip` as an identity element for the semicolon operator | `SeqSkipId.v`       | lemmas  `skip_seq_id_left` <br /> and `skip_seq_id_right`          |
| §4.3, Lemma 4.5b                       | associativity of the semicolon operator                  | `SeqAssoc.v`        | lemma `seq_assoc`                                                  |
| §4.3, Lemma 4.6e                       | distribution of the if operator over semicolon           | `IfClosure.v`       | lemma `if_closure`                                                 |

Our proofs of the main lemmas use the following axioms (and no other assumptions):
- Excluded middle, XM (`classic` from `Coq.Logic.Classical_Prop`);
- (Dependent) Functional Extensionality, (D)FE (`functional_extensionality_dep` from `Coq.Logic.FunctionalExtensionality`);
- Constructive Definite Description, CDD (`constructive_definite_description` from `Coq.Logic.Description`).

You may check that by taking a look at files
- `skip_seq_id_left.axioms.out`, `skip_seq_id_right.axioms.out`, `seq_assoc.axioms.out`, and `if_closure.axioms.out`.

They are generated during the project compilation by `Print Assumptions` instructions at the end of `SeqSkipId.v`, `SeqAssoc.v`, and `IfClosure.v` files.

To check that the project does not contain admitted facts, you may want to run the following script from the project's root folder:

``` bash
grep dmit src/*.v

```

### Description of the project's files

#### Basic definitions of the semantics
- `Events.v` – a definition of events (§4.1)
- `Language.v` – definitions of statements _S_ and expressions _M_ (§4.1)
- `Formula.v` – a language of formulas Φ (§4.1)
- `Action.v` — a definition of actions and related notions (§4.2)
- `PredTransformer.v` — a definition of predicate transformers (§4.3, Def. 4.2)
- `Pomset.v` — a definition of pomsets with predicate transformers (§4.3, Def. 4.4)
- `Semantics.v` — the PwT semantics extended to allow if-closure (§4.3, Fig. 1 and §9.4, Def. 9.6)

#### Properties of the semantics
- `SeqSkipId.v` — `skip` as an identity element for the semicolon operator (§4.3, Lemma 4.5a)
- `SeqAssoc.v` — associativity of the semicolon operator (§4.3, Lemma 4.5b)
- `IfClosure.v` — distribution of the if operator over semicolon (§4.3, Lemma 4.6e)

#### Auxiliary definitions and lemmas
- `AuxDef.v`, `AuxRel.v`, `SeqBuilder.v`


## PwTer

PwTer can be found on the desktop of the virtual machine described above, by following the `PwTer` shortcut on the
desktop. 

Alternatively, it can be built on your own machine by following the instructions in [the
project](https://github.com/graymalkin/pomsets-with-predicate-transformers)'s README. 

Once the tool is built, to replicate the results presented in the paper, navigate to the `data` directory of the PwTer
sources and run `make check`. This will evaluate the Java Causality Test Cases.

### Tool structure

Most of the source is boiler plate to tie together parsers, the two interesting files are:

 - `src/Preliminaries.ml` contains the interface to Z3
 - `src/PomsetPTSeq.ml` implements the semantics as presented in Figure 1, with register recycling. The paper's rules are referenced in comments like `(* M6 *)` and `(* R4a *)`.

The tool has been written to be faithful to the mathematics without too much deviation for efficiency's sake. The
majority of the complexity is in the implementation of `seq_rule` and `if_rule`, as these have to implement merging. In
PwTer, all events have globally unique identifiers, so possible valid merges have to be calculated at these compositions
and new labellings must be produced. This yields quite a lot of fiddly maps which have to be applied carefully to
preserve the semantics.
