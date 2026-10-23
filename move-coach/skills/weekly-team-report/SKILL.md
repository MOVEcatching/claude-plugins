---
name: weekly-team-report
description: Weekly MOVE report for a catching coach — who trained in the last 7 days, each catcher's change on the MOVE launch metrics, and standout catches with their dashboard links. Use when a coach asks for a weekly report, a week recap, "how did my catchers do this week", or a team summary from MOVE.
argument-hint: "[team name]"
allowed-tools:
  - mcp__plugin_move-coach_move__list_teams
  - mcp__plugin_move-coach_move__list_metrics
  - mcp__plugin_move-coach_move__team_overview
  - mcp__plugin_move-coach_move__list_sessions
  - mcp__plugin_move-coach_move__session_numbers
  - mcp__plugin_move-coach_move__catch_numbers
  - mcp__plugin_move-coach_move__metric_stats
  - mcp__plugin_move-coach_move__trend
  - mcp__plugin_move-coach_move__rank_catchers
  - mcp__plugin_move-coach_move__find_catches
  - mcp__move__list_teams
  - mcp__move__list_metrics
  - mcp__move__team_overview
  - mcp__move__list_sessions
  - mcp__move__session_numbers
  - mcp__move__catch_numbers
  - mcp__move__metric_stats
  - mcp__move__trend
  - mcp__move__rank_catchers
  - mcp__move__find_catches
---

# MOVE weekly team report

Write the coach a one-page report on the last 7 days, from the MOVE tools only.
Team (optional): $ARGUMENTS

## MOVE rules — follow every one

- **Tools.** The MOVE server's read-only tools: `list_teams`, `team_overview`, `list_sessions`,
  `metric_stats`, `trend`, `find_catches`, `catch_numbers`, `session_numbers`, `rank_catchers`,
  `list_metrics`. If they aren't connected, tell the coach to connect MOVE and sign in
  (Claude Code: run `/mcp`, pick MOVE; ChatGPT: turn on the MOVE Coach plugin and sign in when asked).
- **Full metric names**, exactly as the tools write them: Glove Speed thru Wrist, Peak Vertical
  Glove Speed, Peak Accel, Peak Decel, Time To Stick, Stick Distance. Never a key (`gloveSpeed`)
  or a short tag ("Vert", "TTS"). A beta metric always says "(beta)".
- **Sessions by day and time** ("Thu Oct 22, 8:23 pm"). Never "S1", "S17": those numbers shift
  every time a new session uploads.
- **Every catch you point to gets its link**, pasted exactly as the tool gave it.
- **The tools do the maths.** Averages, medians, bests, changes and "better/worse/level" come from
  the tools. Don't average, subtract, round differently or rank anything yourself. No tool gave a
  change → don't state one.
- **Never guess a cause.** Say what the numbers show, not why ("tired", "footwork", "the pitcher").
  No outside benchmarks, college or pro comparisons, research, or health advice.
- **Like with like.** A tiny Time To Stick or Stick Distance can come from a soft, short move. Give
  that catch's Glove Speed thru Wrist beside it (from `catch_numbers`).
- **Under 13.** Catchers under 13 aren't in MOVE's tools. If the coach names someone who isn't on
  `team_overview`, say MOVE doesn't share that catcher here. Don't look for them another way.
- **Plain and short.** Short sentences. No "standard deviation", "spread" or "variance" — say how
  much it swings. No filler.
- **Read-only.** Nothing here is saved to MOVE or sent to anyone.

## Steps

1. `list_teams`. More than one team and none named → ask which. Then `team_overview`.
   From it: who caught in the last 7 days (catches, sessions) and who didn't (their last day).
2. `list_sessions` with `window: "7"` → the days each catcher trained.
3. For each launch metric — `gloveSpeed`, `verticalSpeed`, `peakAccel`, `peakDecel`,
   `timeToStick`, `stickDistance`:
   - `metric_stats` with `window: "7"`, `group: "catcher"` → this week's average and best.
   - `trend` with `catcher: "each"`, `window: "14"` → the change over the last two weeks: the
     tool's "first … → last …" figure and its better / worse / level.
   That is 12 calls whatever the team's size. Don't call per catcher.
4. Report a change only for catchers who caught this week. If `trend` says too few catches, or
   "all within 1 day", write "not enough catches to call a change".
5. Standouts: `find_catches` with `window: "7"`, `count: 5` for `gloveSpeed` highest and
   `verticalSpeed` highest. Up to 4 standouts in all, filmed ones first (their link opens the
   clip); say "not filmed" on the others. Don't pick standouts on Time To Stick or Stick Distance:
   their lowest values in a week are soft, short catches.

Leave out Catch Position and Stick Position (the tools don't summarise them) and the hidden beta
metrics (Through-the-Ball, Stick Score, Path Efficiency, Glove Speed thru Pocket) unless the coach
asks; then label them "(beta)".

## Write it like this

```
MOVE weekly report — <team>, <first day>–<today>

Trained: <name> — <n> catches in <n> sessions (<days>). …
Didn't train: <name> (last caught <day>). …

<Catcher>
- Glove Speed thru Wrist: <avg> mph this week, best <best>. Last two weeks: <first> → <last>, <better/worse/level>.
- … one line per launch metric. Time To Stick and Stick Distance: average only, no "best"
  (their lowest values come from soft, short moves).

Standout catches
- <Catcher>, <day time>, Catch <n>: Glove Speed thru Wrist <value> mph — <link>
- …

Next: <one step for the coach, starting with a verb>
```

One block per catcher who trained. No team ranking unless the coach asks (then use
`rank_catchers`, and say who has too few catches to rank). Under 300 words for a small team.
