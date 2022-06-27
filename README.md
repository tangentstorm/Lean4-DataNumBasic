# Lean4-DataNumBasic
project to improve [mathport](https://github.com/leanprover-community/mathport)'s lean4 translation for [Mathlib/Data/Num/Basic](https://github.com/leanprover-community/mathlib3port/blob/master/Mathbin/Data/Num/Basic.lean)

## Context

Lean is dependently typed programming language and proof assistant.

Mathlib is a collection of definitions and formal proofs for general mathematical use, implemented in Lean 3.

Lean 4 is a rewrite of Lean in Lean, with various breaking changes.

Mathport is a tool to automatically transpile Mathlib from Lean 3 to Lean 4.

`Data.Num.Basic` is a file inside Mathlib that defines and implements integer arithmetic as strings of binary digits. (It's like Peano's axioms for the natural numbers, but using binary digits instead of unary, and extended to all the integers.)

## Problems to Solve

Mathport is a work in progress, and the current translation of this particular file does not yet compile in lean 4. (This is currently true for most of Mathlib. I am focusing on this one because it's small, self-contained, and concerns elementary mathematics that I can understand.)

### small / hopefully easy changes

I attempted a manual cleanup of the file, and identified [several small changes](https://github.com/tangentstorm/tangentlabs/commits/master/lean4/Bin/Lean4DataNumBasic.lean) that I expect to be easy to fix:

- [add the mathlib import](https://github.com/tangentstorm/tangentlabs/commit/42718f20803fb540a241b77990b9411943c4fa60), since some of the dependencies are no longer part of lean itself.
- [fix capitalization on some constructors](https://github.com/tangentstorm/tangentlabs/commit/cf81131f36c5a697cb0cf2c46ad22f9bb0d38f07) (`pos` gets capitalized sometimes, for some reason)
- [fix local names for recursive protected functions](https://github.com/tangentstorm/tangentlabs/commit/934d047d35e03b26f8e3ef4dd817a8f5c58eb085) (the `protected` keyword seems to have changed a bit)
- [add motive functions for `casesOn`](https://github.com/tangentstorm/tangentlabs/commit/8cc8ee689a97c1b6f74fa9cc123432d71eee95dc) (a function that dispatches on the constructor for enumerated types takes a new initial parameter)
- a couple other small changes along these lines

### larger problems

- implement dsimp' (proof tactic. probably the hardest problem given my level of knowledge)
- castPosNum :: bit0 needs to be on the α type, and I don't think bit0 is part of lean4? (probably need to learn more about lean4 here (???))
- in general, the generic coercion stuff seems to need a revamp ( `CoeTₓ` -- probably just more to learn here)
- lack of coercion is breaking the repr implementation (probably easy once coercion works)
- replacement for `Nat.binaryRec` (probably easy)
- re-enable `@deriving has_reflect` (antiquotations for terms. probably needs to be implemented in lean4)

