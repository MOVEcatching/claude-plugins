---
name: parent-update
description: Short, warm, plain update for one catcher's parents from that catcher's MOVE sensor data — how often they trained and what improved, against their own past only, never against teammates. Use when a coach asks for a parent update, a note or email to a catcher's family, or "write something for <catcher>'s parents".
argument-hint: "<catcher name> [7|14|30|60|90 days]"
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

# MOVE parent update

Draft a short note from the coach to one catcher's parents: $ARGUMENTS

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

## This one is about one catcher only

- No teammates' names, no team averages, no ranks, no "best on the team". Use `trend` and
  `metric_stats` for **this catcher only** — never `rank_catchers`, never `group: "catcher"`.
- Compare the catcher only with their own past, as the `trend` tool gives it.
- No catcher named → ask which one. Name not on `team_overview` → say MOVE doesn't share that
  catcher here (catchers under 13 aren't included) and stop.

## Steps

1. `list_teams` (ask which team if more than one), then `team_overview` → the catcher's
   catches and sessions in the last 30 days and their last day. Window: what the coach said,
   else `"30"`.
2. `list_sessions` with that `catcher` and `window` → the days they trained.
3. `trend` with that `catcher` and `window` for each launch metric: `gloveSpeed`,
   `verticalSpeed`, `peakAccel`, `peakDecel`, `timeToStick`, `stickDistance`.
4. Pick up to 3 metrics the tool calls **better**, with its "first … → last …" figures.
   Pick at most one the tool calls **worse** as "what we're working on next" — no blame, no cause.
   Too few catches for a trend → say they're just getting started; don't invent progress.
5. Didn't train in the window → a short, warm "we'd love to see them at the next session" note.

## Write it like this

Plain words a parent understands. Name each metric in full, then a few words on what it means:

- Glove Speed thru Wrist — how fast the glove moves to the ball
- Peak Vertical Glove Speed — how fast the glove moves up or down to the ball
- Peak Accel / Peak Decel — how hard the glove speeds up, and brakes after the catch
- Time To Stick — how quickly the glove stops still after the catch (lower is better)
- Stick Distance — how far the glove travels from the catch to the stop (lower is better)

```
Hi <parent or family>,

<Catcher> caught <n> pitches in <n> sessions with the MOVE sensor since <day>.
<One to three sentences: what got better, with the tool's numbers.>
<One sentence: what we're working on next.>

<Coach's sign-off — leave [Coach name] for the coach to fill>
```

80 to 150 words. Warm, not gushing. No links inside the note (dashboard links only open for
the team's coaches). After the draft, on its own line for the coach: if they want to attach a
clip, give one filmed catch's dashboard link to download it from.
