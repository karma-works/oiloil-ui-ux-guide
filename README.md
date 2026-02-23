# oiloil-ui-ux-guide

A Codex Skill for modern, clean interfaces.  
It turns UI/UX recommendations into actionable changes, focusing on two problems:

- Review conclusions that are too vague to implement in code
- Page hints that keep accumulating until they become a "wall of tips"

## Use Cases

- Pre-launch design review using a stable set of rules
- Improving existing pages with prioritized fixes
- Design reviews that produce outputs ready for development tasks

## What This Skill Can Do

This Skill has two modes:

- `guide`: Provides concise, actionable "do / don't" rules
- `review`: Reviews existing interfaces and outputs a `P0 / P1 / P2` fix list

Core capabilities include:

- Task-first: Primary tasks and actions identifiable within 3 seconds
- Layered hints: Keep only necessary information, reduce persistent clutter
- State completeness: Cover loading / empty / error / success / permission states
- Diagnostic methods: Distinguish execution gulf, evaluation gulf, slips vs. mistakes
- Visual standards: Emphasize CRAP (Contrast/Repetition/Alignment/Proximity) and consistent spacing
- Icon standards: No emoji icons; require a consistent icon set

## Cross-Tool Support (Codex / Claude Code / Cursor / Windsurf)

Bottom line: There's no single "universal file standard" adopted by all tools yet.  
The most reliable approach in practice:

- Use `AGENTS.md` as the cross-tool shared instruction entry (single source of truth)
- Use lightweight adapter files for each tool (e.g., `CLAUDE.md`, `.cursor/rules/*.mdc`)
- Keep `SKILL.md` as the Skill's behavior definition

This repository is already configured this way.

## How to Use with Each Tool

- Codex: Native Skill workflow, reads `SKILL.md` and `agents/openai.yaml`
- Claude Code: Reads `CLAUDE.md` in-project (already bridges to `AGENTS.md` + `SKILL.md`)
- Cursor: Can read `AGENTS.md`, supports `.cursor/rules/*.mdc`
- Windsurf: Supports `AGENTS.md` as project-level agent instructions

## Install to Multiple Agents with `skills` CLI (Recommended)

You can use the [vercel-labs/skills](https://github.com/vercel-labs/skills) CLI to install this Skill to multiple agents.

### List Available Skills in the Repository

```bash
npx skills add oil-oil/oiloil-ui-ux-guide --list
```

### Install to Multiple Agents at Once

```bash
npx skills add oil-oil/oiloil-ui-ux-guide \
  -a codex \
  -a claude-code \
  -a cursor \
  -a windsurf
```

### Global Installation (Available Across Projects)

```bash
npx skills add oil-oil/oiloil-ui-ux-guide \
  -g \
  -a codex \
  -a claude-code \
  -a cursor \
  -a windsurf
```

Notes:

- `-a` specifies the target Agent
- `-g` installs to user directory (global)
- To install only a specific Skill from this repository, add `--skill <name>`

## Installation & Configuration (Codex)

### Option A: Install via GitHub (Recommended)

Run in Codex environment:

```bash
scripts/install-skill-from-github.py --repo oil-oil/oiloil-ui-ux-guide --path .
```

### Option B: Manual Installation

Copy the repository to:

```bash
~/.codex/skills/oiloil-ui-ux-guide
```

Recommended directory structure:

```text
~/.codex/skills/oiloil-ui-ux-guide/
  AGENTS.md
  CLAUDE.md
  .cursor/rules/oiloil-ui-ux-guide.mdc
  agents/openai.yaml
  index.html
  skills/
    oiloil-ui-ux-guide/
      SKILL.md
      references/
```

Restart Codex after installation to activate the new Skill.

> If you already used `npx skills add` above to install to Codex, you can skip this section.

## Triggering This Skill Correctly in Different AIs

Two ways to trigger:

1. Explicitly name the Skill
   - `Please use $oiloil-ui-ux-guide to review this settings page.`
2. Describe a matching task directly
   - "Help me review this dashboard and give fix suggestions prioritized by P0/P1/P2."
   - "Give me concise UX rules for this creation flow, focusing on preventing hint stacking."

We recommend explicitly including `oiloil-ui-ux-guide` in Claude/Cursor/Windsurf for more reliable triggering.

## Recommended Prompt Templates

### Template 1: review (Review Existing Interface)

```text
Please use $oiloil-ui-ux-guide in review mode.
Context: Web admin panel, target users are first-time users completing configuration.
Goal: Improve first-time configuration completion rate, reduce errors.
Please output:
1) Key assumptions
2) P0/P1/P2 issue list (with brief evidence)
3) Actionable fix for each issue (layout/component/copy/state)
4) Acceptance checkpoints
```

### Template 2: guide (Rules Before Design)

```text
Please use $oiloil-ui-ux-guide in guide mode.
Page type: B2B settings page.
Please output concise "do / don't" rules covering:
- Primary task and action hierarchy
- Layered hints
- State completeness
- Spacing/repetition/alignment
Requirement: Avoid long paragraphs; use bullet points.
```

## Output Style (Expected Results)

- Short conclusions with clear focus; no vague platitudes
- Every suggestion actionable at the interface and code level
- Clear priorities for scheduling
- Acceptance checkpoints at the end for verifying improvements

## Repository Structure

- `AGENTS.md`: Cross-tool shared instructions (recommended as single source of truth)
- `CLAUDE.md`: Claude Code entry (bridges to shared instructions)
- `.cursor/rules/oiloil-ui-ux-guide.mdc`: Cursor rules entry (bridges to shared instructions)
- `agents/openai.yaml`: Skill display info and default prompts
- `index.html`: Skill introduction and visual examples page
- `skills/oiloil-ui-ux-guide/SKILL.md`: Main Skill rules and workflow
- `skills/oiloil-ui-ux-guide/references/system-principles.md`: System-level guiding principles
- `skills/oiloil-ui-ux-guide/references/interaction-psychology.md`: Interaction psychology (HCI laws, cognitive biases, interaction pacing, attention economy)
- `skills/oiloil-ui-ux-guide/references/design-psych.md`: Design psychology diagnostic vocabulary
- `skills/oiloil-ui-ux-guide/references/icons.md`: Icon consistency and comprehensibility rules
- `skills/oiloil-ui-ux-guide/references/review-template.md`: Standard review output template
- `skills/oiloil-ui-ux-guide/references/checklists.md`: Extended checklists

## References

- skills CLI (cross-Agent distribution): <https://github.com/vercel-labs/skills>
- Claude Code memory mechanism (`CLAUDE.md`): <https://docs.anthropic.com/en/docs/claude-code/memory>
- Cursor rules and `AGENTS.md`: <https://docs.cursor.com/context/rules-for-ai>
- Windsurf `AGENTS.md` support: <https://docs.windsurf.com/windsurf/cascade/memories>

## License

This project is licensed under Apache License 2.0, see `LICENSE.txt` for details.
