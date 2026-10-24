# Changelog

## Unreleased

- On the desktop app the gate strip no longer runs past its panel and off the screen. Graphical surfaces (desktop, VS Code, mobile) can draw a mark wider than a cell (■ measured about 1.4 cells on the desktop app), so there rows of marks (the gate strip, the inline summary's strip, the other-loops dots) hold fewer marks and still end on the newest. Should a surface draw them wider still, every row of marks, the architect timeline included, is cut at its box. A terminal draws them as before. ([#10](https://github.com/scasella/claude-flightdeck/pull/10), thanks @bhpdev1; also found in [#11](https://github.com/scasella/claude-flightdeck/pull/11) by @darrentmorgan)
- On those surfaces the legend keeps one row of air above the panels, whose borders touched it on the desktop app; the log's row budget counts that row.
- A draw that fails shows `draw failed (…)` in the pane instead of leaving an empty box. A surface module that faults, such as the cut-off `flightdeck: Client hooks/rail.tsx: …` line in the desktop app, is drawn as plain text on that surface for the rest of the session; the other module and other surfaces keep animating. ([#12](https://github.com/scasella/claude-flightdeck/pull/12), thanks @Alendro305; [#7](https://github.com/scasella/claude-flightdeck/issues/7), thanks @NathanAB)
- A subagent resumed with `SendMessage` runs again on its card: ◐ running from its next request, `resumed` in the log, and counted in the status line's `agents N/M`. Its clock still counts from the first spawn. A second spawn under the same id resumes the card rather than adding another. ([#8](https://github.com/scasella/claude-flightdeck/issues/8), thanks @momchilon)
- The context gauge, its `tokens/window` and the status line's `ctx N%` measure against the compaction window when the session compacts in a smaller window than the model's, whether `autoCompactWindow` (global or per model) or Claude Code itself sets it, so the gauge reads against the window the session actually compacts in. The window comes from a local `summary` breakdown (no request sent), read once per model window. ([#9](https://github.com/scasella/claude-flightdeck/issues/9), thanks @DrWBlow)
- `paneColumns` sets the width the docked pane asks for (default 66, at least 40). ([#6](https://github.com/scasella/claude-flightdeck/issues/6), thanks @matheusmaais)
- README: options go under `pluginConfigs["flightdeck@claude-flightdeck"]` in your user settings; `"flightdeck"` and project settings are ignored. ([#13](https://github.com/scasella/claude-flightdeck/issues/13), thanks @jangerhard) Troubleshooting notes that the VS Code extension shows no mod pane yet. ([#5](https://github.com/scasella/claude-flightdeck/issues/5), thanks @jonathon-lawlor798)

## 0.4.0

- The main box shows the time left until each rate-limit window resets (`5h ▰▱▱▱▱ 19% ↻3h10m`), from the `resetsAt` the session already reports. Below 56 columns the gauges stay as they were. ([#3](https://github.com/scasella/claude-flightdeck/pull/3), thanks @vihrea1337)
- The main box shows the last main-loop request's time to first token and decode speed (`last req  ttft 0.8s · 60 tok/s`), timed as its response streams past. ([#1](https://github.com/scasella/claude-flightdeck/issues/1))
- The session log has a one-row gap above it, in both layouts. ([#2](https://github.com/scasella/claude-flightdeck/issues/2))

## 0.3.2

- A background architect's advice is read from its `SubagentHandback` tool call, where the report actually arrives, with the hand-back text as a fallback. Bold markers no longer leak into the advice line.
- README: no longer promises that counters survive every update; a change to the state's shape may reset them once.

## 0.3.1

- The main box shows the model and effort as soon as a request starts, not after the first one finishes.
- Advice from a background architect agent (such as `fable-advisor`) now reaches the architect's `»` line; it arrives as a hand-back message, not as the agent's own answer.
- New README media showing the Flightdeck header; plainer wording about opening on start.
- More gate tests (24 in all).

## 0.3.0

First public release.

- Panels: main vitals (context, compactions, cost, rate limits), architect timeline, permission gate strip with per-family drill-down, agent cards and swimlanes, other loops, turn receipt, session log.
- Layouts: docked one- or two-column, and an 8-row inline summary for the main screen. Cards fall back to swimlanes when they don't fit.
- Theme colours by default, with a `pastel` palette option.
- Animated connectors and live clocks as surface modules, only while work flows.
- Works on the terminal, desktop app, VS Code and mobile surfaces.
- Config for the architect pattern, labels, panels, layout, card limit, motion, moments, palette, opening on start and the status line.
- `/clear` and `/flightdeck reset` start the pane fresh; reads tolerate missing or older fields.
