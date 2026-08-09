---
name: financial-chart-end-labels
description: Design and implement collision-aware endpoint labels for financial line charts. Use when a financial chart needs line-end names, values, connector lines, non-overlapping label placement, entry/exit annotations, or historical replay that fades the future portion of a line.
---

# Financial Chart End Labels

Use this for the end-of-line annotation language of financial charts. Keep it separate from numeric color semantics: obtain label and line colors from `$stock-colors` when red-up/green-down or magnitude color is required.

## Preserve Financial Meaning

- Keep the data point's true value, event, timestamp, and source intact. A visual floor, compressed band, or label displacement must not overwrite the true value.
- Anchor every connector at the final real plotted point. Move only the label, never bend a series to make its label look tidy.
- Keep a line's color and its endpoint label color consistent unless the user asks for a separate state color.
- Do not use color as the only distinction. Retain names, signed values, units, and event markers.

## Place Labels: Strongest Stays Parallel

Apply this default rule: **stronger labels stay parallel; only a later label that overlaps follows downward.**

1. Resolve each visible series' final valid point at the selected or replayed time. Exclude missing points and inactive series.
2. Convert endpoint values to chart coordinates after the chart frame and scale are known. Sort endpoints from higher screen position to lower screen position.
3. Start each label at the same screen Y as its real endpoint.
4. Walk the sorted labels. Preserve the candidate Y if it clears the immediately preceding accepted label by the minimum gap. If it overlaps, move only this label below the preceding accepted label by that gap.
5. Continue the same rule for a collision chain. Do not put all labels in a universal evenly spaced stack when they do not collide.
6. Clamp the collision chain to the plot bounds. If its bottom overflows, shift that collided suffix upward together while preserving gaps. Do not move unrelated labels. If the available height is still insufficient, abbreviate low-priority metadata or omit only the lowest-priority label with an accessible tooltip.
7. Draw a thin connector from the real endpoint to the displaced label. A label that remained parallel needs no artificial offset or connector bend.

Use stable pixel gaps after fonts are chosen. Default to 16–20 px for a compact desktop financial chart; scale only when the actual font size changes. Recompute when the plot height changes, not for every pointer move.

## Stateful Series

Use state annotations only when the product exposes a rotating, selected, or otherwise changing series universe:

- Treat entry, continuity, exit, suspension, and replacement as product-defined states. Let the product supply their marker glyphs and copy; do not hard-code a project-specific emoji vocabulary in this skill.
- Preserve the event-time factual value, change, flow, and source in data and tooltip even when the chart intentionally draws an event marker on a floor or zero axis.
- Do not imply that a series' membership or coverage changed unless the underlying event history says so.

For compressed score charts, retain the raw score in the label and side list. A floor is a display transform, not a claim that every low score equals the floor.

## Replay And Focused Inspection

- At a historical hover or replay time, calculate endpoints from that time, not the latest time.
- Fade the part of each line after the selected time. Do not fade axes, grid, or the historical portion.
- Preserve the same endpoint-label placement algorithm in live and replay states.
- Keep dwell rings, path-reveal animation, lunch breaks, dynamic Y-axis range, and data loading outside this skill. They may coexist with these labels but are independent chart concerns.
- Respect `prefers-reduced-motion`; line-label placement must be correct without animation.

## Validate

Before finishing, verify all of the following in the actual chart:

- Two endpoints that are naturally separated remain parallel to their lines.
- A crowded high-to-low group becomes a minimal downward collision chain with correct connectors.
- The highest label remains at its real endpoint whenever possible.
- Labels stay inside the chart and do not collide with each other, axes, or the right boundary.
- Product-defined state markers match the underlying event history.
- A compressed visual coordinate still exposes the raw factual value in the label or tooltip.
- Historical inspection fades only future line segments and preserves correct labels at the chosen time.
