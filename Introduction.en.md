# Introduction to The Causality Composing Language

## Background - why designing the language
## What does it provide

## examples

## semantics

Terms start with capital letters are grammar rules. Those with lower cases are literals.
Codes wrapped like `| this |` mean that it is a abstract description for those grammar rule who hasn't been described.
For example: `| this is comment |` is the actual code `# this is comment`'s abstract description.

- - -

### Program

    # Grammar
    Program := [Fact] [Context]

A Program which describe a series of events, containing a set of Facts and a set of Contexts.
Facts are events or objects that the program want to describe. And within different Contexts,
Facts would be interpreted as rational or irrational.

- Examples:

    | the fact that an apple released by the branch and hit the ground |
    | the context that things not shored by someone would hit the ground |

    | an orange freed from my hands and fly away |
    | context that things without wings cannot fly |

There're two methods that could be applied on a program: `verify`, `rationalize`. 
`verify` is used for checking if there exists facts conflict within declared contexts, or any inconsistent context.
Of course, conflicting does not necessarily mean erroneous, we'll talk about this below.
*rationalize will be described later*

- Description of operations:

    verify a program = verify the consistency of the program (context)

Note that a program A may be included to another program B, then we call that A is a context included by B.
When a program becomes a context, those Facts will also be translated to Contexts.

- - -

### Fact

    # Grammar
    Fact :=
        | ConceptEntity
        | ConceptEntity & ConceptEntity
        | Fact => Fact

A Fact is a ConceptEntity, or a causality between Facts.
Facts can only be composed with `and'(`&`) operator, because they're only used to describe things that are really exist,
no possibility or uncertainty.

- Examples:

    | (Fact) person A's settings |
    | (Fact) person B's settings |
    | A laughs at B | => | B hits A | => | A is laughing harder |
    | (Context) a context in a classroom |

In this example, we may interpret that A and B are just being frolic, but not maybe A has some strange mental problem.

- Description of operations:

    verify a Fact = verify if the Fact is consistent in the context(the whole program including Facts and Contexts), 
                    which means the Fact doesn't violate any rule in the context.

We'll talk more about `=>` later in Causality section.

- - -

## Context

    # Grammar
    Context :=
        | InContext { Context }
        | ContextIdentifier
        | ContextComposition
        | CommonSense
    InContext :=
        | with Context
        | ""
    ContextComposition :=
        | ...


    CommonSense :=
        | ConceptEntity
        | Causality
        | no CommonSense
    ConceptEntity :=
        | ...
    ContextIdentifier :=
        | ...
    Causality :=
        | ContextUnification -> ContextModification
    ContextMatching :=
        | Context is in Context
        | Context consist with Context
        | Context conflict with Context under x%
        | not ContextVerification
        | ContextVerification BoolOperator ContextVerification
    ContextModification :=
        | ContextIdentifier.Action
        | add Context to current context
        | ContextModification, ContextModification
    
## syntax

## problems

* context circular containing

## proof
