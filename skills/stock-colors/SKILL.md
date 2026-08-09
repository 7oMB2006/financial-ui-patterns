---
name: stock-colors
description: Apply a consistent Chinese-market red-up/green-down magnitude color system to financial dashboards, heatmaps, cards, tables, charts, and numeric labels. Use when the user asks for red涨绿跌, 云图深浅, market heat colors, or visual strength based on absolute value.
---

# Stock Colors

Use this for financial value semantics, not as a mandate to use a treemap or a heatmap layout.

## Direction And Magnitude

- Positive values are red. Start with light pink for small moves and progress to vivid red for large moves.
- Negative values are green. Start with light mint for small moves and progress to vivid green for large moves.
- Zero, unavailable, or incomparable values use neutral foreground or secondary text.
- Normalize magnitude within the user-visible comparison set. Do not compare percentages, money flow, ranks, and scores on one shared scale.
- Prefer a capped reference range or the visible set's robust high percentile so one outlier does not wash out every other value.

Default dark-surface intent:

```ts
const magnitude = Math.min(1, Math.abs(value) / referenceAbs);
const saturation = 48 + magnitude * 46;
const lightness = 72 - magnitude * 18;
const color = value > 0
  ? `hsl(0 ${saturation}% ${lightness}%)`
  : `hsl(158 ${saturation}% ${lightness}%)`;
```

This intentionally produces `+1` as soft pink and `+4` as stronger red, rather than a near-black muted red.

## UI Rules

- Always show the signed number and unit. Color is reinforcement, never the only signal.
- Use text color first for dense tables and cards. Use tinted backgrounds only for tiles or heatmaps where surface area carries meaning.
- A companion value may inherit the primary value's color when it explains that same move. Example: percentage on top, bold `强度 94` directly below.
- Keep labels, sources, timestamps, and unavailable states neutral. Do not color a score merely because it is numerically high unless its direction is explicitly positive or negative.
- Preserve readable contrast on dark surfaces. Validate that low-magnitude pink/mint text remains legible.

## Related Chart Layout

- Use `$financial-chart-end-labels` when financial line-end names or values need collision-aware placement, connector lines, entry/exit annotations, or replay-time labels. This skill defines their colors; that skill defines their spatial layout.

## Validation

Before finishing, check a representative range such as `-4%, -1%, 0%, +1%, +4%` in the actual UI. Confirm stronger absolute moves are visibly more saturated, zero stays neutral, and direction is readable without hue alone.
