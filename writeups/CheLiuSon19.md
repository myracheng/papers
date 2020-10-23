# EXECUTION-GUIDED NEURAL PROGRAM SYNTHESIS

Xinyun Chen, Chang Liu, Dawn Song. [Execution-Guided Neural Program Synthesis.](https://openreview.net/pdf?id=H1gfOiAqYm) ICLR 2019. 27 cites.


## abstract
use semantic information (basically what the program is actually doing at intermediate steps) to learn programs: execution guided synthesis, synthesizer ensemble.

## intro
state of the art is using encoder-decoder NN, and frame program synthesis as a sequence generation problem.
`execution guided synthesis` : sequence of manipulations (like transformations!). condition on intermediate states, so it can combined with a encoder-decoder neural synthesizer.

`synthesizer ensemble`: use semantic info to ensemble multiple synthesizers.

evaluate on Karel task, which is a publicly available benchmark for input-output program synthesis

## program synthesis
want consistency w/ input-output pairs. so encoder converts input-output examples into an embedding (e.g. for robutsfill, use LSTM since we are transforming strings; CNN for 2D grids). and then use decoder to generate programs.

^this uses syntax information, but not the semantics of the DSL. 

`program aliasing`: multiple semantically equivalent programs, but most r penalized as wrong programs QQ huh???
- one way of solving this issue is RL, so we reward all semantically corrrect programs

- what is the diff between semantics and syntax?   
    - semantics = meaning, syntax = set of rules

## execution guided synthesis
- figure 2: we have an understanding of the outcome after part of the program.
- extend the DSL L to include types of control flow: sequential, branching, looping
    - code block B is a sequence of statements or subcode blocks, if statements, while statements
- table 2: semantics rules for transitioning betewen programs B and B`. 
    QQ TODO come back to this and see why its necessary

initial and final states are simply two special states. so we can put any state-pairs into the synthesizer.

- sequential programs
    - take input: synthesizer, input-output pairs, and the ending token. iteratively generate a statement at a time. this transitions the synthesizer into a new state. that way we consider where the program already is, rather than the initial state.
- branching programs: if we have if statements
    - if we just naively do the algo 1, we have to synthesize the entire if statement before deriving intermediate states.
    - so we have algo 2: if the next predicted thing is an `if` token, first predict the condition, then diide the IO pairs based on the conditioning logic (like what ahinav was saying)
- looping programs: while
    - treat it as an if statement since `while C do B end ` is equivalent to `if C then (B; while C do B end) else ⊥ fi`

- we use this to improve the synthesizer QQ how exactly does this interact with the synthesizer?

## synthesizer ensemble
- we have many programs that satisfy the input ouput examples. then just combine them lol


## evaluation
- karel task: modify a 2d grid world, contains conditionals, loops, etc
- use the architecture of Bunel et al 2018. use their exec algorithm, as well as ensemblign 15 models
- breaking stuff up due to the if statement = breaking it up into small pieces

qq why does citadel care about this?