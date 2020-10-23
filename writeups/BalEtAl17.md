# DeepCoder: Learning to Write Programs

Matej Balog, Alexander L. Gaunt, Marc Brockschmidt, Sebastian Nowozin, Daniel Tarlow. [DeepCoder: Learning to Write Programs.](https://arxiv.org/pdf/1611.01989.pdf) ICLR 2017. 290 cites.


## abstract
learn from input-output examples using deep learning
train NN to predict properties of program, then use NN to augnment search techniques

differentiable program induction (use gradient descent, each synthesis problem is solved independently) is worse than discrete search-based techniques.

1) learn to induce pograms
2) integrate NN with search, rather than replacing them
    - specifically, predict an order on the program space, use it to guide search-based techniques. so search becomes a supervised learning problem. also, if NN fails, its ok cuz were not relying on a single prediction. and we leverage existing best solvers

they define a programming language that is expressive enoguh to include real world programming problems, but high-level to be predictable

they provide models for mapping sets of examples to program properties

## background on inductive program synthesis
IPS: given input-output, produce program that does this. two problems:
1) search problem: search over set of possible programs
2) ranking: if many good programs, which one do we return

- DSLs: choice of DSL can allow more efficient search, and difficulity of ranking
-search techniques: 
    - brute force e.g. enumerate all derivations of grammar. 
    - Satisfiability modulo theories: use theories (constraints) like inequalities. convert a DSL into constraints between variables, and then call an SMT solver. good when we have `special purpose reasoning` (TODO what is that QQ), but not helpful when DSL is complex cuz then we have very large constraint problem
    - stochastic local search, genetic algorithms

## LIPS!
- DSL choice: must be expressive enough to capture the problems that we want to solve.
- `attribute function` maps programs of DSL to attribute vectors a. machine learning model predicits distribution q(a | eps), eps is input-output examples. then we search over programs ordered by q(A(P) | eps). so attributes are useful if we can predict them from eps, and if it reduces the size of the search space.
    - example of attributes: presence or absence of high level functions, control flow templates
    
next, data generation: generate a dataset of programs, their attributes, and eps. (MC we could do this using NEAR). generate millions of programs!

3) ML model: learn distribution of attribues, q(a| eps). 
    - e.g. if attributes are a fixed size binary vector, then we can use NN with independent sigmoid outputs. if variable size, then RNN output makes more sence

4) search: use q(a|eps) to guide search

## DEEPCODER: their version of LIPS
1) binary attribute: presnece of highlvl functions in target program. 
define DSL based on query lagnagues (use functions in sequence to manipulate data). program is a sequence of function calls, so each call initializes a variable. then these functions can be applied to any of the inputs.
only linear control flow (QQ TODO what is example of nonlinear?)

2) data generation: to genreate valid inputs, enforce constraint on the output value to bound integers, propagate backward so that the input values are valid. QQ wait so is this input output pairs? yea for eps for each program

3) ML model
aim to recognize patterns in input-output examples, and predict the presence or absence of functions.
netowrk has *encoder* (diffable mapping from input-output examples to a vector) and *decoder* (map from vector to predictions of attributes)
    QQ why use encoder and decoder? why not just a classifier? todo think abt

4) search
how ML model guides the search:
- DFS: use DFS to search over programs. when search rocedure extends a partial program by a new function, it tries the functions in ordre based on the neural net. so basically this distribution is the heuristic of what functions to try.
- sort and add: maintain set of active functions, perform DFS only there. if it fails, we add a new fn based on the NN
- sketch: fill in holes in incomplete source code. 
- \lambda^2 : enum search. also use sort and add

loss function: cross entropy, so that predictions are marginal probabilities. DeepCoder loses ? by ignoring correlations b/w functions.

we can upper bound the tutal run time by a quantitay that is minimized by adding the functions in the order of their probabilities (Lemma 1)

## Experiments
todo