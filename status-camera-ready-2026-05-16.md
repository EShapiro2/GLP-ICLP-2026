# GLP-ICLP-2026 Camera-Ready — Status Report

**Date:** 2026-05-16
**Repo:** `/Users/udi/Grassroots/GLP-ICLP-2026/`
**Latest commit:** `9df5a1b` — "Move Grassroots Social Graph to its own §4..."
**All changes pushed to `origin/main`.**

---

## Conference & Deadline

- **Venue:** ICLP 2026
- **Page limit:** 12pp (EPTCS format)
- **Camera-ready due:** 2026-05-30 (~2 weeks out)
- **Build flag:** `\appendixfalse` for ICLP submission; `\appendixtrue` for arXiv. `\arxivref` macro renders as `the full paper~\cite{shapiro2025glp}` in the ICLP build.
- **Companion arXiv paper:** `shapiro2025glp` (full version with all proofs and the complete social-graph program).

---

## Paper Structure (Current Build)

The paper has six sections after the recent restructure. The Social Graph is now §4, lifted out of §3 (maGLP) so that §3 focuses on the language semantics and §4 presents the example platform.

| § | Title | File | Key contents |
|---|---|---|---|
| 1 | Introduction | `sections/introduction.tex` | 6 \mypara blocks: **Grassroots**, **Grassroots Logic Programs**, **Semantics**, **Historical Context**, **AI**, **Paper outline** |
| 2 | GLP | `sections/glp.tex` | §2.1 Syntax · §2.2 Operational Semantics (cGLP transition system) · §2.3 Guards · §2.4 GLP Programming Techniques |
| 3 | Multiagent GLP | `sections/maglp.tex` | §3.1 Multiagent Transition Systems · §3.2 From cGLP to maGLP (merged subsection covering the maGLP definition) · §3.3 Safety Properties of maGLP |
| 4 | The Grassroots Social Graph | `sections/social-graph.tex` | Channels · Cold-call befriending (init clause + recipient clause + user-decision clause + `bind_response` narration) · Friend-mediated introduction · Text messaging · Boot and deployment · closing grassroots-claim forward-pointer to `corollary:social-graph-grassroots` |
| 5 | Multiagent GLP is Grassroots | `sections/grassroots.tex` | Theorem `theorem:maGLP-grassroots` · Definition "GLP Application" · Proposition `prop:app-grassroots` · Corollary `corollary:social-graph-grassroots` |
| 6 | Conclusion | `sections/conclusion.tex` | Hyper-programmer thesis (¶1 expanded with concurrent-semantics specifics: suspend/commit/communicate, safety/fairness/deadlock-freedom reasoning) + closing ¶ on Constitutional governance / textbook / open-source URL |

### `\input` order (`main_GLP_ICLP_2026.tex`)

```
\input{sections/introduction}
\input{sections/glp}
\input{sections/maglp}
\input{sections/social-graph}
\input{sections/grassroots}
\input{sections/conclusion}
```

Appendices (conditional on `\appendixtrue`):

```
\input{sections/appendix-lp}
\input{sections/appendix-term-matching}
\input{sections/appendix-grassroots-defs}
\input{sections/appendix-proofs}
\input{sections/appendix-guards}
\input{sections/appendix-additional-techniques}
\input{sections/appendix-social-graph-walkthrough}
\input{sections/appendix-social-graph-complete}
```

### Files on disk but **not** in build

None. `sections/related-work.tex` and `sections/platforms.tex` have been deleted (2026-05-16); their content was either folded into the intro `\mypara{Historical Context}` (related-work) or no longer needed (platforms). Recoverable from git history if ever required.

---

## Key Labels (Cross-Reference Map)

| Label | Refers to |
|---|---|
| `sec:glp` | §2 GLP |
| `sec:glp-ext` | §2.1 Syntax |
| `sec:glp-operational` | §2.2 Operational Semantics |
| `sec:guards` | §2.3 Guards |
| `sec:maglp` | §3 Multiagent GLP |
| `sec:mts` | §3.1 Multiagent Transition Systems |
| `sec:glp-to-maglp` = `sec:maglp-def` | §3.2 (two labels on same subsection after merge) |
| `sec:maglp-safety` | §3.3 Safety Properties |
| `sec:ma-social-graph` | §4 The Grassroots Social Graph |
| `sec:grassroots` | §5 Multiagent GLP is Grassroots |
| `section:conclusion` | §6 Conclusion |
| `def:cglp-ts` | cGLP Transition System (defines "asynchronous resolvent") |
| `definition:maGLP` | maGLP definition |
| `theorem:maGLP-grassroots` | maGLP is grassroots |
| `prop:app-grassroots` | GLP applications using cold-calls are grassroots |
| `corollary:social-graph-grassroots` | The grassroots social graph is grassroots |

