# claude-skills

Opinionated Claude Code skills. Built to be used, not admired.

![demo](./media/demo.gif)

---

## What's in here

### `timeline-patterns`

A pattern catalog for timeline, activity feed, history, and personal memory interfaces. Pull it up while you're designing. Pick one choice per axis. Compose an interface in minutes.

- 30+ named patterns across 5 axes: time encoding, density, navigation, detail, search
- 7 pre-composed combinations, each with effort, risk, and failure mode
- Meta-patterns for memory products (Three Questions, Moment Card, Replay vs Explore)
- Anti-patterns called out
- Seven wireframe mockups in [`previews.html`](./plugins/timeline-patterns/skills/timeline-patterns/previews.html) — open in a browser, scroll

---

## Install

```
/plugin marketplace add sksareen/claude-skills
/plugin install timeline-patterns@sksareen-skills
```

Then `/timeline-patterns` from any session.

---

## Built in an hour

Idea to `git push` in ~60 minutes. How:

| Model | Role |
|---|---|
| Opus 4.7 | Catalog writing, wireframes, design judgment |
| Opus subagents | Parallel mechanical edits |
| Haiku 4.5 | Final verification (17 seconds) |

**Use Haiku for verification.** When the question is concrete — does this file exist, does this JSON parse, does grep find this string — Haiku is 10× faster. Tighter loop. It's not about cost. It's about speed.

**The shape:** Opus for judgment. Subagents for anything parallelizable. Haiku for checks. Match model to task, not to project importance.

---

## License

MIT.

## More

Built by [@sksareen](https://github.com/sksareen) with [Claude Code](https://claude.com/claude-code). Originally forged designing [Sauron](https://github.com/sksareen/sauron). Catalog is generic.
