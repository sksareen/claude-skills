---
name: timeline-patterns
description: Working reference of UX patterns for timeline interfaces — layouts, density, navigation, detail surfaces, filtering. Use when designing or prototyping a timeline, activity feed, history view, or personal memory interface. Returns named patterns with essence, fit, exemplars, tradeoffs, and ready-to-build combinations.
---

# Timeline UX — Pattern Catalog

A working reference for designing timeline interfaces. Patterns are named, atomic, and composable. Pick one from each axis to compose an interface.

Applies to: activity feeds, version history, personal memory tools, observability dashboards, notification inboxes, Git log viewers, chat transcripts, journaling apps, analytics explorers — anything where time is the primary axis.

---

## 0. Mental Model — the Five Axes

Every timeline interface is a choice on these five axes. Name your choice on each before prototyping.

| Axis | Question | Choices |
|---|---|---|
| **Time encoding** | How is time visually represented? | Linear list · Calendar grid · Heatmap · Scrubber · Spiral/semantic |
| **Density** | How much shown per unit of screen? | Dense (log) · Feed · Gallery · Clustered · Summarized |
| **Motion** | How does the user move through time? | Scroll · Scrub · Jump · Play · Zoom |
| **Focus** | What is the primary unit of attention? | Item · Range · Pattern · Session |
| **Intent** | What does the user want? | Recall · Analyze · Relive · Find |

A safe default for most recall/review products: **Linear · Clustered · Scroll+Jump · Session-focused · Recall-primary**. Start there — but the interesting prototypes invert one axis at a time (e.g. keep everything but flip to Scrubber motion).

---

## 1. Core Layout Patterns (Time Encoding)

### 1.1 Reverse-Chronological Feed
**Essence.** Infinite vertical list, newest-first, sticky date headers.
**Data fit.** Homogeneous event stream. Text-dominant.
**When to use.** Recall recent activity. Scan-for-novelty.
**When not.** Pattern-finding over weeks+. User wants range analysis.
**Exemplars.** Slack, iMessage, Twitter, Linear Activity, Superhuman.
**Key knobs.** Sticky headers (day? hour?) · Group-same-type collapse · Unread divider · Pagination vs infinite.
**Opinionated take.** Overused. Ships fast, but collapses all structural information about time into "more scroll = older." Great v0 — do it first, then outgrow it.

### 1.2 Chronological Feed
**Essence.** Same as reverse, but oldest-first. User reads forward in time.
**When to use.** Storytelling / narrative review. "Replay my day."
**Exemplars.** Apple Memories, Day One, Reflect daily notes.
**Opinionated take.** Feels profoundly different from reverse-chron. Matches how we tell stories. Underused in "activity" products — almost everyone defaults to newest-first by reflex.

### 1.3 Calendar Grid (Month / Week / Day)
**Essence.** Time as 2D grid. Days as cells; events placed in cells.
**Data fit.** Scheduled items with duration, or daily aggregates.
**When to use.** Weekly rhythms, recurring patterns, planning.
**When not.** High-frequency events (>20/day renders as a blob).
**Exemplars.** Google Calendar, Fantastical, Cron, Notion Calendar.
**Key knobs.** Month-at-a-glance vs week · Heat encoding in cells · Multi-day spans.

### 1.4 Heatmap Grid
**Essence.** Time as cells, intensity as color. No individual events shown.
**Data fit.** Aggregate count/intensity per time bucket.
**When to use.** Habit tracking, consistency visualization, "where was I active."
**Exemplars.** GitHub contributions, WakaTime, Strava heatmaps.
**Key knobs.** Bucket granularity (hour/day/week) · Color scale (sequential/diverging) · Drill-in on click.
**Opinionated take.** Extremely powerful as a *secondary* view + jump-to-date affordance. Never use alone for a memory tool — it hides every individual moment.

