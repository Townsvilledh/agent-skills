# Token Launch Radar

**Description:** Ranks pre-token DeFi protocols by implied value and produces a farm plan for each. Point it at a DefiLlama protocol snapshot and it scores every rankable pre-token protocol with one deterministic function — no protocol is special-cased — and writes a ranked board (`board.json`) plus a web dashboard.

## When to use this skill

Use it when the user wants to know which protocols that have **not yet launched a token** are worth attention or farming, ranked by what they might be worth at launch. Typical asks: "which pre-token protocols are undervalued?", "build me a watchlist of upcoming token launches", "rank these protocols by implied value".

## What it does

1. Reads a DefiLlama snapshot (a JSON file with the protocol list and a watchlist) that you supply.
2. For every pre-token protocol, prices its **implied value from live-token peers in its own category**: the median market-cap/TVL of the live protocols in that category, read from the same snapshot at run time.
3. Combines that peer price with the protocol's TVL, seven-day growth, how long it has run with no token on record, and how many chains it runs on.
4. Sets wrapped, staked and bridged products of tokens that already trade aside, so a bridge never outranks a genuine launch.
5. Writes the ranked board and a dashboard with a farm plan for each protocol.

Because the same function scores every row and prices come from the snapshot itself, running it on a later snapshot re-prices the whole board from that snapshot's own market.

## Requirements

- Node.js 22 or later. Standard library only — nothing to install.
- A snapshot JSON file to score. The run makes **no network calls**: fetch the snapshot first (for example from DefiLlama's public protocol data), then run the radar on the file.
- The bundled `scripts/` folder, kept together (the program reads its `dashboard/` and `screenshots/` folders).

## How to run it

```sh
mkdir -p out
MAKEFUN_OUTPUT_DIR=out node scripts/main.ts --input <snapshot.json>
```

Outputs, written to `out/`:

- `board.json` — the ranked rows (on the author's reference snapshot: 198 rows — the full 40-protocol watchlist plus every other rankable pre-token protocol).
- `data.js` and `dashboard/` — the web dashboard presenting the board, with a farm plan per protocol.
- `dossier.json` — a build record of the run.

The run is deterministic: the same snapshot always writes the same bytes, so two runs agree exactly.

## Presenting results

- Lead with the top rows: name, category, TVL, implied value, and the farm plan.
- Always state which snapshot date the board was priced from — implied values are only as current as the snapshot.
- Never present implied value as a prediction or a price target. It is a peer-relative ranking signal: what a protocol would be worth if it were valued like the live median of its own category.

## Limits

- It ranks; it does not verify that a protocol will launch a token, run an airdrop, or reward farmers. Say so when the user treats the board as a guarantee.
- Protocols whose category has no live-token peers cannot be peer-priced and are handled by the model's own rules, not by a guess.
- See `reference/methodology.md` for the full scoring method.
