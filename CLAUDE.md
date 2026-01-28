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
├── main GLP ICLP 2026.tex              # ← Main document
├── bib.bib                             # ← Bibliography
│
├── STYLE FILES:
│   ├── new_tlp.cls                     # ← TPLP document class
│   ├── acmtrans.bst                    # ← Bibliography style
│   └── aopmath.sty                     # ← Math package
│
├── SECTIONS (Main Content):
│   ├── glp_section_introduction.tex
│   ├── glp_section_concurrent_glp.tex  # ← Combined TS/LP/GLP section
│   ├── glp_section_foundations.tex
│   ├── glp_section_logic_programs.tex
│   ├── glp_section_glp.tex
│   ├── glp_section_multiagent.tex
│   ├── glp_section_examples.tex
│   ├── glp_section_social_graph.tex
│   ├── glp_section_implementation.tex
│   ├── glp_section_related_work.tex
│   └── glp_section_conclusion.tex
│
├── APPENDICES:
│   ├── glp_appendix_proofs.tex
│   ├── glp_appendix_social_graph_properties.tex
│   ├── glp_appendix_social_networking.tex
│   ├── glp_appendix_guards_system.tex
│   ├── glp_appendix_additional_techniques.tex
│   ├── glp_appendix_security.tex
│   ├── glp_appendix_workstation.tex
│   └── glp_appendix_smartphone.tex
│
├── Code/                               # ← Code snippets for paper
├── Figs/                               # ← Figures
└── OLD/, Backup/                       # ← Previous versions
```

## Core Rules

### CRITICAL: Do Not Edit Bibliography
- **NEVER edit bib.bib** - The bibliography file is managed by the user only
- If there are bib-related errors, report them but do not attempt to fix

### CRITICAL: Filesystem Access
- **Bash/shell commands DO NOT WORK** on the user's local filesystem
- Use ONLY the Filesystem tools (read_text_file, edit_file, write_file, search_files, list_directory)
- NEVER use bash_tool for file operations on /Users/udi/
- For git operations, provide commands for the USER to run manually

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

### Common LaTeX Patterns in This Paper
- `\mypara{Name}` - Paragraph headers
- `\temph{text}` - Bold emphasis
- `\Program{title}` - Program listings
- `\begin{verbatim}...\end{verbatim}` - Code blocks
- `\udi{comment}` - Author annotations (blue)
- `\claude{comment}` - Editor annotations (red)

## Git Protocol (Claude Code only)

### Standard Workflow
```bash
# Check status
git status

# Stage and commit
git add -A
git commit -m "Description of changes"

# Push
git push
```

### Overleaf Workflow
Overleaf syncs directly from GitHub's `main` branch.

**To push changes to Overleaf for PDF compilation:**
```bash
cd /Users/udi/Grassroots/GLP-ICLP-2026 && git add -A && git commit -m "<message>" && git push
```

After pushing to GitHub, pull in Overleaf (Menu → GitHub → Pull) to see the compiled PDF.

## Related Repositories

- **GLP Implementation**: `/Users/udi/Grassroots/GLP/`
- **Moded-Types Paper**: `/Users/udi/Grassroots/Moded-Types/`
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
