# Instructions for Claude

## Division of Labor

### Claude Web (Chat Interface)
- **Paper writing and LaTeX editing** - All revisions to .tex files
- **Discussion and planning** - Reviewing content, proposing changes
- **Direct file editing** - Uses Filesystem tools to read/write files

### Claude Code (Terminal Interface)
- **Running GLP code** - Executing .glp programs
- **Testing** - Running test suites
- **Git operations** - Commits, pushes, syncs
- **NOT for paper writing** - Do not edit .tex files

## CRITICAL - START OF EVERY CONVERSATION
1. **READ CLAUDE.md** - Always read this file first (thoroughly)
2. **ACKNOWLEDGE** - State that you have read this document and are ready for discussion
3. **DO NOTHING ELSE** - Wait for user direction before any other action

## Project Overview

**Repository:** GLP-ICLP-2026
**Purpose:** Academic paper "GLP: A Grassroots, Multiagent, Concurrent, Logic Programming Language"
**Target Venue:** ICLP 2026 (Theory and Practice of Logic Programming)
**Author:** Ehud Shapiro

## Directory Structure

```
/Users/udi/Grassroots/GLP-ICLP-2026/
├── CLAUDE.md                           # ← This file
├── main_GLP_ICLP_2026.tex              # ← Main document
├── main_GLP_ICLP_2026.bbl              # ← Inlined bibliography (no bib.bib)
│
├── STYLE FILES:
│   ├── tlp.cls                         # ← TPLP document class
│   ├── tlplike.bst                     # ← TLP bibliography style
│   └── acmtrans.bst                    # ← ACM bibliography style
│
├── SECTIONS:
│   ├── introduction.tex
│   ├── concurrent-glp.tex
│   ├── maglp.tex
│   ├── grassroots.tex
│   ├── related-work.tex
│   ├── conclusion.tex
│   ├── appendix-lp.tex
│   ├── appendix-term-matching.tex
│   ├── appendix-grassroots-defs.tex
│   ├── appendix-proofs.tex
│   ├── appendix-guards.tex
│   ├── appendix-additional-techniques.tex
│   ├── appendix-social-graph-walkthrough.tex
│   └── appendix-social-graph-complete.tex
```

## Core Rules

### CRITICAL: Always Commit and Push When Done
- At the end of every completed task, **always commit and push** without being asked
- Never leave changes uncommitted or only committed locally
- This ensures Overleaf stays in sync via GitHub

### CRITICAL: Bibliography
- **bib.bib has been removed** from this repo for arXiv submission (master copy is in Bib-Grassroots/)
- Bibliography is inlined via `main_GLP_ICLP_2026.bbl`
- If citations are missing, add them directly to the .bbl file
- If there are bib-related errors, report them but do not attempt to fix

### Tool Permissions (Claude Code)
- Claude Code should use commands that do not require constant user approval
- Prefer Read/Edit/Write/Grep/Glob tools over shell commands where possible
- For git operations, use Bash directly (git add, commit, push are pre-approved)

### Do Exactly What Is Asked
- When the user asks something, do exactly as asked and nothing else
- Do not add extra steps, analysis, or actions beyond the specific request
- If clarification is needed, ask first rather than assuming

### Never Implement Without Agreement
- NEVER start editing without an agreed upon plan
- First discuss and document the changes
- Get explicit user agreement on the plan
- Only then proceed to implementation

### Accuracy and Honesty
- NEVER guess, speculate, or hallucinate
- If unsure, say so: "I'm not sure, need to check X"
- NEVER remove content without explicit user approval

### Communication Style
- Brief, direct responses
- No long explanations - get to the point
- Mistakes: Just acknowledge - no apologies or promises
- **Never use boxed questions** (AskUserQuestion tool) — only free text discussion
- **Never leave a discussion unilaterally** — always wait for user to approve that the discussion has ended before moving on
- NEVER use the word "pattern" in any paper or document (except in the technical context of pattern-matching).  ALWAYS use more precise alternatives.

## Working Modes

### Discussion Mode (DEFAULT)
- NO EDITS - Not even small fixes
- BRIEF RESPONSES - Show content, explain what you see
- STAY ON TOPIC - Don't jump ahead
- WAIT FOR AGREEMENT - Explicit approval needed before editing

### Implementation Mode
- ONLY AFTER EXPLICIT AGREEMENT
- FOLLOW GUIDANCE - Implement what was discussed
- VERIFY CHANGES - Check edits are correct
- REPORT RESULTS - Show exactly what changed

## LaTeX Editing Guidelines

### Before Editing
1. READ THE FILE - Always read the file before editing
2. UNDERSTAND CONTEXT - Know what section you're in
3. PRESERVE FORMATTING - Maintain existing style

### Making Edits
1. SMALL CHANGES - Make targeted edits, not wholesale rewrites
2. PRESERVE LABELS - Don't change \label{} references without updating \ref{}
3. CHECK MATH - Verify math mode is correct
4. MATH-ONLY FORMAL ENVIRONMENTS - Propositions and definitions contain only math; all auxiliary/explanatory text must be placed before or after the environment, not inside it

### Common LaTeX Patterns in This Paper
- `\mypara{Name}` - Paragraph headers
- `\temph{text}` - Bold emphasis
- `\Program{title}` - Program listings
- `\begin{verbatim}...\end{verbatim}` - Code blocks
- `\udi{comment}` - Author annotations (blue)
- `\claude{comment}` - Editor annotations (red)

## Git Protocol (Claude Code only)

### CRITICAL: Always Commit AND Push
- At the end of every task, **commit and push** to the remote
- Never leave work only committed locally — always push
- Overleaf syncs directly from GitHub's `main` branch, so pushing makes changes visible there

### Standard Workflow
```bash
git add <specific files>
git commit -m "Description of changes"
git push
```

After pushing to GitHub, pull in Overleaf (Menu → GitHub → Pull) to see the compiled PDF.

## Related Repositories

- **GLP Implementation**: `/Users/udi/Grassroots/GLP/`
- **TGLP**: `/Users/udi/Grassroots/TGLP/`
- **Art-of-GLP-2025**: `/Users/udi/Grassroots/Art-of-GLP-2025/`

## Paper Structure (Agreed Jan 2026)

1. Introduction (revise when main content done)
2. Concurrent GLP (TS, LP as TS, GLP, examples, social graph with network switch)
3. maGLP (MTS, maGLP definition, MA social graph - NOT grassroots yet)
4. maGLP is Grassroots (grassroots definition, proofs, corollaries)
5. Related Work
6. Conclusion

## #remember Directive

When the user says `#remember <something>`, add that information to this CLAUDE.md file so it persists across sessions.
