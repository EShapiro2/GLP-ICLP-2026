# Proposal: Add `@<` lexicographic comparison guard to GLP paper

**Date:** 2026-05-18
**Audience:** Claude Chat working on `GLP-arXiv/sections/concurrent-glp.tex` and `GLP-ICLP-2026/sections/appendix-guards.tex`
**Status:** Draft for integration
**Runtime status:** Implemented and tested in `/Users/udi/Grassroots/GLP/` — all 481 REPL tests pass.

## Context

The CSSN GLP implementation now uses lexicographic comparison of ground constants to break the symmetry of simultaneous bilateral befriend attempts (see `CSSN/docs/cssn-glp-implementation-spec.md` §"Idempotent Befriend Commit with Smaller-Name Tie-Break").  The smaller-named participant of a friendship is canonical; this requires a guard that compares two atoms lexicographically.  GLP had only arithmetic comparison guards (`<`, `>`, `=<`, `>=`, `=:=`, `=\=`) plus structural equality (`=?=`); no term ordering.  We add one guard, `@<`, restricted to ground constants.

## Semantics

`X @< Y` is a three-valued guard:

- **Success**: both `X` and `Y` are bound to ground constants AND `X`'s name lexicographically precedes `Y`'s name.
- **Suspend**: either operand is an unbound reader.
- **Fail**: both bound and `X` does not precede `Y`, or either operand is bound to a non-constant (type error, parallel to the arithmetic guards' failure on non-numeric operands).

Success implies both arguments are ground.  Non-negatable, same rationale as the arithmetic comparisons (negation would conflate "not lex-smaller" with "type error").

The procedure signature is `procedure @<(Constant?, Constant?).` and lives in the root `programs/self.glp`.

## Edit 1 — `GLP-arXiv/sections/concurrent-glp.tex`

### Current text (lines 220–285 approximately)

Two changes inside this region.

(a) Line 220 lists groundness-implying guards:

> Groundness-implying guards include `ground`, `integer`, `number`, `string`, `constant`, arithmetic comparisons (`<`, `>`, `=<`, `>=`, `=:=`, `=\=`), and ground equality (`=?=`).

Insert `@<` after the arithmetic comparisons:

> Groundness-implying guards include `ground`, `integer`, `number`, `string`, `constant`, arithmetic comparisons (`<`, `>`, `=<`, `>=`, `=:=`, `=\=`), lexicographic comparison (`@<`), and ground equality (`=?=`).

(b) The "Arithmetic comparison guards" `\mypara` block at line 271 currently has six rows in its table.  Add a new `\mypara` block immediately after it, before "Time guards":

```latex
\mypara{Lexicographic comparison guard}
The lexicographic comparison guard compares two ground constants by name and succeeds when the first lexicographically precedes the second.  Success implies both arguments are ground constants; the guard fails on non-constant operands.  It is non-negatable, like the arithmetic comparisons.

\begin{center}
\begin{tabular}{ll}
\textbf{Guard} & \textbf{Signature} \\
\hline
\verb|@<| & \verb|procedure @<(Constant?, Constant?).| \\
\end{tabular}
\end{center}

\noindent The intended use is symmetry-breaking on participant identity, for example choosing a canonical channel when two agents attempt to establish a friendship concurrently.
```

## Edit 2 — `GLP-ICLP-2026/sections/appendix-guards.tex`

The ICLP camera-ready mirrors the arXiv version's guard table.  Two changes parallel to Edit 1.

(a) The main guard table (lines 23–42) — no change there; `@<` appears in the Arithmetic comparison block.

(b) Add a new `\mypara{Lexicographic comparison guard}` block immediately after the "Arithmetic comparison guards" block (after line 62), with the same text as Edit 1(b).

(c) Update the "Monotonicity and implications" paragraph at line 78 if it lists all groundness-implying guards — at present it does not enumerate them, so no change is required here.  Skip if already silent.

## What stays

Bibliography, lemma names, theorem statements, the surrounding prose about guard semantics, and the user-defined guard predicates section all stay as-is.  Only the two `\mypara` blocks are added.

## Questions for Claude Chat

If unclear, flag rather than guess:

1. Whether to retain "lex-smaller participant" or rephrase as "lex-smaller of the pair" in the closing sentence of the new `\mypara` block.
2. Whether the new block belongs immediately after "Arithmetic comparison guards" (as proposed) or as a subsection of "Equality and comparison" in a future restructure — defer the restructure if any.
