
	Program := [Fact] [Context]

	Fact :=
		| ConceptEntity
		| ConceptEntity & ConceptEntity
		| Fact => Fact						# => is left associative?
    Context :=
        | [CommonSense]
        | ContextIdentifier
        | ContextComposition
        | InContext { Context }
    InContext :=
        | in Context
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
        | ContextUnification -> [ContextModification]
    ContextUnification :=
        | Context is in Context
        | Context consist with Context
        | Context conflict with Context under x%
        | not ContextVerification
        | ContextUnification BoolOperator ContextUnification
    ContextModification :=
        | ContextIdentifier.Action
        | ContextComposition