---

## Editorial Conventions

### Codified in `/Grassroots/docs/writing-style-guide.md` and `/Grassroots/claude.md` this session

- **NEVER invent acronyms.** Do not introduce abbreviations like "XYZ" for multi-word concepts (e.g., do not write "CLP" for "concurrent logic programming"). Spell terms out each time; use pronouns ("these languages", "it") or rephrasing for repetition. Proper system names (GLP, FCP) and well-established short forms (LP) are not acronyms in this sense.

### Pre-existing rules used throughout

- **NEVER PDF metadata** (`pdftitle`, `pdfauthor`, etc.) in LaTeX preambles.
- **NEVER** use "pattern" (except pattern-matching), "shape", or "involving" — imprecise and lazy.
- **NEVER apologise.** No "even though...", "although still...", "while not..." constructions.
- **No marketing language.** No "novel", "revolutionary", "paradigm shift".
- **Tense discipline.** Present tense only for what is already true; future/may/can for what the project will/may enable.
- **No fragmented sources.** Primary sources only; flag secondary explicitly.
- **No hand-waving.** Every claim has either a proof or an explicit "informal" mark.
- **"Here we present..."** framing for contributions, never "In this paper, we..."
- **"We"** throughout, never "I".
- **Three-part structures** using `(\ia), (\ib), (\ic)` for complex concepts.

### Working method

- **Discussion Mode by default.** Propose edits, get approval, then apply.
- **`edit_file` ALWAYS `dryRun=true` first.** Inspect diff before applying.
- **`edit_file` cascade risk** on LaTeX/math-dense files — fall back to `write_file` if dry-run shows surprises.
- **Re-read files before editing within a session.** Stale in-context copies cause failed matches.
- **Edits in textual order.** Never prioritise across the paper.
- **`bib.bib` MUST NOT be read** by Claude Chat (file too large, crashes session). Edits to `Bib-Grassroots/bib.bib` only with a known-exact `oldText`.

---

## Page Budget

After all whitespace tightening (etoolbox/titlesec/amsthm preskip/postskip = 4pt, verbatim -0.6/-0.4 baselineskip, titlespacing 8pt/4pt 6pt/3pt 4pt/2pt, `\mypara` 1pt vspace), plus Related Work and Platforms sections dropped, plus Conclusion ¶1 expanded, plus the social-graph expansion (Channels + befriend-acceptance + text-messaging + grassroots claim):

**Currently ~0.7 page spare.** Comfortable.

---

## Bibliography State

**Single source of truth:** `/Users/udi/Grassroots/Bib-Grassroots/bib.bib` (~300 KB). Paper repo's `bib.bib` is auto-imported via Overleaf and must NEVER be edited locally.

### Cite keys added/used heavily in this paper

**Historical Context paragraph:**
`shapiro1983subset`, `ueda1986guarded`, `clark1986parlog`, `shapiro1989family`, `mierowsky1985fcp`, `houri1989sequential`, `ueda1994moded`, `ueda1995io`, `ueda2001resource`, `moto1983overview`, `shapiro1983fifth`, `Ubique`, `shapiro19935th`, `armstrong2010erlang`, `akka2022`, `orleans2022`, `safra1988meta`, `lichtenstein1988concurrent`

**GLP foundational connections (intro):**
`girard1987linear`, `baker1977future`, `friedman1976impact`

**Concurrent logic programming techniques (§2.4):**
`shapiro1984fair`, `shapiro1986multiway`, `tribble1988channels`, `takeuchi1988bounded`, `shafrir1988distributed`, `shapiro1983object`, `shapiro1984systems`, `silverman1988logix`, `safra1988meta`, `lichtenstein1988concurrent`, `codish1986compiling`, `shapiro1989or`

