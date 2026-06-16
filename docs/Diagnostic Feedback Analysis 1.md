Copilot prompt:

`/explain Ambiguous: "User asks for help with README.md". This phrase is underspecified: 'help' could mean write a new README, revise an existing one, fix mistakes, or explain parts of a README. A model may choose the wrong task and produce an unexpected result. Suggestion: Replace it with: 'Use this skill when the user asks for a new or updated README.md for this repository.'`

## Diagnostic Feedback Analysis 📋

The diagnostic is flagging ambiguity in your `c:\Users\jocil\.claude\skills\readme\SKILL.md` skill definition. Here's what needs to be fixed:

### Current Issue
```markdown
User asks for help with README.md
```

**Problem:** This is too vague - "help" could mean anything (write, revise, fix, explain). The model might choose the wrong task.

---

## Recommended Fix ✨

Based on your other skills in the list (`readme-generator`, `docx`, etc.), here's a clearer definition:

```markdown
Use this skill when the user asks for a new or updated README.md for this repository, including comprehensive documentation with architecture diagrams, setup instructions, and troubleshooting guides.
```

### Why This Works Better ✅

1. **Specific trigger condition** - "new or updated README.md" is clear
2. **Explicit scope** - mentions what the skill produces (documentation)
3. **Consistent pattern** - matches other skills like `readme-generator` which says: *"Use this skill whenever the user provides a GitHub URL and wants to generate, improve, or create documentation for a repository"*

---

Would you like me to update your `SKILL.md` file with this improved definition?