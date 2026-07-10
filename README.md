# Strike Wings — The Sundering War

The authoritative backend of Strike Wings' **shared season war**. A GitHub
Action here advances the official war state every six hours and publishes
it for every game client — and for the live map at
https://strike-wings-games.github.io/war/.

## Published files (GitHub Pages)

- `current.json` — pointer: `{season, path, tickIndex, stateHash,
  generatedAtEpoch, winner, endEpoch, seasonOver}`
- `<SEASON>/war_state.json` — the official state clients fetch via
  ISteamHTTP (schema `strikewings.warshared/v1`; embeds the war, the
  absorbed player totals, and a self-check hash the client verifies)

## How it works

Every six hours the `war-tick` workflow builds the deterministic war
engine from the game's source, folds the season leaderboard through its
validation and per-player budgets, advances the war one step, and commits
only the two public files above. Its private working state persists
between runs in the Actions cache — never in this tree, never on Pages.

Ended seasons stay published as frozen monuments under their season
directory.
