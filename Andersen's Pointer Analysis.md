- Andersen Analysis is a [[Flow-insensive]], [[Context-insensitve]] analysis.
	- Program order is not considered
- Also refer to as "inclusion-based" or "unification-based" points-to analysis, because it treat assign statement `p = q` as "the points-to set of `p` is a subset `q`'s points-to set'" 
- Models points-to as a list of set constraints, and use constraint solver to solve them

- Thus, an Andersen Analysis has 3 phases:
	- A constraint collection collect all of the constraints
	- An optimization optimize the constrain into equivalent constraints
	- A solver solve the constraints
