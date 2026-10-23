# MOVE plugins

Plugins from [MOVE](https://movecatching.com), the catching sensor, for coaches' own AI.

| Plugin | What it does |
| --- | --- |
| [MOVE Coach](move-coach/) | Your team's MOVE numbers in Claude or ChatGPT: weekly team report, practice plan, parent update, recruiting one-pager. Read-only. |

**Claude Code**

```
/plugin marketplace add MOVEcatching/claude-plugins
/plugin install move-coach@movecatching
```

**ChatGPT desktop / Codex**

```
codex plugin marketplace add MOVEcatching/claude-plugins
```

Then install MOVE Coach from the plugins list. Setup and sign-in: [move-coach/README.md](move-coach/README.md).

Your team must be on the MOVE Coach plan. This repository is published from MOVE's own repo; changes made here directly are overwritten.