### 1.5 Horizontal Scrubber / Timebar
**Essence.** Horizontal axis = time. User drags a playhead. Content updates as they scrub.
**Data fit.** Dense continuous data (screenshots, logs, videos).
**When to use.** Find a specific moment visually. High-frequency data.
**Exemplars.** Rewind.ai, Final Cut, Datadog APM, Chrome DevTools Performance tab, Figma's prototype player.
**Key knobs.** Thumbnail strip above bar · Snap points for significant events · Multi-resolution (drag = day, ⌘+drag = minute) · Keyboard scrub (←/→).
**Opinionated take.** The killer pattern for screenshot-rich or high-frequency data. Few products have nailed this for personal activity — plenty of room to differentiate here.

### 1.6 Swim Lanes (Multi-Track Timeline)
**Essence.** Horizontal time axis, multiple parallel rows (one per source/type/entity).
**Data fit.** Multiple concurrent streams that need comparison.
**When to use.** "What was happening in system A vs. system B at 3pm?"
**Exemplars.** Chrome DevTools, Perfetto, Datadog trace viewer, Gantt charts, Ableton.
**Key knobs.** Lane grouping strategy · Lane reorder/pin · Crosshair cursor · Zoom both axes.
**Opinionated take.** Underused outside dev tools. Reveals context-switching patterns invisible in any feed layout.

### 1.7 Semantic Zoom / Fractal Timeline
**Essence.** Content representation changes with zoom level. Year → month → day → hour, each with different visual treatment.
**Data fit.** Data that is interesting at multiple scales.
**When to use.** User's intent spans "which year was that?" to "what exactly at 3:17pm."
**Exemplars.** Apple Photos (year/month/day chrome), Mapbox, OrgPad.
**Key knobs.** Visual encoding per zoom level · Smooth vs stepped transitions · What clusters into what.
**Opinionated take.** High effort, high payoff. Apple Photos is the gold standard — study it before attempting. A three-level zoom with distinct renderings at each is worth the build.

### 1.8 Spiral / Non-Linear
**Essence.** Time wrapped (weekly spiral, daily clock, radial).
**When to use.** Emphasize cyclical patterns. Art / data-viz piece.
**Exemplars.** Nicholas Felton reports, some health apps.
**Opinionated take.** Skip for v1. Great for a launch visual, bad as a primary navigator.

---

## 2. Density & Clustering Patterns

### 2.1 Item-per-Row
Dense list, one event per row. Icons + summary + timestamp.
**When.** Homogeneous events, user wants to scan quickly.
**Watch.** Past ~200 items visible without clustering, cognitive load collapses.

### 2.2 Session Clustering
Group contiguous events into "sessions" (gap > N minutes = new session). Collapse each session to a summary + expand-to-see-items.
**When.** Activity is bursty with natural pauses. Perfect fit for activity timelines.
**Exemplars.** Strava auto-splits workouts; Toggl auto-groups by project; Chrome History's time-gap grouping.
**Knob.** Gap threshold (15 min? 30? adaptive?) · Session title (auto-summarized? manual?).

### 2.3 Type Clustering / Merged Runs
Collapse N consecutive events of same type: "[42 clipboard captures]" with disclosure.
**When.** Noisy signal types would overwhelm mixed view.
**Exemplars.** GitHub collapses force-pushes; Slack groups same-user consecutive messages.

### 2.4 Adaptive Summarization
At low zoom, show LLM-generated summary of a time range; at high zoom, show raw items.
**Exemplars.** Apple Journal suggestions, Rewind's "Ask your past" summaries.
**Opinionated take.** Natural fit whenever events are already LLM-tagged or summarizable. Make the summary click → zoom to raw.

### 2.5 Skeletonized Overview
Show *only* significant moments ("peaks") at low zoom. Filter noise.
**When.** Vast event stream, user wants the few things that mattered.
**Knob.** "Significance" scoring — duration? rarity? user-pinned? LLM-judged?

### 2.6 Gallery / Thumbnail Wall
Image-dominant grid ordered by time. Timestamp as caption or hover.
**When.** Data includes screenshots or visual artifacts.
**Exemplars.** Apple Photos, Google Photos, Are.na.
**Opinionated take.** Screenshot-heavy products demand this view. Pair with scrubber for a strong combo.

