# Claude Code Team Agents

Two sub-agent role definitions designed to be included in any Claude Code multi-agent workflow. Add these to your `CLAUDE.md` to automatically include them whenever you dispatch a team of sub-agents.

## What's Included

- **Quality Advocate** (`quality-advocate.md`): Pressure-tests every decision the domain-specific agents make. Identifies weaknesses and proposes concrete alternatives.
- **Executive** (`executive.md`): Owns coordination across all team members. Resolves disagreements, identifies gaps, and owns the final delivery checklist.

## How to Use

Copy the content from both files into your `CLAUDE.md` under a section like `## Sub-Agent Team Composition`. Then add an instruction like:

```
When dispatching any team of sub-agents (via the Agent tool, subagent-driven-development, or similar parallel workflows), always include these two roles in addition to the domain-specific agents. Both must be dispatched as Opus agents.
```

## Sequencing Rules

Both agents run **after** the domain-specific agents finish. They are never dispatched in parallel with domain agents.

1. Dispatch domain-specific agents first
2. Wait for their results
3. Dispatch the **Quality Advocate** with the artifact AND the domain agents' output
4. Dispatch the **Executive** with the consolidated output from all other agents

The QA pressure-tests the domain agents' findings. The Executive reviews the reviewers.
