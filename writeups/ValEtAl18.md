# HOUDINI: Lifelong Learning as Program Synthesis

Lazar Valkov, Dipak Chaudhari, Akash Srivastava, Charles Sutton, Swarat Chaudhuri. [HOUDINI: Lifelong Learning as Program Synthesis](https://arxiv.org/pdf/1804.00218.pdf) NIPS 2018. 22 cites.

## abstract
- in lifelong learning, we want to reuse high-level concepts and learn complex procedures, namely mixing perception + algorithmic tasks. 
- this paper presents a framework that uses gradient descent + combinatorial search. It represents NNs as diffable functional programs that contain a library of neural functions. It has two parts: 1) create program by searching over programs, functions, and architectures 2) program trainer using SGD. 
    - enables transfering high level modules due to modularity of these fxal programs
- This was evaluated on tasks that combine perception with algorithmic tasks. 

## terms
- *combinatorial search* : constraint satisfaction problem, find an assignemnt for each variable that satisfies constraints. b^n possible assignments (e.g. graph coloring). solved by, for example, a* or branch-and-bound
- *differentiable programming language* : have diffable parameters, so we can learn parameters using gradients. e.g. pytorch. They allow transfering knowledge across different tasks due to the modularity of the language, in particular *high level transfer* of more abstract levels of the network, rather than just layers of it. QQ what types of abstractions are these?
    - A: e.g. count_digit is learned for counting a certain type of digit, and then the synthesizer uses it for another type of digit.
- *lifelong learning* : just long-term learning? every round is based on prev round 
    - sequence of individual learning tasks, including object reocgnition, counting, etc
    - challenges: catastrophic forgetting (later tasks overwrite learning fro mearlier tasks), negative transfer (info from earlier tasks hurts later tasks).
    - we mitigate these challenges by using a library, where we can selectively reuse the earlier parts that are good
- *ADT* abstract data types: lists or graphs of tensor types (TTs ha ha)

## intro
- how do we infer the structure of a diffable program?
    - gaunt et al [14], which describes approach of having a library of trainable NNs as subroutines, require hand written templates
    - use symbolic search algorithms
- represent programs in *typed functional language*: can describe many common neural architectures, and help prune bad programs
    - e.g. `fold` for RNNs, convlns
- neurosymbolic learning framework: search over space of strongly typed functional programs, and then tune parameters using SGD
- experiments: compute least-cost path in grid, discovers Bellman-Ford with a neural function to approximate the relaxation step. 

### program synthesis
-  functional representations, type-based pruning accelerate search

## HOUDINI programming lang
1. functional language (containing ?) diffable programs
2. learning procedure: symbolic module + neural module

- compose together functions
    - functions are neural networks from a library. (so diffable)
    - `map` a list, `fold`, `conv`
- higher-order combinators to represent neural architectures
- type discipline

## learning algo
given: types of the training instances, and of the target function. 
- symbolic module `gen`: repeatedly proposes parameterized programs using:
    - top down: generate partial programs, evaluate short programs first (performs better experimentally)
    - evolutionary algo QQ todo 
    - use type safety to cut down on program space
- gradient-based opt `tune`

- for lifelong learning, repeatedly add to the library. and freeze the previous functions, so that forgetting is not possible. *selective transfer*: decide whether to use info in the next iteration

## eval
- compare to networks that dont do transfer learning, networks that transfer all weights, and approach that has pools of pretrained networks
- for CS1 task (low level transfer), Houdini picks the correct modules to use.

## QQ
- these concepts make sense, but I dont get how this is actually done. Like since Houdini *is a programming language* how is it implemented? 
- how are types assigned? this limits it to tasks that can be assigned to these specific tasks.