---

## 3. Navigation Patterns

### 3.1 Infinite Scroll
Load more as user reaches end. Optional pull-to-refresh at top.
**Watch.** Lose scroll position on navigate-away. Anchor state in URL (`?t=1712345678`).

### 3.2 Virtualized Scroll
Render only visible rows. Mandatory above ~5k items.
**Implementation.** `react-virtuoso`, `@tanstack/react-virtual`.

### 3.3 Jump-to-Date
Keyboard-accessible date input + calendar popover. URL-addressable.
**Opinionated take.** Non-negotiable for any timeline with >1 week of data. Missing from 80% of products.

### 3.4 Minimap
Secondary compressed timeline (usually right edge or top) with a viewport rectangle showing current position. Click/drag to jump.
**Exemplars.** VS Code minimap, Figma, Adobe timeline scrubbers.
**Opinionated take.** Underused in web products. High-value anywhere — pair a 1-day heatmap strip at top with main feed below.

### 3.5 Keyboard-First Navigation
`j/k` = next/prev item, `g d` = go-to-date, `/` = search, `?` = help.
**Exemplars.** Superhuman, Linear, GitHub, Arc.
**Opinionated take.** This is the difference between a toy and a tool. For any product users return to daily: essential from day one.

### 3.6 Rewind / Playback
Auto-advance through time at N× speed. Pause/play controls.
**When.** Storytelling, end-of-day review.
**Exemplars.** Apple Memories, Duolingo year-in-review, Spotify Wrapped (story-ified).
**Opinionated take.** Brilliant as a once-a-day trigger ("replay your afternoon") not as the primary UI.

### 3.7 Time-Scoped Chips
Top-of-page chips: `Today · Yesterday · This week · Last week · This month · Custom`. One-click scope switch.
**Exemplars.** Datadog, Grafana, most analytics.

---

## 4. Detail-Surface Patterns (How an Item Reveals)

### 4.1 Inline Expand
Click row → row grows in place, showing full content.
**Pros.** Preserves context. **Cons.** Scroll position shifts.

### 4.2 Master-Detail Split
Two-pane: list on left, detail on right. Row click fills right pane.
**Exemplars.** Superhuman, Linear issue view, Finder.
**Opinionated take.** Strong default for desktop-first products. Weak on mobile/narrow.

### 4.3 Modal / Lightbox
Row click opens overlay. Dismiss with Esc.
**When.** Item is rich (screenshots + metadata + linked items).

### 4.4 Hover Preview
Hovering row reveals inline thumbnail / snippet without committing.
**Exemplars.** GitHub PR hovercards, Arc.
**Opinionated take.** Cheap win. Pairs with any other pattern.

### 4.5 Cmd-Click to Pin
Hold cmd + click row → pin to a side column for comparison.
**Exemplars.** Linear (side-peek), Arc Max compare.
**Opinionated take.** Rare, underappreciated. For a recall tool this is gold — "compare what I was doing on Tuesday vs Wednesday afternoon."

---

## 5. Search & Filter Patterns

### 5.1 Command Palette (Cmd+K)
Global search + navigation. Fuzzy text. Time-scoped with natural-language ("yesterday morning"). Keyboard-first.
**Exemplars.** Raycast, Linear, Notion, Arc.
**Opinionated take.** Table stakes for any tool users will return to.

### 5.2 Faceted Filter Sidebar
Checkboxes / chips for type, source, tag. Count badges per facet.
**Exemplars.** Datadog Log Explorer, Amazon, Linear filter bar.
**Watch.** Clutter. Hide behind a pill that expands.

### 5.3 Token Search Bar
Search bar that parses tokens: `type:clipboard app:Figma since:yesterday`.
**Exemplars.** GitHub issues, Gmail, Jira.
**Opinionated take.** Power-user feature. Ship alongside faceted UI that composes the same tokens — don't force users to memorize them.

### 5.4 Time-Range Brush
Drag on the heatmap/scrubber to select a range; main feed filters to it.
**Exemplars.** Grafana, Datadog, CloudWatch.

