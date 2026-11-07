# ShockAtlas

An open atlas of economic exposure to climate and geopolitical shocks.
Website: https://shockatlas.com · MCP server: `https://shockatlas.com/api/mcp` · Not investment advice.

ShockAtlas is a project of H2CO3. This repository documents what ShockAtlas publishes, how it is produced and how to query it. The site's source code is not published here.

## What one signal contains

Each signal documents one shock in one place, for example the Rhine at Kaub falling below the level at which tankers can load, or a cancelled anchovy season in Peru.

- **Three public data series**: one physical (a river gauge, a rainfall total, an ENSO index), one economic (a price, a freight quote), one flow (tonnes shipped, port calls, transits).
- **The mechanism**: a causal chain from the physical event to the economic consequence. Each link is typed (physical, logistical, economic, behavioural), carries a lag in days, and has a status from the data: observed, consistent, untested or contradicted.
- **The organisations on the chain**, each with verbatim public evidence and a sector code (NACE or NAICS).
- **Dated hypotheses** with a threshold on a published series. From November 2026, each hypothesis is reviewed when its date passes and marked confirmed, invalidated or expired; a correction is published as a dated update, and the original stays visible.
- **A reasoning dossier** (constants with source quotes, constraints, alternatives, conditional trajectories) reviewed by an independent counter-analyst. Disagreements are kept, not smoothed over.

Every figure on an edition is recomputed from the published observations when the site is built.

## Classification

Signals are classified in a public tree: **domain › sector › chain**.

| Domain | Sectors |
|---|---|
| Transport | inland waterways, maritime, rail, air, road |
| Energy | gas and LNG, oil products, nuclear, hydropower, wind, solar |
| Agriculture | cereals, tropical crops, farm inputs |
| Animal feed | fishmeal and fish oil, oilseed meals |

A sector with no signal yet is shown as "not covered yet". A chain is added only when a real signal fills it. Signals also cross the tree through shared axes: mechanism, geography (ISO 3166), series family, publisher, organisation sector. The live tree is at https://shockatlas.com/atlas.

## How it is produced

ShockAtlas is run by AI agents, with separate roles that do not see each other's reasoning:

1. **Scout**: picks a shock from the news or from a threshold crossed on a tracked series.
2. **Data collector**: fetches the series from their publishers and records licence, publication and retrieval dates. It writes a data reading before any analysis: if the data do not show the shock, the subject stops or is reframed.
3. **Organisation mapper**: finds the organisations on the chain, with verbatim public evidence.
4. **Analyst**: writes the causal chain, hypotheses and trajectories.
5. **Counter-analyst**: reviews the dossier from the files alone. The review is bounded to two rounds.
6. **Editor** and **QA**: write the edition and check it against the data and the publication rules.

Data rights are checked per series. A series whose licence does not allow redistribution keeps its provenance and its source link, but its observations are withheld for everyone.

## Access

**Free, no key**

- Index: `https://shockatlas.com/api/atlas`
- One signal: `https://shockatlas.com/api/atlas/<signal>`
- A series, JSON or CSV, last 12 observations: `/api/atlas/<signal>/series/<key>`, `/api/atlas/<signal>/csv/<key>`
- Editions, dossiers and organisations as HTML pages, an RSS feed (`/feed.xml`) and `llms.txt`
- The free weekly newsletter: https://shockatlas.com/newsletters (double opt-in)

**MCP server** (streamable HTTP, stateless), listed in the official MCP registry as `com.shockatlas/atlas`.

```
claude mcp add --transport http shockatlas https://shockatlas.com/api/mcp
```

| Tool | Returns |
|---|---|
| `list_signals` | published signals, filterable by domain and sector |
| `get_signal` | one signal: series, figures, hypotheses, organisations |
| `get_edition` | the edition text |
| `get_dossier` | the reasoning dossier (preview without a key) |
| `get_series` | one series (last 12 observations without a key) |
| `get_organisation` | one organisation, with its sector and public evidence |
| `get_offers` | what is free and what is paid |
| `get_export` | the full export of a signal (member key) |
| `subscribe_newsletter` | asks the free weekly for one consenting address (double opt-in); the only write |

## What is for sale

**ShockAtlas Premium, 49 USD per month**, the only paid offer:

- every published analysis, old and new, while the subscription is active;
- three files per analysis, and the full series and dossiers through the API and the MCP with a member key;
- when the subscription ends, access stops; files already downloaded remain the subscriber's.

Details and current limits: https://shockatlas.com/premium

## Contact

hello@shockatlas.com · support@shockatlas.com
