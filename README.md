# claude-skills

Opinionated Claude Code skills. Built to be used, not admired.

![demo](./media/demo.gif)

---

## What's in here

### `timeline-patterns`

A pattern catalog for designing timeline, activity feed, history, and personal memory interfaces. Not a tutorial. Not a listicle. A working reference you pull up *while* you're designing — structured so you can compose an interface in minutes by picking one choice per axis.

- **30+ named patterns** across five axes (time encoding · density · navigation · detail · search/filter)
- **Meta-patterns** for recall/memory products (Three Questions model · Moment Card · Replay vs Explore)
- **7 ready-to-build combinations** — each with effort, risk, and a named failure mode
- **Anti-patterns** called out
- **Visual preview** — all seven combos rendered as working wireframes in a single self-contained HTML file ([`previews.html`](./plugins/timeline-patterns/skills/timeline-patterns/previews.html))

---

## Install

```
/plugin marketplace add sksareen/claude-skills
/plugin install timeline-patterns@sksareen-skills
```

Invoke with `/timeline-patterns` from any Claude Code session.

---

## How this got built in under an hour

This entire skill — catalog, visual preview with seven rendered mockups, plugin packaging, genericization, and publish — went from "hey can you make this?" to `git push` in roughly 60 minutes. Worth breaking down *how*, because the shape is reusable.

**The orchestration pattern:**

| Model | Role | Why |
|---|---|---|
| Opus 4.7 | Lead / synthesis | Needed for the opinionated catalog — tradeoffs, design judgment, the actual *content* of the patterns |
| Subagents (Opus) | Parallel editing | Genericizing files, transforming the Sauron-specific preview into a generic version |
| **Haiku 4.5** | **Verification** | **Checked the work at the end — file tree, JSON schema, frontmatter, zero Sauron refs, git state** |

**Use Haiku for verification.** Haiku is dramatically faster than Opus and costs ~15× less. For checks that are concrete (does this file exist? does this JSON parse? does grep find a string?) Haiku is the right call — not because it's cheaper but because it's *faster*, which tightens the iteration loop. The final pass before push took 17 seconds. That loop-tightening compounds across a session.

**The shape that worked:**
1. **Opus for the creative work** — writing the catalog, designing the wireframes, making the opinionated calls.
2. **Parallel subagents for mechanical edits** — I had two transformations to do (genericize SKILL.md, genericize previews.html). They were independent. Running them sequentially would have been 2× the wall time.
3. **Haiku for verification** — everything was built, the final question was "did it actually land?" That's a checklist, not a judgment call. Haiku nailed it.

You can use this shape for almost anything. The rule I'm settling into: **match model to task shape, not to project importance**. An important project still has 80% mechanical tasks.

---

## Design principle: ship the reference, then iterate

The original skill is dense — 400+ lines, opinionated takes, real exemplars. That density is load-bearing: a pattern catalog with shallow entries is worse than no catalog because it gives a false sense of completeness. Better to be comprehensive-in-scope-and-opinionated-in-depth than shallow-and-neutral.

If you use this and hit a pattern that's missing or a take you disagree with — open an issue or PR. The catalog gets sharper the more people use it.

---

## License

MIT — see [`LICENSE`](./LICENSE).

## More

- Built by [@sksareen](https://github.com/sksareen) with [Claude Code](https://claude.com/claude-code)
- The origin context was designing [Sauron](https://github.com/sksareen/sauron), a personal memory daemon — the catalog is generic but it was forged against a real product