**Grassroots framework:**
`shapiro2023grassrootsBA`, `shapiro2025atomic`, `lewis2026volitional`, `shapiro2025characterising`

### Bib entries with known weakness

None outstanding. (`Ubique` cite is the Wikipedia entry; Udi confirmed acceptable.)

---

## Workflow

- **Repo paths:**
  - Paper repo: `/Users/udi/Grassroots/GLP-ICLP-2026/`
  - Shared bib: `/Users/udi/Grassroots/Bib-Grassroots/bib.bib`
  - Style guide: `/Users/udi/Grassroots/docs/writing-style-guide.md`
  - Master Claude instructions: `/Users/udi/Grassroots/claude.md`

- **Git push pattern (always pull before push):**
  ```bash
  cd /Users/udi/Grassroots/GLP-ICLP-2026 && \
    git add <specific-files> && \
    git commit -m "<message>" && \
    git pull --no-rebase --no-edit origin main && \
    git push origin main
  ```

- **Overleaf sync:** Overleaf pulls from GitHub via Menu → GitHub → Pull. After every push from the local repo, Udi triggers an Overleaf pull. After every Overleaf-side edit, Udi pushes from Overleaf and runs `git pull` locally; Claude must re-read files before editing.

- **Concurrent Claude sessions:** Possible. Always `git add <specific-files>`, never `git add -A`. Never revert/reset without Udi's permission.

---

## Open / Pending Items

### Resolved 2026-05-16

- **"Asynchronous resolvent" usage** — Udi confirmed keep as-is at all sites; the qualifier is intentional.
- **Stale files cleanup** — `related-work.tex` and `platforms.tex` deleted.
- **`Ubique` cite** — Wikipedia entry confirmed acceptable.

### Standing

1. **Page budget headroom.** ~0.7 page spare. Available if reviewer feedback or late additions require it. Candidates previously discussed but not pursued:
   - A walkthrough scenario in the body (Alice/Bob/Charlie cold-call with resolvent states before/after)
   - The network-switch process for single-process testing
   - `lookup_send` and `inject_msg` shown explicitly

### Logistics

- Conference camera-ready due 2026-05-30 (~2 weeks).

---

## Recent Commits (newest first)

```
9df5a1b  Move Grassroots Social Graph to its own §4 (after maGLP, before grassroots proof).
         Uses existing social-graph.tex draft (Channels + cold-call init/recipient +
         befriend-acceptance + friend-mediated introduction + text messaging + boot +
         grassroots-claim forward-pointer). Remove §3.4 from maglp.tex; add \input to
         main; update intro outline; fix stale sec:social-graph → sec:ma-social-graph
         in grassroots corollary.

6d7ec81  Udi's revisions: "in Scala"/".Net" for Akka/Orleans; "evolution" replaces
         "migration"; closing clause "while maintaining the simplicity and efficiency
         of futures/promises". Merged labels sec:glp-to-maglp + sec:maglp-def in
         maglp.tex. §2 opener slimmed.

(earlier) Drop the CLP acronym: spell out "concurrent logic programming" throughout.

(earlier) Move related-work into intro as \mypara{Historical Context}: CLP family in
         the 80s; Fifth Generation deployment incl. Ubique/Virtual Places (FCP,
         acquired by AOL 1995, migrated to C); Fifth Gen closure → CLP went out of
         fashion; Erlang as closest descendant, then Elixir/Akka/Orleans. Expand
         conclusion ¶1. Drop related-work.tex from build.
```

---

## Quick-Reference: File Paths

```
/Users/udi/Grassroots/GLP-ICLP-2026/
├── main_GLP_ICLP_2026.tex        # Main document
├── CLAUDE.md                       # Project-specific Claude instructions
├── bib.bib                         # Auto-imported from Bib-Grassroots; DO NOT EDIT
├── sections/
│   ├── introduction.tex            # §1
│   ├── glp.tex                     # §2
│   ├── maglp.tex                   # §3
│   ├── social-graph.tex            # §4 (NEW separate section)
│   ├── grassroots.tex              # §5
│   ├── conclusion.tex              # §6
│   └── appendix-*.tex              # 8 appendices, conditional on \appendixtrue
└── status-camera-ready-2026-05-16.md  # THIS FILE
```
