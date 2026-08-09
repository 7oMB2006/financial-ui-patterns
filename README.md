# Financial UI Patterns

<p align="right">
  English · <a href="./README.zh-CN.md">简体中文</a>
</p>

<p align="center">
  <img src="./assets/readme/hero.svg" width="100%" alt="Financial UI Patterns: personal design patterns for market data interfaces, showing value semantics and collision-aware line-end labels.">
</p>

<p align="center">
  Personal frontend design patterns and Codex skills distilled from my own financial product work.
</p>

<p align="center">
  <a href="#included-skills">Skills</a> · <a href="#install-for-codex">Install</a> · <a href="#principles">Principles</a>
</p>

<p align="center">
  <img src="./assets/readme/personal-oc-notes.gif" width="160" alt="The author's original character holding a notebook.">
</p>

## What This Holds

A small, growing set of reusable decisions for financial interfaces: how values carry directional meaning, and how dense charts keep their final labels readable without corrupting the underlying market facts.

This is not a product codebase, market-data source, trading system, or investment advice.

## Included Skills

### [`stock-colors`](./skills/stock-colors)

**Make financial values readable at a glance.** Defines Chinese-market red-up/green-down magnitude semantics for values, labels, tables, heatmaps, and charts. Small moves stay soft; stronger moves become more vivid without turning low-magnitude values muddy.

<p align="center">
  <img src="./assets/readme/stock-colors-example.png" width="100%" alt="A financial theme panel where large gains use deep red, small gains use light red, and declines use progressively stronger green.">
</p>


### [`financial-chart-end-labels`](./skills/financial-chart-end-labels)

**Keep the end of a line truthful and legible.** Defines collision-aware endpoint labels, real-point connectors, compact collision chains, state annotations, and replay-time behavior. The strongest line stays parallel; only labels that would overlap follow downward.

<p align="center">
  <img src="./assets/readme/financial-chart-end-labels-example.png" width="100%" alt="A market fund-flow chart whose line-end labels retain real endpoints, use connectors, and form compact collision-aware label groups.">
</p>


## Design Boundary

The skills are deliberately complementary:

| Concern | Skill | Rule of thumb |
| --- | --- | --- |
| What a value's color means | [`stock-colors`](./skills/stock-colors) | Color reinforces a signed number and its unit. |
| Where a line-end label belongs | [`financial-chart-end-labels`](./skills/financial-chart-end-labels) | Move labels, not market data or curve geometry. |

## Install For Codex

~~~bash
git clone https://github.com/7oMB2006/financial-ui-patterns.git
cp -R financial-ui-patterns/skills/stock-colors ~/.codex/skills/
cp -R financial-ui-patterns/skills/financial-chart-end-labels ~/.codex/skills/
~~~

On Windows PowerShell, use `Copy-Item -Recurse` in place of `cp -R`. Reload Codex after installation so it discovers the skill folders.

## Principles

- Derive rules from real financial-product implementation work, then abstract them so they remain portable.
- Keep product names, private data, endpoints, and application-specific conventions out of reusable skills.
- Treat a financial interface as an explanation surface: show signed values, units, timestamps, source state, and unavailable data explicitly.
- Prefer interaction and visual rules that preserve market facts over decorative visual effects.

## License

Released under the [MIT License](./LICENSE).
