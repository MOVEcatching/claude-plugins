---
name: recruiting-one-pager
description: Recruiting one-pager for one catcher from MOVE sensor data — typical, top and best numbers on the MOVE metrics, beta metrics labelled beta, and links to their best filmed catches, stated as sensor-measured with no accuracy claims. Use when a coach asks for a recruiting sheet, a profile for college coaches or scouts, or a one-pager for a catcher.
argument-hint: "<catcher name> [90|180|365|all days]"
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

# MOVE recruiting one-pager

Make a one-page profile of one catcher's MOVE numbers: $ARGUMENTS

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

## Honest about what the numbers are

- These are **readings from the MOVE sensor on the catcher's glove**, worked out by MOVE's
  software. Say so on the page. Never call them radar, video or "verified" measurements, and
  never state an accuracy ("±1 mph", "lab-grade", "validated").
- No comparison with college, pro or age-group standards, and no ranks against teammates.
- Lead with "typical" (the median) and "top 10%", not just the single best: one catch is one
  catch.

## Steps

1. `list_teams` (ask which team if more than one), then `team_overview` → the catcher's
   catches, sessions, first and last day. Not listed → say MOVE doesn't share that catcher here
   and stop. Window: what the coach said, else `"all"`.
2. `metric_stats` with that `catcher` and `window`, for `gloveSpeed`, `verticalSpeed`,
   `peakAccel`, `peakDecel`, `timeToStick`, `stickDistance`, and `pocketSpeed`
   (Glove Speed thru Pocket — always "(beta)"). Take the tool's median, top-10% average, best
   and catch count. Leave out Through-the-Ball, Stick Score and Path Efficiency unless the coach
   asks; then mark them "(beta)" too.
3. Clips: `find_catches` with that `catcher` and `window`, `count: 10`, for `gloveSpeed`
   highest and `verticalSpeed` highest. Pick up to 3 **filmed** catches across both lists.
   None filmed → say so; don't link unfilmed catches as clips.

## Write it like this

```
<Catcher> — Catcher, <team>
MOVE glove-sensor data: <n> catches in <n> sessions, <first day> – <last day>

| Metric                          | Typical | Top 10% | Best | Catches |
| Glove Speed thru Wrist (mph)    |         |         |      |         |
| Peak Vertical Glove Speed (mph) |         |         |      |         |
| Peak Accel (g)                  |         |         |      |         |
| Peak Decel (g)                  |         |         |      |         |
| Time To Stick (s), lower better |         |    —    |  —   |         |
| Stick Distance (in), lower better |       |    —    |  —   |         |
| Glove Speed thru Pocket (beta) (mph) |    |         |      |         |

Clips
- <day>: Glove Speed thru Wrist <value> mph — <link>
- …

Measured by the MOVE sensor on the catcher's glove and computed by MOVE's software.
Sensor readings, not radar or video. "Beta" marks a newer metric MOVE is still checking.
```

For Time To Stick and Stick Distance give **Typical only**. Their lowest values come from soft,
short catches (a 1 in Stick Distance is a glove that barely moved), so a "best" there would
mislead a reader. Give each row's own catch count — it differs by metric.

Then, to the coach (not on the page): the clip links open on the MOVE Coach dashboard, for the
team's coaches only. Download a clip there to send it. Share the page with the catcher's and
family's OK.
