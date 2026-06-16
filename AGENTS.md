# AGENTS.md - Working in this Repo

## Purpose Context
This repository stores self-contained **skill packages** that extend Claude's capabilities. Each skill is a mini-project with `SKILL.md` (required) and optional bundled resources (`scripts/`, `references/`, `assets/`). Output: distributable `.zip` files sharing those skills with users, not internal app/maintenance code this repo serves as infrastructure for the developer to create/sell these packages.

## Directory Boundaries
- **Root** `/`: Project docs (README.md), analysis notes from reviewing existing SKILLs
- `skills/`: Skill source directory - contains all skill definitions (`_template`, `readme`, `skill-creator`) and their metadata/scripts  
  *No skills outside this folder* — don't assume new dirs contain active work unless you see a `.gitkeep` or files matching the pattern above.
- **Packaging output**: Zip packages go to external locations; no persistent packaging artifacts stored here.

## The Core Rule: Read Frontmatter First
When opening any skill, always parse its YAML frontmatter lines (starting with `---`) for exact metadata values (`name`, `description`). These determine what Claude uses when triggered in a user chat — more precise than the body text or instructions inside SKILL.md matters most here.

## Validation Rules from SKILLs
From existing skills, enforce these patterns:
- Scripts need deterministic reliability if written repeatedly; reference files contain domain knowledge (database schemas like `reference/finance.json`) that Claude references but may also be loaded via grep into context when relevant. Assets are output templates/files that don't load fully but can copy to user's local environment later or as part of the deliverable zip package
- Skills should stay lean: body content and reference files combined < 5k words for performance; larger info must live purely in referenced assets (not scripts) unless it's critical procedural logic

## Essential Commands from SKILLs Documentation
```bash
# Generate new skill template directory with example skeletons 
python /mnt/c/Users/jocil/Downloads/ai-skills-workspace/skills/readme/scripts/package_skill.py <skill-folder-name>
    # Example: python package_skill.py my-skill --path ./skills/my-skill

# Validate then pack into external .zip (no persistent artifacts left here if successful)
python /mnt/c/Users/jocil/Downloads/ai-skills-workspace/skills/readme/scripts/checks.py <skills-directory>/readme > report.md

```

**Command Order Pattern**: `init/py_init_py <skill-foldernam>`, then validate via `checks.py` to catch missing frontmatter (name/desc required), directory structure (`scripts/`=deterministic code, `references/domains.json`=knowledge files) and assets as needed for user's skill package.

**Note from docs**: If checks fail before zip generation fix the issue — you may need an interactive prompt loop here to ensure no empty directories were created unintentionally after deleting example scripts or references that should be removed once finalized (the pattern shows `scripts/init_skill.py` creates sample files that most skills won't fully adopt).

## Writing Style for SKILLs
When authoring new content: write entire skill in **imperative form** rather than second person. Example instead of "Use this tool when..." use "This skill should be invoked when...". For reference materials (JSON/API specs) embed search terms into the instructions so users don't need to grep everything themselves unless those files exceed ~10k words total, at which point move them to an external `reference/*.json` file instead.

Do not include non-functional fluff; focus on what Claude needs as a working agent — concrete workflows and reusable patterns that make tasks reliable or deterministic when executed. Avoid generic software boilerplate if it differs across domains (e.g., API queries differ fundamentally from code generators).