### 5.5 Semantic Search
Embedding-based search: "when I was frustrated with the build." Not just keyword.
**Exemplars.** Rewind.ai, Heyday, Mem.
**Opinionated take.** If your data already has embeddings, it's a low-cost, high-magic addition.

### 5.6 Saved Views
Persistent named filters. "My reading," "Code sessions," "Meetings last week."
**Exemplars.** Linear, Jira, Superhuman.

---

## 6. Meta-Patterns for Personal Memory Interfaces

These are patterns specific to recall/memory products like Rewind, Heyday, Day One, and adjacent tools.

### 6.1 The Three Questions Model
Personal memory users ask three things:
1. **"What did I do?"** — summary/recall → cluster view + summarization
2. **"When did I do X?"** — search → palette + semantic search
3. **"What was I doing when X happened?"** — correlation → swim lanes + time-range brush

Every screen should make one of these primary. Don't try to serve all three in one view.

### 6.2 Today / Then / Patterns
Three-tab structure that maps to recall horizons:
- **Today** — last 24h, high detail, feed
- **Then** — jump to any past day, detail view
- **Patterns** — heatmap/aggregate, pattern-finding

Avoids the "one mega-view" trap. Each tab nails one intent.

### 6.3 The Moment Card
A single atomic "moment" — screenshot + context + metadata + linked items. Shareable, permalinkable.
**Opinionated take.** Makes your memory tool *quotable*. A moment-as-a-URL is a strong primitive.

### 6.4 Ambient Presence / Now-Strip
A thin always-visible strip showing "what you're doing right now" — current context, session duration, focus score. Meta-awareness.
**Opinionated take.** If you have live data, surfacing a small strip above the timeline is a free win.

### 6.5 Annotation Layer
User pins / tags / comments on past moments. These become landmarks on the timeline.
**Exemplars.** Marginalia in Roam, Readwise highlights, Sticky notes on dashboards.

### 6.6 Privacy Gutter
Visible indicator per-row of "what was captured" (🖼️ screenshot · 📋 clipboard · ⌨️ keystrokes off). Matters for trust in any capture-heavy tool.

### 6.7 Replay Mode vs Explore Mode
Two fundamentally different sessions:
- **Replay** — passive, narrative, auto-advancing, end-of-day
- **Explore** — active, query-driven, mid-task

Design them as separate entrances, not a mode toggle inside one screen.

---

## 7. Anti-Patterns

Avoid:
- **Flat list with no date anchors.** Scroll into the void.
- **Heatmap as only navigator.** Erases individual moments.
- **Dropdowns for time scoping.** Use chips or calendar popover.
- **Modal-only detail view.** Breaks multi-item comparison.
- **No URL state.** Can't share or reopen a view.
- **Sorting options that aren't chronological.** "Sort by relevance" on a timeline means you broke the timeline.
- **Loading spinners without skeleton.** Timelines feel slow because they're inherently paginated.
- **Mixing micro and macro in one view without zoom.** 30-day view with per-minute rows = unusable.

---

## 8. Ready-to-Prototype Combinations

Each combo is a full interface composed from the patterns above. Build one, use it for a day, decide if it's a keeper, move to the next.

A visual preview of all seven combos is shipped with this skill as `previews.html` — open it in a browser to see them rendered as mockups with sample data.

### Combo A — "Slack for your life"
Reverse-chron feed + session clustering + sticky day headers + master-detail split + Cmd+K palette + keyboard j/k.
**Effort.** Low. **Risk.** Boring but functional. **Good for.** Ship v1 in a day, use as baseline.

### Combo B — "Rewind, done right"
Horizontal scrubber top + thumbnail strip + gallery wall below + scrubber drags gallery position + keyboard ← → scrub + semantic search palette.
**Effort.** Medium. **Risk.** Highest differentiation. **Good for.** The "I know it was around 2pm Tuesday" case.

