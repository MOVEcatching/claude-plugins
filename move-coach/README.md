# MOVE Coach — plugin for Claude and ChatGPT

Your team's MOVE catching-sensor numbers inside your own Claude or ChatGPT, with four ready-made workflows.
It reads the same numbers as the MOVE Coach dashboard. It only reads: nothing it does changes
MOVE or sends anything to anyone.

## Install (Claude Code)

```
/plugin marketplace add MOVEcatching/claude-plugins
/plugin install move-coach@movecatching
```

For a local copy of this folder: `/plugin marketplace add /path/to/ClaudePlugin`.

## Install (ChatGPT)

- **ChatGPT desktop or Codex, with the four skills:** add the marketplace
  (`codex plugin marketplace add MOVEcatching/claude-plugins`), then install **MOVE Coach** from
  the plugins list in the ChatGPT desktop app and sign in when asked.
- **ChatGPT on the web, data only:** the plus button › **Add custom MCP server**, paste
  `https://move-catching-sensor.web.app/mcp`, choose OAuth, then **Create as a plugin**. You get
  your team's numbers but not the four ready-made skills.

Not yet in OpenAI's public plugin directory.

## Connect your team (once)

1. In Claude Code, run `/mcp`, pick **plugin:move-coach:move**, and choose to sign in.
   In ChatGPT, sign in when it asks to connect MOVE.
2. Your browser opens MOVE's connect page. Sign in with your MOVE coach account, tick the
   teams your AI app may read, and press **Allow**.
3. Back in Claude or ChatGPT, ask "list my MOVE teams" to check it worked.

Your team must be on the MOVE Coach plan. You can disconnect at any time on the same connect page
(Team settings on the dashboard links to it). Every lookup is logged where your team's staff can see it.

Catchers under 13 are not shared with Claude or ChatGPT at all.

Already connected MOVE yourself (by hand or as a claude.ai connector)? Claude Code keeps that
connection and skips the plugin's copy, so there's nothing to sign in to again. The skills work
with either.

## The skills

| Command | What you get |
| --- | --- |
| `/move-coach:weekly-team-report [team]` | Who trained in the last 7 days, each catcher's change on the MOVE metrics over two weeks, and standout catches with links to them on the dashboard. |
| `/move-coach:practice-plan [catcher or group] [days] [your drills]` | A plan per catcher or group from the metrics MOVE marks as getting worse, using only the drills you give it. Text only for now. |
| `/move-coach:parent-update <catcher>` | A short, warm note to one catcher's family: how often they trained and what improved, against their own past only — no teammates, no ranks. |
| `/move-coach:recruiting-one-pager <catcher>` | One page of a catcher's typical, top-10% and best MOVE numbers, beta metrics marked "(beta)", and links to their best filmed catches. Stated as sensor readings. |

You can also just ask in plain words ("write a parent update for Alex") and it picks the
right one.

## How the answers are written

- Metrics by their full names (Glove Speed thru Wrist, Peak Vertical Glove Speed, Peak Accel,
  Peak Decel, Time To Stick, Stick Distance); beta metrics say "(beta)".
- Sessions by their day and time; catches with their dashboard link.
- Every average, best and change comes from MOVE's own tools, not the AI's arithmetic.
- No guessed causes, no outside benchmarks.
- Catch links open on the MOVE Coach dashboard and need your coach sign-in. To share a clip
  with a parent or recruiter, download it there.
