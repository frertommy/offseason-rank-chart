# Offseason Rank Index — OFFv1

A self-contained demo that turns the **OFFv1 offseason model** into a trading chart, built on
[TradingView Lightweight Charts](https://www.tradingview.com/lightweight-charts/) (v5). First team: **RB Leipzig** (Bundesliga, 2026-27 offseason).

**Live:** open `index.html`.

## The idea
In the offseason there are no games to settle — a team's index price drifts purely as the market's
**expected league finish** moves. This view makes that legible:

- **Rank ladder** (P1…P7 horizontal rungs) — the rank→price ladder for the team. Each rung is where the
  index sits if the market expects that finishing place. **P4 = the Champions-League cut-off.** The price
  axis effectively becomes a *rank* axis: read finish position straight off where the line sits.
- **Price line** — the live OFFv1 oracle price, drifting as the implied rank moves.
- **One long corridor** to the season's first ball (the **kickoff** divider) — no settlements until then.
- **Ladder / Drift** views — zoom out to the full rank ladder, or in to the day-to-day repricing.

## The underlying
The implied rank is built from **de-vigged consensus across 10+ sharp books + Polymarket/Kalshi**
(the L1→L2→L3 board pipeline), fused across title / top-4 / relegation markets — not an invented fair value.

## How it works
- The rank→price ladder is computed from the team's anchor (`carry_b`, `anchor_rank`, `per_place_idx`) via the
  universal index→USD curve `USD = exp(0.0028781 · idx)`.
- Event-driven oracle ticks are resampled to a uniform 12h grid so the time axis is proportional and the
  long runway to kickoff reads correctly.
- Data is a **static JSON snapshot** (`off-leipzig.json`) — the page runs with no backend.

No build step — plain HTML/CSS/JS plus the Lightweight Charts CDN.
