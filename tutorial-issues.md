# Tutorial Issues (PartI)

Notes accumulated while going through `../site/src/documentation/tutorial/PartI/` and solving exercises in `../tutorial-code/PartI/`.
Each entry: chapter, location, what's wrong / outdated / confusing, suggested fix.

Issues that are quickly fixable in the tutorial-code repo are committed there directly. The ones logged here are deficiencies that either:
- need broader discussion (so I just note them without changing tutorial code),
- are spots where Arend tactics (`linarith`, `simplify`, `ext`, …) would make a clunky proof much nicer,
- or live in textual content that I should leave for the maintainers.

---

## ProofsEx exercise 12 — `or-assoc` requires 8 enumerated cases

Because `or` is defined with `\elim a, b` (not `\elim a` then nested `\elim b`), Arend won't fire clause `| true, _ => true` when the second arg is a free variable. So the obvious 4-case split with `_` patterns gets `Expressions are not equal: true or y or z vs true or (y or z)`. The full 2x2x2 enumeration works. A tactic like `cases (x, y, z)` would let students write the proof in a single line; without it, the bookkeeping is unpleasant. Worth mentioning in the chapter, or providing a `\func or` defined by `\elim a` only. (Left unchanged: the chapter deliberately uses `\elim a, b` to demonstrate multi-arg pattern matching.)

## UniversesEx exercise 4 — `filter`-correctness needs ~70 lines of manual `\case` plumbing

The "any sublist that satisfies `p` is a sublist of `filter p xs`" direction (`filter-maximal`) requires repeatedly case-splitting `\case p x \as b, idp : p x = b \return ... \with`-style on every clause that touches `filter p (cons x xs)`. With a `cases (p x \with ...)` or `mcases` tactic the proof shrinks by ~3x. Worth flagging as a tutorial-tactics opportunity once tactics land in the curriculum. (Half-measure applied: a note in the exercise file flags maximality as optional / advanced.)
