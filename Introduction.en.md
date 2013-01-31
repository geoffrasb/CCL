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

	# Grammar, not program example
	Program := [Fact] [Context]

A Program which describe a series of events, containing a set of Facts and a set of Contexts.
Facts are events or objects that the program want to describe. And within different Contexts,
Facts would be interpreted as rational or irrational.

● Examples:

	# positive example
	| the fact that an apple released by the branch and hit the ground |
	| the context that things not shored by someone would hit the ground |

	# negative example
	| an orange freed from my hands and fly away |
	| context that things without wings cannot fly |

There're two methods that could be applied on a program: `verify`, `rationalize`. 
`verify` is used for checking if there exists facts conflict within declared contexts, or if there exists 
any self-inconsistent context.
However, conflicting does not necessarily mean erroneous, it still can be interpret as other meanings.
We'll talk about this in the **Causality** section.
*rationalize will be described later*

● Description of operations:

	verify a program = verify all declared contexts,
                       verify all facts

Note that a program A may be included to another program B, then we call that A is a context included by B.
When a program becomes a context, those Facts will also be translated to Contexts.

- - -

### Fact

	# Grammar, not program example
	Fact :=
		| ConceptEntity
		| ConceptEntity & ConceptEntity
		| Fact => Fact						# => is left associative?

A Fact is a ConceptEntity, or a causality between Facts.
Facts can only be composed with `and'(`&`) operator, because they're only used to describe things that are really exist,
no possibility or uncertainty.

● Examples:

	| (Fact) person A's settings |
	| (Fact) person B's settings |
	| A laughs at B | => | B hits A | => | A is laughing harder |
	| (Context) a context in a classroom |

In this example, we may interpret that A and B are just being frolic, but not A has some mental problems.

● Description of operations:

	# not program example
	verify a fact = in cases that Fact is:
		| ConceptEntityX : 
            verify ConceptEntityX
		| ConceptEntityA & ConceptEntityB : 
            verify ConceptEntityA,
            verify ConceptEntityB
		| FactA => FactB :
            verify FactA,
            verify FactB

In the second case of the verification, not introducing conjunction is because the verification process does not
return a boolean value. Again, it just tell where exists inconsistence.

And in the third case of the verification, it only verify on those Facts. The result of the causality checking
could obtain from the process of verification on Contexts.
We'll talk more about `=>` later in **Causality** section.


- - -

### Context

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
