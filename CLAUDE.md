# Instructions for Claude Code (Terminal Interface)

## CRITICAL - START OF EVERY CONVERSATION
1. **READ CLAUDE.md** - Always read this file first (thoroughly)
2. **ACKNOWLEDGE** - State that you have read this document and are ready for discussion
3. **DO NOTHING ELSE** - Wait for user direction before any other action
4. **MOUNT REPOSITORIES** - Clone related repos when needed:
   - FCP: `git clone --depth 1 https://github.com/EShapiro2/FCP.git /tmp/FCP`
   - Art-of-GLP-2025: `git clone --depth 1 https://github.com/EShapiro2/Art-of-GLP-2025.git /tmp/Art-of-GLP-2025`
5. **IDENTIFY CURRENT MODE** - Discussion or Implementation
6. **FOLLOW MODE RULES** - Never mix modes

## Project Overview

**Repository:** GLP-2025
**Purpose:** Academic paper "GLP: A Secure, Multiagent, Grassroots, Concurrent, Logic Programming Language"
**Target Venue:** ICLP 2026 (Theory and Practice of Logic Programming)
**Format:** TPLP (new_tlp.cls)
**Author:** Ehud Shapiro

## Directory Structure

```
/home/user/GLP-2025/
├── CLAUDE.md                           # ← This file
├── main GLP 2025.tex                   # ← Main document
├── bib.bib                             # ← Bibliography (574 entries)
│
├── STYLE FILES:
│   ├── new_tlp.cls                     # ← TPLP document class
│   ├── acmtrans.bst                    # ← Bibliography style
│   └── aopmath.sty                     # ← Math package
│
├── SECTIONS (Main Content):
│   ├── glp_section_introduction.tex
│   ├── glp_section_logic_programs.tex
│   ├── glp_section_glp.tex
│   ├── glp_section_examples.tex
│   ├── glp_section_multiagent.tex
│   ├── glp_section_social_graph.tex
│   ├── glp_section_security.tex
│   ├── glp_section_implementation.tex
│   ├── glp_section_related_work.tex
│   └── glp_section_conclusion.tex
│
├── APPENDICES:
│   ├── glp_appendix_lp_syntax.tex
│   ├── glp_appendix_proofs.tex
│   ├── glp_appendix_social_graph_properties.tex
│   ├── glp_appendix_social_networking.tex
│   ├── glp_appendix_guards_system.tex
│   ├── glp_appendix_additional_techniques.tex
│   ├── glp_appendix_workstation.tex
│   └── glp_appendix_smartphone.tex
│
├── Code/                               # ← Code snippets for paper
├── Figs/                               # ← Figures
└── OLD/, Backup/                       # ← Previous versions
```

## Core Rules

### Do Exactly What Is Asked
- **When the user asks something, do exactly as asked and nothing else**
- Do not add extra steps, analysis, or actions beyond the specific request
- If clarification is needed, ask first rather than assuming

### Never Implement Without a Plan
- **NEVER start editing without an agreed upon plan**
- First discuss and document the changes
- Get explicit user agreement on the plan
- Only then proceed to implementation

### Instructions from Claude Web
When receiving instructions from Claude Web (via user copy-paste):
- **REVIEW FIRST** - Read and understand the instructions before executing
- **RAISE CONCERNS** - Let Udi know if you have comments, questions, or see potential issues
- **DON'T BLINDLY EXECUTE** - Wait for confirmation if something seems unclear or problematic

### Accuracy and Honesty
- **NEVER BS, GUESS, SPECULATE, OR HALLUCINATE**
- **IF UNSURE, SAY SO** - "I'm not sure, need to check X"
- **NEVER REMOVE CONTENT** - Never delete text without explicit user approval

### Communication Style
- **BE TERSE** - Brief, direct responses
- **NO LONG EXPLANATIONS** - Get to the point
- **MISTAKES**: Just acknowledge - no apologies or promises
- **NO VERBOSE POLITENESS** - Skip the fluff

## Working Modes

