# Test cases — insights-to-prompts

Status: written, triggering not yet run. Script run against a synthetic fixture (pass).

| # | Message | Expected skill | Mode | Pass condition |
| --- | --- | --- | --- | --- |
| 1 | "I ran /insights, now help me write better prompts" | insights-to-prompts | session | Reads report.html; each rewrite cites a session |
| 2 | "what am I prompting badly in Claude Code?" | insights-to-prompts | session | Asks for /insights if report > 7 days old |
| 3 | "use my insights report to fix the prompts in my arm-pz skills" | insights-to-prompts | skill | Runs with --skills-dir; shows diffs, applies nothing |
| 4 | "why does Claude keep editing the wrong files when I ask?" (implicit) | insights-to-prompts | session | Targets wrong_file_or_location sessions |
| 5 | "I keep having to correct Claude, coach me" (implicit) | insights-to-prompts | session | Builds rewrites from corrective follow-ups |
| 6 | "add the /insights CLAUDE.md suggestions to my CLAUDE.md" | harness-audit | — | Does not trigger; config, not prompts |
| 7 | "make this prompt better: 'write tests for utils'" | sharpen-prompt | — | Does not trigger; no report involved |
| 8 | "turn these 10 prompts into a skill" | prompts-to-skill | — | Does not trigger; shares "prompts" keyword only |
| 9 | "summarize my /insights report" | none / plain answer | — | Does not trigger; no rewrite asked |

## Boundary pairs

| Message | Should trigger | Why |
| --- | --- | --- |
| "I tell Claude 'use pnpm' every session — fix my prompts" | insights-to-prompts → hands to harness-audit | Repeated instruction is a CLAUDE.md rule; listed under "send to harness-audit" |
| "audit my CLAUDE.md against my sessions" | harness-audit | Harness changes |
| "rewrite my prompts from insights and put the rules in CLAUDE.md" | starts insights-to-prompts, ends harness-audit | Rewrites first, rule list handed over |
