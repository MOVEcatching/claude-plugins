---
name: practice-plan
description: Practice plan for a catching coach built from this week's MOVE sensor data — one focus per catcher or group, from the metrics MOVE marks as getting worse, using only the coach's own drills. Use when a coach asks for a practice plan, a week's training plan, "what should my catchers work on", or what to focus on next.
argument-hint: "[catcher or group] [days] [your drills]"
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

# MOVE practice plan

Write a practice plan from this week's MOVE numbers. The coach may name a catcher, a group,
the days, and their drills: $ARGUMENTS

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

## Drills: only the coach's

MOVE's tools here can't read the coach's drill bank. Use only drills the coach gives you (in the
request, or ask once: "Which drills do you use for receiving, sticking and glove speed?").
Never invent a drill, warm-up or rep scheme. No drills given → write the focus and leave a slot:
`[your drill for Time To Stick]`.

## Steps

1. `list_teams` (ask which team if more than one), then `team_overview`. Plan only for catchers
   who caught in the last 14 days; list the rest as "no recent MOVE data".
2. For each launch metric — `gloveSpeed`, `verticalSpeed`, `peakAccel`, `peakDecel`,
   `timeToStick`, `stickDistance`:
   - `trend` with `catcher: "each"`, `window: "14"` → each catcher's change and the tool's
     better / worse / level.
   - `metric_stats` with `window: "7"`, `group: "catcher"` → this week's average.
   12 calls whatever the team's size. A single catcher named → pass their name instead of "each"
   and "catcher", same 12 calls.
3. Each catcher's focus = up to 2 metrics the trend tool calls **worse**. None worse → "Keep
   the current work" and name the metric that improved most in the tool's own words. Don't rank
   metrics by your own sums.
4. Groups: catchers who share a focus metric train together. Say who is in each group.
5. For a speed, accel or decel focus, one catch to watch: `find_catches` for that catcher,
   `window: "14"`, `pick: "highest"`, `count: 10`. Pick a filmed one if there is one; give its
   day and link. No "watch" catch for a Time To Stick or Stick Distance focus — their lowest
   values are soft, short catches, not good models.

## Write it like this

```
MOVE practice plan — <team>, week of <day>

<Group or catcher>: <names>
Focus: <full metric name> — this week <avg>; last two weeks <first> → <last>, worse.
Drills: <coach's drills, or [your drill for <metric>]>
Watch: <catcher>'s catch on <day time> — <link>   (speed / accel / decel focus only)
Check next session: <full metric name> average on the MOVE dashboard.

…

No recent MOVE data: <names>
```

If the coach gave days, lay the plan out day by day instead. No made-up numeric goals — the goal
is to beat this week's average the tool gave.

This version writes text only. A later version of this plugin can save the plan into MOVE as a
Draft program and put it on the team calendar (MOVE tools `draft_program` / `put_on_calendar`,
being built). Don't look for them or wait on them in this version.