### Discussion Mode (DEFAULT)
- **NO EDITS** - Not even small fixes
- **BRIEF RESPONSES** - Show content, explain what you see
- **STAY ON TOPIC** - Don't jump ahead
- **WAIT FOR AGREEMENT** - Explicit "let's edit" signal needed

### Implementation Mode
- **ONLY AFTER EXPLICIT AGREEMENT**
- **FOLLOW GUIDANCE** - Implement what was discussed
- **VERIFY CHANGES** - Check edits are correct
- **REPORT RESULTS** - Show exactly what changed

## Mode Transition Protocol
1. User must explicitly say: "Discussion complete, let's implement" or similar
2. Confirm understanding: "Moving to implementation mode"
3. Only then modify files

## LaTeX Editing Guidelines

### Before Editing
1. **READ THE FILE** - Always read the file before editing
2. **UNDERSTAND CONTEXT** - Know what section you're in
3. **PRESERVE FORMATTING** - Maintain existing style

### Making Edits
1. **USE EDIT TOOL** - Not Write for existing files
2. **SMALL CHANGES** - Make targeted edits, not wholesale rewrites
3. **PRESERVE LABELS** - Don't change \label{} references without updating \ref{}
4. **CHECK MATH** - Verify math mode is correct

### Common LaTeX Patterns in This Paper
- `\mypara{Name}` - Paragraph headers
- `\temph{text}` - Bold emphasis
- `\Program{title}` - Program listings
- `\begin{verbatim}...\end{verbatim}` - Code blocks
- `\udi{comment}` - Author annotations (blue)
- `\claude{comment}` - Editor annotations (red)

## Git Protocol

### Branch Rules
- **Work on assigned branch**: `claude/revise-paper-Az0EC`
- **Commit frequently** with clear messages
- **Push changes** after completing tasks

### Standard Workflow
```bash
# Check status
git status

# Stage and commit
git add -A
git commit -m "Description of changes"

# Push to branch
git push -u origin claude/revise-paper-Az0EC
```

### After Completing Work - Merge Instructions for User
```bash
cd /Users/udi/GLP-2025  # or wherever user's local copy is
git checkout main
git pull origin main
git fetch origin claude/revise-paper-Az0EC
git merge -m "Merge paper revisions" origin/claude/revise-paper-Az0EC
git push origin main
```

## Reference Repositories

### FCP (Flat Concurrent Prolog)
- **GitHub**: https://github.com/EShapiro2/FCP
- **Reference Release**: `/tmp/FCP/Savannah`
- **Clone**: `git clone --depth 1 https://github.com/EShapiro2/FCP.git /tmp/FCP`

### Art-of-GLP-2025
- **GitHub**: https://github.com/EShapiro2/Art-of-GLP-2025
- **Main file**: `/tmp/Art-of-GLP-2025/main_AofGLP.tex`
- **Clone**: `git clone --depth 1 https://github.com/EShapiro2/Art-of-GLP-2025.git /tmp/Art-of-GLP-2025`

## Paper Format

**Current Format:** TPLP (Theory and Practice of Logic Programming)
- Document class: `new_tlp`
- Bibliography style: `acmtrans`
- Required files: `new_tlp.cls`, `acmtrans.bst`, `aopmath.sty`

**Author Format:**
```latex
\author[E. Shapiro]{Ehud Shapiro}
\affiliation{London School of Economics and Weizmann Institute of Science}
\email{ehud.shapiro@weizmann.ac.il}
\keywords{concurrent logic programming, grassroots platforms, ...}
```

## Environment Notes

- **LaTeX not installed** - Cannot compile locally; user compiles on their machine
- **No `tail`, `head`, `grep`** - Use Read tool or full file output
- **Working directory**: `/home/user/GLP-2025`

## #remember Directive

When the user says `#remember <something>`, add that information to this CLAUDE.md file so it persists across sessions.

## Important Insights (Lessons Learned)

### Format Conversion (Jan 2026)
- Converted from LNCS (llncs) to TPLP (new_tlp) format for ICLP 2026
- Removed: thmtools, thm-restate option, TOC, titlerunning, authorrunning
- Added: aopmath package, keywords, email, affiliation format