### Combo C — "Apple Photos for your activity"
Semantic zoom (year → month → day → hour) with distinct renderings per level + gallery at hour-level + feed at minute-level + pinch or ⌘+scroll to zoom.
**Effort.** High. **Risk.** Build cost, but iconic if nailed. **Good for.** Long-term memory ("which week was that?").

### Combo D — "DevTools for yourself"
Swim lanes (one per source) + horizontal time axis + crosshair cursor + click a block to see full detail + top pill chips (Today / Yesterday / This week).
**Effort.** Medium. **Risk.** Information-dense — may feel engineering-y. **Good for.** Pattern-finding, self-audit, productivity coaching.

### Combo E — "Daily review ritual"
Auto-playing replay + voice-over summary + pause to annotate + generates a daily journal draft at end.
**Effort.** Medium (needs summarization). **Risk.** Narrow use case. **Good for.** End-of-day + weekly review + narrative generation.

### Combo F — "Three Questions"
Tabbed: Today (feed) · Then (calendar + master-detail) · Patterns (heatmap + swim lanes). Each tab is a different interface for a different intent.
**Effort.** Medium (it's three screens, not one). **Risk.** Feels like three products. **Good for.** The "don't force one UI to do three things" discipline.

### Combo G — "Scrollytelling"
Chronological (oldest first) feed + auto-scroll button + moments expand inline as they enter viewport + end-of-day "chapter break" cards.
**Effort.** Low-Medium. **Risk.** Novel feel; may confuse users who expect reverse-chron. **Good for.** Storytelling, narrative review, weekly recap.

---

## 9. How to Use This Reference

When the user invokes this skill asking to design something:

1. **Pin the intent first.** Which of the Three Questions (§6.1) is primary? Don't pattern-shop until intent is fixed.
2. **Pick an axis choice (§0) for each of the five.** Name the combination. If it matches a combo in §8, start there.
3. **Prototype one combo end-to-end** before trying a second. Comparing half-built combos is useless.
4. **Instrument what you build.** Which patterns do they actually use? Silent gold is better than loud hypotheticals.
5. **Be opinionated in output.** Don't list options neutrally — recommend. A confident take + a named tradeoff beats a menu.

When proposing a design, structure response as:
- **Intent** (one line)
- **Axis choices** (five bullets)
- **Pattern citations** (§X.Y refs from this skill)
- **Sketch** (ASCII or component tree)
- **What could be wrong with this** (the design-review lens — name one failure mode)

Point the user at `previews.html` (in this skill's directory) if they want to see the seven combos rendered as working mockups.

---

## 10. Adapting to Your Data

The patterns above assume a timeline-shaped data model. Most products fit one of these shapes:

```ts
// Minimum: time + summary
type MinimalEvent = { timestamp: number; summary: string };

// Typed events (activity feeds, logs, history)
type TypedEvent = { timestamp: number; type: string; summary: string };

// Rich events (memory tools, dashboards)
type RichEvent = {
  timestamp: number;
  type: string;
  source?: string;        // which app/system
  summary: string;
  thumbnail?: string;     // for gallery/scrubber patterns
  duration?: number;      // for session clustering
  significance?: number;  // for skeletonized overview
  tags?: string[];        // for faceted filter
  embedding?: number[];   // for semantic search
};

// Aggregates (heatmaps, patterns view)
type Aggregate = {
  bucket: number;         // hour or day epoch
  count: number;
  focusScore?: number;
  breakdown?: Record<string, number>;
};
```

Pattern-to-data mapping:
- **Feed / gallery / session cluster** — works with any event list
- **Heatmap / patterns view** — needs aggregates (cheap to compute)
- **Scrubber with thumbnails** — needs `thumbnail` per event
- **Swim lanes** — needs `source` or `type` for lane assignment
- **Semantic search** — needs `embedding` per event
- **Adaptive summarization** — needs either LLM-on-the-fly or pre-computed summaries per time range

If your data doesn't have a field a pattern wants, either compute it (often cheap — a significance score can just be `duration × rarity`) or choose a different pattern. The five axes in §0 are deliberately orthogonal so you can rebuild without replacing the whole interface.
