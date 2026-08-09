# Financial UI Patterns

Personal frontend design patterns and Codex skills distilled from my own financial product work, covering market data visualization, chart interactions, and financial UI semantics.

This repository captures reusable interface decisions, not a product codebase, market-data source, trading system, or investment advice.

## Included Skills

| Skill | Focus |
| --- | --- |
| [`stock-colors`](./skills/stock-colors) | Chinese-market red-up/green-down magnitude semantics for financial values, tables, heatmaps, charts, and labels. |
| [`financial-chart-end-labels`](./skills/financial-chart-end-labels) | Collision-aware line-end labels, connectors, state annotations, and replay-time endpoint behavior for financial line charts. |

## Design Boundary

Use the two skills together without merging their responsibilities:

- `stock-colors` defines what a financial value's color means.
- `financial-chart-end-labels` defines where a line's final label belongs and how it avoids collisions.

Both preserve factual values and readable labels. Neither should make a chart look tidier by changing the underlying data or bending a series.

## Install For Codex

Clone the repository, then copy the skills you want into your local Codex skills directory:

```bash
git clone https://github.com/7oMB2006/financial-ui-patterns.git
cp -R financial-ui-patterns/skills/stock-colors ~/.codex/skills/
cp -R financial-ui-patterns/skills/financial-chart-end-labels ~/.codex/skills/
```

On Windows PowerShell, use `Copy-Item -Recurse` in place of `cp -R`. Reload Codex after installation so it discovers the new skill folders.

## Principles

- Derive rules from real financial-product implementation work, then abstract them so they remain portable.
- Keep product names, private data, endpoints, and application-specific conventions out of reusable skills.
- Treat financial UI as an explanation surface: show signed values, units, timestamps, source state, and unavailable data explicitly.
- Prefer interaction and visual rules that preserve market facts over decorative visual effects.

## License

Released under the [MIT License](./LICENSE).
