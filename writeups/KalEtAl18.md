# Neural-Guided Deductive Search for Real-Time Program Synthesis from Examples

Ashwin Kalyan, Abhishek Mohta, Oleksandr Polozov, Dhruv Batra, Prateek Jain, Sumit Gulwani. [Neural-Guided Deductive Search for Real-Time Program Synthesis from Examples](https://arxiv.org/pdf/1804.01186) ICLR 2018. 56 cites.

## Abs
Find programs from small numbers of input-output examples

## intro
- programming by examples:
    - symbolic (enumerative search) or statistical
- a priori predict usefulness of subproblems.
    - learn a model trained on *real world data* to predict a score for how good a branch will be
- branch and bound to speed up search
- Markovian search: *independent* suprograms

- use a dataset of search decisions. 
- learn separate models for different sub-problems (e.g. different depths or levels)

- in their empirical evaluation, they generate a dataset of 400k search decisions, and their algorithm produces programs on 68% using only one input-output example

- inductive program synthesis: find a set of programs that satisfy a specification and generalize well. MC similar strategy to NEAR.

- the search strategy (section 2, page 4):
    - deduce specs, recursively solve subproblems.

## synthesis algorithm
- N is a nonterminal symbol, defined through productions, and phi is a spec on N. brute force: select top k programs rooted at N, learn them, and then select a union of porgrams from there
- MC in classification task, we canot really cut out entire functions based on the input/output format
    - or can we? not based on input/output format, but based on if some functions dont give any helpful info at all?

- branch selection: bnb