# Live-service event archetypes: a coded catalog of 1,403 events in four games

This dataset accompanies the manuscript "Event Archetypes Across Four Live-Service Games: Activity Trajectories and Player-Level Churn" (under review at IEEE Transactions on Games; authors anonymized for review).

It contains every live-service event that *Destiny 2*, *Dota 2*, *PUBG*, and *World of Warships* announced between January 1, 2024 and December 31, 2025, coded by two independent coders on six design attributes under one written coding scheme. The joint combination of the six attributes is the event's *archetype*.

| Game | Records |
|---|---|
| Destiny 2 | 287 |
| Dota 2 | 61 |
| PUBG | 338 |
| World of Warships | 717 |
| Total | 1,403 |

## Files

| File | Rows | Contents |
|---|---|---|
| `events.csv` | 1,403 | One row per event record: dates, name, six coded attributes, archetype id |
| `archetypes.csv` | 41 | The 40 named archetypes (attribute combinations) plus the pooled `arch_other` class |
| `README.md` | | This file: column definitions, coding rules, reliability, license |
| `LICENSE` | | CC BY 4.0 |

Both CSV files are UTF-8 with a header row and comma separators.

## `events.csv` columns

| Column | Type | Meaning |
|---|---|---|
| `game` | text | `Destiny 2`, `Dota 2`, `PUBG`, or `World of Warships` |
| `event_id` | text | Unique record id. The prefix gives the game: D, E, P, W |
| `event_name` | text | Title recorded during coding. 969 of the 1,403 names are in Korean, as recorded from the announcement used |
| `start_date` | date | First day the event is active (YYYY-MM-DD) |
| `end_date` | date | First day the event is no longer active. The active span is `start_date` up to, but not including, `end_date` |
| `duration_days` | integer | `end_date` minus `start_date` in days |
| `event_cycle` | text | `Seasonal` during school vacation periods, otherwise `NonSeasonal`. Not used in the manuscript |
| `concurrent_events` | integer | Number of the game's other events active at the start. Not used in the manuscript |
| `participation_type` | text | `Login`, `Active` |
| `monetization` | text | `Free`, `Paid` |
| `event_type` | text | `Esports`, `Collab`, `Anniversary`, `CashShop`, `Balance`, `Season`, `NewContent`, `Existing`, `Social`, `Promo`, `CurrencyEvent` |
| `player_behavior` | text | `Login`, `Mission`, `Stream`, `OutGame`, `Purchase` |
| `reward_type` | text | `Skin`, `Currency`, `Pass`, `Gacha`, `Lottery`, `Goods`, `None` |
| `effort_level` | text | `High`, `Mid`, `Low` |
| `archetype_id` | text | `arch_01` to `arch_40`, or `arch_other` |

## `archetypes.csv` columns

| Column | Meaning |
|---|---|
| `archetype_id` | `arch_01` to `arch_40`, then `arch_other` |
| `participation_type` to `effort_level` | The six attribute values that define the archetype, in the same order as `events.csv` |
| `n_records` | Number of event records with this archetype across the four games |
| `n_games` | Number of games in which the archetype occurs |

The 1,403 records contain 156 distinct attribute combinations. The 40 most frequent, ranked by the number of game-days on which at least one event of the combination was active, are named `arch_01` to `arch_40` and cover 1,187 records (84.6%). The remaining 116 combinations, 216 records, are pooled as `arch_other`.

## Coding scheme

A record is a distinct live-service intervention or player-facing offering that the publisher identified separately in an announcement, news post, or patch note: seasonal events, content releases, balance updates, promotions, collaborations, esports-related activities, and other operational events.

### Attribute definitions and decision rules

**Participation Type.** The action needed to obtain the event's reward. `Login`: the reward is obtainable by logging in alone. `Active`: any further in-game action is required (matches, missions, purchases).

**Monetization.** `Paid` if the event includes any paid component (a purchase requirement, a paid track, or a paid item); `Free` otherwise.

**Event Type.** The category of the event. `Collab` takes precedence over every other category. `NewContent`: new maps, modes, characters, or items are added. `Existing`: the event reuses existing content. `CurrencyEvent`: the event is built around earning or exchanging an existing in-game currency. `Promo` was applied as labelled in the source announcement and carries no additional rule. The other categories are `Esports`, `Anniversary`, `CashShop`, `Balance`, `Season`, and `Social`.

**Required Player Behavior.** The player action required to participate. `Login`: logging in only. `Mission`: completing in-game tasks. `Stream`: watching designated streams (drops). `OutGame`: actions outside the game client, such as external sites or social-media sharing. `Purchase`: buying. Events almost always require one behavior; the coded value is that behavior.

**Reward Type.** The reward obtainable through participation. `Gacha`: in-game probabilistic boxes. `Lottery`: a draw among participants. `Goods`: physical merchandise. `None`: no reward (for example, balance updates). The other categories are `Skin`, `Currency`, and `Pass`.

**Effort Level.** The participation demand. `High`: requires placing within a ranked threshold. `Mid`: requires completing in-game activities. `Low`: no play task is required (login, check-in, or a purchase alone). By convention, reward-less gameplay updates such as balance patches are coded `Mid`, because engaging with them means playing the changed content; 68 of the 70 such records follow this convention.

### Record-level rules

1. An announcement that describes several events with different start or end dates, or several distinct rewards, is split into one record per event or reward. A login reward and a mission reward announced together are recorded separately.
2. The two coders coded every record independently and resolved disagreements by re-reading the original announcement or patch note together until they agreed. No third adjudicator was used.

### Inter-coder reliability

Cohen's kappa between the two coders, pooled across the 1,403 records:

| Attribute | Kappa | Agreement |
|---|---|---|
| Participation Type | 1.000 | 100.0% |
| Monetization | 1.000 | 100.0% |
| Event Type | 0.987 | 98.9% |
| Required Player Behavior | 0.990 | 99.2% |
| Reward Type | 0.983 | 98.8% |
| Effort Level | 0.985 | 99.2% |

Coding followed the written decision rules above, so kappa measures the consistency of rule application rather than free judgment.

## Sources and what is not included

Event records were built from each publisher's official announcements, news posts, and patch notes. Event names and dates are factual metadata of those public announcements.

The manuscript also uses two data sources that are not redistributed here:

- Daily average concurrent players from SteamDB (the "Average Players" field). These can be obtained from SteamDB directly.
- Player-level activity logs from the Bungie API (*Destiny 2*) and the OpenDota API (*Dota 2*). These are not released; the manuscript describes how the cohorts were built.

## License and citation

The dataset is released under the Creative Commons Attribution 4.0 International license (CC BY 4.0); see `LICENSE`.

Citation: the manuscript is under review. A full citation will be added on acceptance.
