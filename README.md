# mroowa-stack

The agent skills I use from [tstack](https://github.com/t3dotgg/tstack) by Theo ([@t3dotgg](https://github.com/t3dotgg)) and [pstack](https://github.com/cursor/plugins/tree/main/pstack) by poteto ([@poteto](https://github.com/poteto)), plus [Cloudflare's security-audit-skill](https://github.com/cloudflare/security-audit-skill). Each skill name has the `mroowa-` prefix, so typing `/mroowa` lists them all together.

| Skill | Purpose |
| --- | --- |
| [mroowa-how](skills/mroowa-how/SKILL.md) | Explore a codebase and explain subsystem architecture, runtime flow, and ownership. |
| [mroowa-tdd](skills/mroowa-tdd/SKILL.md) | Reproduce a bug with a focused failing test, then fix it and verify the result. |
| [mroowa-typescript-best-practices](skills/mroowa-typescript-best-practices/SKILL.md) | Model domain contracts with TypeScript types and validate external data at boundaries. |
| [mroowa-laziness-protocol](skills/mroowa-laziness-protocol/SKILL.md) | Prefer deletion, smaller changes, and fewer layers of complexity. |
| [mroowa-model-the-domain](skills/mroowa-model-the-domain/SKILL.md) | Encode state and domain rules in suitable data structures instead of scattered conditionals. |
| [mroowa-babysit](skills/mroowa-babysit/SKILL.md) | Watch a PR through CI and review bots with one watcher, fix real findings, and stop when it is ready to merge. |
| [mroowa-file-pr](skills/mroowa-file-pr/SKILL.md) | File a short PR that leads with the problem, not an inventory of changes. |
| [mroowa-leaving-pr-comments](skills/mroowa-leaving-pr-comments/SKILL.md) | Format GitHub comments an agent posts on your behalf, with a model attribution note. |
| [mroowa-teach](skills/mroowa-teach/SKILL.md) | Explain concepts and code in small conversational layers, with concrete examples and optional diagrams. |
| [mroowa-interrogate](skills/mroowa-interrogate/SKILL.md) | Adversarially review changes with one read-only reviewer, then filter findings through parent judgment. |
| [mroowa-security-audit](skills/mroowa-security-audit/SKILL.md) | Find vulnerabilities across real trust boundaries at three levels: `low` (single-agent scan), `medium` (two layers, at most two subagents), or `full` (complete audit with report). |

## Source

All skills are MIT licensed. See [LICENSE](LICENSE).

- **[pstack](https://github.com/cursor/plugins/tree/11713c683fe4add4fd403ea880580abbc9e0875f/pstack)** (v0.15.17): `how`, `tdd`, `typescript-best-practices`, `laziness-protocol`, `model-the-domain`, `teach`, `interrogate`. `teach` and `interrogate` are trimmed to use a single agent. The TypeScript skill doesn't depend on other skills.
- **[tstack](https://github.com/t3dotgg/tstack/tree/7de017b3fc9d50c03cf3ecb98fb71e0ca65a78bd/skills)**: `babysit`, `file-pr`, `leaving-pr-comments`. They are unchanged apart from the prefix. Install all three together. Outside T3 Code, `babysit` needs `python3` and an authenticated `gh`.
- **[security-audit-skill](https://github.com/cloudflare/security-audit-skill/tree/c1c8a8c1471069fb0e188eeaff69b8e8db6564a8/skills/security-audit)** by Cloudflare: `security-audit`. Adds the `low` and `medium` audit levels; `full` is the original workflow.
