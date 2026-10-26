# mroowa-stack

The agent skills I use from [tstack](https://github.com/t3dotgg/tstack) by Theo ([@t3dotgg](https://github.com/t3dotgg)) and [pstack](https://github.com/cursor/plugins/tree/main/pstack) by poteto ([@poteto](https://github.com/poteto)). Each skill name has the `mroowa-` prefix, so typing `/mroowa` lists them all together.

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

## Source

The `mroowa-how`, `mroowa-tdd`, `mroowa-typescript-best-practices`, `mroowa-laziness-protocol`, `mroowa-model-the-domain`, `mroowa-teach`, and `mroowa-interrogate` skills originate from [Lauren Tan’s pstack](https://github.com/cursor/plugins/tree/11713c683fe4add4fd403ea880580abbc9e0875f/pstack), version 0.15.17, at commit `11713c683fe4add4fd403ea880580abbc9e0875f`.

The `mroowa-how` and `mroowa-tdd` skills retain their upstream contents. The principle skills use shorter names. The TypeScript skill is self-contained, with dependencies on separate pstack skills removed and examples kept in an optional reference file.

The `mroowa-how` skill includes its explorer and explainer prompt templates. Its upstream instructions use Cursor’s subagent tools and model configuration.

The `mroowa-teach` skill is adapted for a smaller token budget: one agent by default, existing evidence reused, design history investigated only when relevant, and optional diagrams. It has no required `how`, `why`, or `unslop` dependency and does not automatically generate images. It preserves explicit invocation in Codex through `skills/mroowa-teach/agents/openai.yaml`.

The `mroowa-interrogate` skill uses exactly one read-only review subagent, inheriting the parent model by default. The parent evaluates its findings using the bundled rubric and judgment framework. Multi-model panels, further delegation, and the agreement map are removed. If delegation is unavailable, it falls back to one local review. It preserves explicit invocation in Codex and reports findings without automatically applying fixes.

The pstack imports are MIT licensed. See [LICENSE](LICENSE).

The `mroowa-babysit`, `mroowa-file-pr`, and `mroowa-leaving-pr-comments` skills originate from [Theo Browne’s tstack](https://github.com/t3dotgg/tstack/tree/7de017b3fc9d50c03cf3ecb98fb71e0ca65a78bd/skills) (`babysit-pr`, `file-pr`, and `leaving-pr-comments`), at commit `7de017b3fc9d50c03cf3ecb98fb71e0ca65a78bd`. They keep their upstream contents. Names have the `mroowa-` prefix, and the skills refer to each other by those names. `babysit-pr` is imported as `mroowa-babysit` and replaces the earlier Claude-Mem import of that name.

`mroowa-babysit` waits with T3 Code’s `watch_pull_request` when it is available. Otherwise it uses the bundled `skills/mroowa-babysit/scripts/pr-wait`, which requires `python3` and an authenticated `gh`. `mroowa-file-pr` and `mroowa-babysit` use `mroowa-leaving-pr-comments` for every comment they post, so install the three together.

The tstack imports are MIT licensed. See [LICENSE](LICENSE).
