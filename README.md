# insights-to-prompts

**Turn your Claude Code `/insights` report into better prompts.**

`/insights` tells you where your sessions went wrong, but it doesn't rewrite the prompts behind that friction. insights-to-prompts does. It reads your report, the cached session facets and your transcripts. Then it finds the prompts that caused a misread request, an edit to the wrong file, over-engineering or a rejected action, and writes before/after rewrites. Each rewrite is tied to the sessions that justify it. It can also check the prompts inside your own skills and propose SKILL.md fixes as diffs.

## Usage

```text
/insights
Improve my prompts from insights.
Use my insights report to fix the prompts in my skills in ~/arm-pz.
```

## When to use

- You ran `/insights` and want to act on the friction section
- Claude keeps misreading your requests or touching the wrong files
- You keep correcting Claude with "no, I meant…"
- You want to know which of your skills cause friction when invoked

## What it produces

- `prompt-rewrites.md`: up to ~10 before/after rewrites, each with its evidence and a one-line note on what changed
- Diffs for skill prompts, shown but never applied without approval
- A "not a prompt problem" list (tool failures, environment issues)
- A list of repeated instructions to move into CLAUDE.md via `harness-audit`

## How it works

`scripts/extract_insights.py` (Python standard library only) reads `~/.claude/usage-data` and `~/.claude/projects` and writes `insights-digest.json`. The digest holds the prompt-type friction ranked by severity, repeated prompt openers, and per-skill friction when you pass `--skills-dir`.

```bash
python3 scripts/extract_insights.py --skills-dir ~/arm-pz --out insights-digest.json
```

## Install

```bash
npx skills add arm-pz/insights-to-prompts
```

## Not for

- Adding rules to CLAUDE.md, hooks or settings: use `harness-audit`
- Sharpening one pasted prompt with no report behind it: use a sharpen-prompt skill
- Building a skill from a list of prompts: use `prompts-to-skill`
