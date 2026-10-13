# Claude Code Team Agents

Three sub-agent definitions designed to be included in any Claude Code multi-agent workflow. Each one runs in its own fresh conversation, so it reviews the work without the assumptions of the session that produced it.

These are the same agents published in [ai-workflows](https://github.com/myleshungerford/ai-workflows/tree/main/agents), alongside the Review Team skill that uses them and other workflows such as Goodnight.

## What's Included

- **Quality Advocate** (`quality-advocate.md`): Pressure-tests every decision the domain-specific agents make. Identifies weaknesses and proposes concrete alternatives.
- **Executive** (`executive.md`): Owns coordination across all team members. Resolves disagreements, identifies gaps, and owns the final delivery checklist.
- **Plain-Language Reviewer** (`plain-language-reviewer.md`): Reads a deliverable as a non-technical reader would, before it reaches that audience.

## How to Use

Copy the three files into `~/.claude/agents/` to use them in all your projects, or into a project's `.claude/agents/` folder. If the `agents` folder did not exist when your session started, restart Claude Code. Then add an instruction like this to your `CLAUDE.md`:

```
When dispatching any team of sub-agents (via the Agent tool, subagent-driven-development, or similar parallel workflows), always include the quality-advocate and executive agents in addition to the domain-specific agents. Never run them on Sonnet or Haiku; otherwise the main session chooses the model.
```

## Model Policy

Quality Advocate and Executive never run on Sonnet or Haiku, because work that warrants this review should not be reviewed by a lighter model. Beyond that, the main session chooses. Both default to Opus, which the Pro plan includes; a session with Fable available might choose Fable instead. The Plain-Language Reviewer runs on Sonnet because its job is wording, not judgment.

## Sequencing Rules

Quality Advocate and Executive run **after** the domain-specific agents finish. They are never dispatched in parallel with domain agents.

1. Dispatch domain-specific agents first
2. Wait for their results
3. Dispatch the **Quality Advocate** with the artifact AND the domain agents' output
4. Dispatch the **Executive** with the consolidated output from all other agents
5. For a non-technical audience, dispatch the **Plain-Language Reviewer** last

The QA pressure-tests the domain agents' findings. The Executive reviews the reviewers.
