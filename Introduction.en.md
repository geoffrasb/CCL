# Introduction to The Causality Composing Language

## Background - why designing the language
## What does it provide

## examples

## semantics

Terms start with capital letters are grammar rules. Those with lower cases are literals.
Codes wrapped like `| this |` mean that it is a abstract description for those grammar rule who hasn't been described.
For example: `| this is comment |` is the actual code `# this is comment`'s abstract description.

- - -

### The Program

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

● Description of operations:

There're two methods that could be applied on a program: `verify`, `rationalize`. 
`verify` is used for checking if there exists any fact or context conflict with declared contexts.
However, conflicting does not necessarily mean erroneous, it still can be interpret as other meanings.
We'll talk about this in the **Causality** section.
*rationalize will be described later*

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

    # CE is short for ConceptEntity
	|(CE) person A's settings |
	|(CE) person B's settings |
	|(CE) A laughs at B | => |(CE) B hits A | => |(CE) A is laughing harder |
	|(Context) a context in a classroom |

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

And in the third case of the verification, it only verify on those Facts. The result of the causality checking could
obtain from the process of verification on Contexts.
We'll talk more about `=>` later in **Causality** section.


- - -

### Context

    # Grammar, not program example
    Context :=
        | [CommonSense]
        | ContextIdentifier
        | ContextComposition
        | InContext { Context }
    InContext :=
        | in Context
        | ""

A context, in this language, is a set of common-sense rules in the environment where we recognize concepts. We would
interpret a phenomena into different meanings because of the existence of different contexts in the environment. For
example, flying metals makes no sense in the context everyday-life, but may make sense in the context - an eletrical
experiment.

A ContextIdentifier is a variable, assigned at somewhere, or loaded context (As mentioned previously, a program may be
loaded into another program and becomes a context.). And an InContext denote that the declared common-sense rules in the
curly brackets are in the scope of some contexts.

Despite we could load many contexts into a program, how are those rules belong to each context exist simultaneously,
especially when two rules conflict with each other?
ContextComposition will take the job. It'll be detaily described in the next section.

● Example:

    |(CE) a piece of metal released from my hands| => |(CE) the meta flies away|
    MyExperiment = Physics > Experiment
    in MyExperiment {
        |(CommonSense) a metal bears forces in a magnetic field |
        |(CommonSense) things bearing forces may move |
    }

In the example, `>` is a context-composition operator, which means `Physics` has higher priority than `Experiment`. If
there exists conflict rules, we preserve one in `Physics`.

Since there's no more words on how I hold the piece of meta or how the meta flies, verifying this code will still obtain
the result that no conflict happens. But what if I add this fact:

    |(CE) I'm standing outside the magnetic field of the experiment |

The verification may still not alarm for any conflict, because maybe I'm holding the metal via a machine, which
should be operated outside the magnetic field. If the fact really, truely violate some common-sense rules, then
inconsistency shall be warned. Again, the violation still has its value. It'll be described in **Causality** section, as
I mentioned.

● Description of operations:

We can apply not only `verify` on a context, but also `compose`, which will be introduced detaily in the next section.

    # not program example
    verify a context = in cases of the context:
        | [CommonSense] :
            verify each CommonSense
        | ContextIdentifier :
            verify the loaded context
        | ContextComposition :
            verify (compose ContextComposition)
        | InContext { Context }
            verify (InContext > Context)        # also a context-composition

- - -

### ContextComposition

    ContextComposition :=
        | ...

- - -

### CommonSense

    CommonSense :=
        | ConceptEntity
        | Causality
        | no CommonSense

Common-senses are the core of the language. ConceptEntities could represent actions, things that are concrete or
abstract, or anything that can be form as an object,or entity. For example, Human beings. we have a common-sense that a
normal adult may has height in a range, say 160~210cm. When seeing someone is only 120cm high, we find this is uncommon,
and coin the word "Dwarfism". For other examples: "John loves David", actually contains three ConceptEntities in
"normal" context: "John" and "David" are names for male, and a man loves another man is fine nowadays, but may not in
the past; "There's a belief that a fallen grape is still edible if picked up in 3 seconds." is about "belief" -- an
abstract concept. If the belief has no physical or psychological support, we may say it uncommon, unreasonable.

A Causality is a common-sense telling about "something cause something".

- - -

    ConceptEntity :=
        | ...
    Causality :=
        | ContextMatching       -> [ContextModification]
        | [ContextModification] <- ContextMatching
    ContextMatching :=
        | Context is in Context
        | Context consist with Context
        | Context conflict with Context under x%
        | not ContextMatching
        | ContextMatching BoolOperator ContextMatching
    ContextModification :=
        | ContextIdentifier.Action
        | add Context to current context
    
## syntax

## problems

* context circular containing

## proof
