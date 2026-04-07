# CRITICAL

Before starting a new task, review `.agents/knowledge/INDEX.md` and the relevant domain `rules.md` and `hypotheses.md`.
Apply rules by default. Check if any hypothesis can be tested with today's work.

**Insights:**

- At the end of each task which user accepts as good, extract insights.
- Do not extract insights for work that is not yet completed and marked by the user as done
- Store insights in domain folders:
  - `.agents/knowledge/<domain>/knowledge.md` for facts and patterns
  - `.agents/knowledge/<domain>/hypotheses.md` for items that need more data
  - `.agents/knowledge/<domain>/rules.md` for confirmed guidance to apply by default

Maintain `.agents/knowledge/INDEX.md` so it routes to each domain folder. Create the structure if it does not exist yet.
When a hypothesis gets confirmed 3+ times, promote it to a rule.
When a rule gets contradicted by new data, demote it back to a hypothesis.

When about to make a decision that affects more than today's task, first grep `.agents/decisions/` for prior decisions in that area. Follow them unless new information invalidates the reasoning.
If no prior decision exists, or you are replacing one, log it:
File: `.agents/decisions/YYYY-MM-DD-{topic}.md`
Format:
```
## Decision: {what you decided}

### Context: {why this came up}

### Alternatives considered: {what else was on the table}

### Reasoning: {why this option won}

### Trade-offs accepted: {what you gave up}

### Supersedes: {link to prior decision, if replacing}
```

Durable domain knowledge and apply-by-default rules live under `.agents/knowledge/`. Keep this file focused on workflow and repository guidelines.
