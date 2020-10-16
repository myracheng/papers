# Learning Syntactic Program Transformations from Examples

Reudismam Rolim, Gustavo Soares, Loris D’Antoni, Oleksandr Polozov, Sumit Gulwani, Rohit Gheyi∗,Ryo Suzukik, Björn Hartmann. [Learning Syntactic Program Transformations from Examples.](http://pages.cs.wisc.edu/~loris/papers/icse17.pdf) ICSE 2017. 100 cites.

## Technique 
- DSL for program transformations
    - tree edit operators (insert, delete, update), list processing operators (filter, map), and pattern matching
    - define transformation: list of rewrite rules, where each rule is an operation applied to a set of locations. the locations are chosen by doing pattern matching.
        - each rule is a replacement of some node with a new node. location expression (`Filter` + `match`)
            - pattern-matching: compare context of a node against a pattern. pattern is combo of concrete +abstract tokens (abstract only matches the kind, e.g. `if statement`)
            - does some sort of operation: insert, delete, update, prepend this
- backpropagation with witness functions
    - `filter` is a witness function.
    - backprop for `Transformation` operator: given examples of edits, find constraints on the rules. so basically given input and output program, find individual edits (use tree edit distance algorithm). then, partition those edits into clusters, and then build a set of operation examples

## MC
- It doesnt really make sense to do NEAR on this DSL. We have created a language for these transformations. but we dont have a way to approximate them thats better than just replacing the whole location with a neural network. 
- can we use an AST representation for CRIM 13? but we dont have good examples