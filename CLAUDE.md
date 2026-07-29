# GLP-ICLP — Instructions for Claude

Read `/Grassroots/claude.md` first, and the writing style guide it names.  The root file carries everything that applies to every project: writing style, the bib protocol, the git and Overleaf workflow, discussion mode, the working protocol, and the content policy.  This file adds only what is specific to this paper.

## Start of every conversation

1. Read this file.
2. Read the code-ownership map (below) in full.
3. State that you have done so, and wait for direction.  Do nothing else.

## What this is

The paper "GLP: A Grassroots, Multiagent, Concurrent, Logic Programming Language for AI", by Ehud Shapiro, for ICLP 2026, typeset with the EPTCS class.

- **Working directory:** `/Users/udi/Grassroots/GLP-Definitive-Spec`.  The git remote is `EShapiro2/GLP-ICLP-2026` — the directory and the repository have different names.
- **Main file:** `main-GLP-ICLP-2026.tex`.
- **Bibliography:** `\bibliographystyle{eptcs}`, `\bibliography{bib}`.  `bib.bib` is imported from Bib-Grassroots in Overleaf; never edit it, and never read it.  The protocol is in the root file.

## Code ownership

This project is **GLP-ICLP**.  Ownership and authority are not restated here — they live in the map, `/Grassroots/docs/glp-paper-code-map.md`, the single source of truth.  Read the map in full at session start.  Implementation decisions go in this paper's arXiv "Implementation Notes" appendix, not a separate spec document.

GLP-ICLP is the language authority.  The guard, body-kernel and system-predicate tables in `sections/appendix-guards.tex` are the language definition that the other projects cite, so those projects send requests for rows in them; TGLP owns the type and module system, IGLP the runtime and kernels, Secure-GLP the attestation and signature layer.

## Sections

Body, in the order the main file inputs them:

| File | Content |
|---|---|
| `introduction.tex` | Introduction |
| `glp.tex` | GLP: syntax, operational semantics, guards, programming techniques |
| `maglp.tex` | Multiagent transition systems, maGLP, safety properties |
| `social-graph.tex` | The grassroots social graph |
| `grassroots.tex` | maGLP is grassroots |
| `conclusion.tex` | Conclusion |

Appendices, in input order: `appendix-lp.tex`, `appendix-term-matching.tex`, `appendix-grassroots-defs.tex`, `appendix-guards.tex`, `appendix-proofs.tex`, `appendix-social-graph-walkthrough.tex`.

## The appendix build flag

The main file defines `\ifappendix`.  `\appendixfalse` is the ICLP submission build, which omits the appendices; `\appendixtrue` is the arXiv full version, whose title gets " (Full Version)" appended by hand, since EPTCS extracts `\title` verbatim into the arXiv metadata and it must stay literal.

Appendix material is referenced with `\appref{label}{fallback}`, which renders as an appendix reference in the arXiv build and as the fallback — normally `\arxivref` — in the submission build.  Never reference appendix material with a bare `\ref`: it breaks the submission build.

## LaTeX commands defined in this paper

`\mypara{Name}` paragraph header; `\temph{text}` for a defined term inside a definition, `\emph` everywhere else; `\Program{title}` program-listing header; `\appref` and `\arxivref` as above; `\udi{...}` blue author comment and `\claude{...}` red editor comment; `\remove{...}`, which drops its argument; `\ia` through `\iv` for roman numerals.

## Project-specific rules

- **No code appendix.**  Appendices carry no listings, no code figures, no type-definition blocks — only pointers to the public GLP repository.  The reference tables in `appendix-guards.tex` stay.  (Standing decision, Udi, 2026-07-02.)
- **Paper editing belongs to the chat session.**  Claude Code does not edit `.tex` files in this repo; it runs and tests GLP code, and does git.
- **Never use boxed questions** (the AskUserQuestion tool).  Free text only.
- **Never use the word "pattern"** except in the technical sense of pattern-matching.
- **Commit and push at the end of a task.**  In Cowork, that means giving Udi the one-liner; the network is his.

## docs/

`docs/` holds notes that predate the paper's appendices: `body-kernels-reference.md`, `guards-reference.md`, `naming-conventions.md`, `glp-predicate-taxonomy.md`, `glp-cheat-sheet.md`, `mutual-ref-spec.md`.  They restate what `sections/appendix-guards.tex` now defines, and they are not updated when it changes.  The appendix is authoritative; treat these as background only.

## Related repositories

- `/Users/udi/Grassroots/GLP` — the implementation and the GLP programs the paper points to.
- `/Users/udi/Grassroots/TGLP` — the type system and the module system.
- `/Users/udi/Grassroots/IGLP` — the implementation paper: dGLP, madGLP, kernels, networking seam.
- `/Users/udi/Grassroots/Secure-GLP` — mutual attestation, signatures.

## #remember

When Udi says `#remember <something>`, add it to this file.
