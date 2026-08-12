# hecate-tom-general

**TOM, Traders of Macao.** A trading game played over the Macula mesh, where
ships and their goods move from harbour to harbour by physically migrating
between services.

This repository holds the **plans, designs, guides and decisions**. No code
lives here.

## The shape of the game

Three roles, and **one thing to install**. A player runs `hecate-tom-house` on
their own machine and it serves one web UI.

| Role | Power | Fixed or mobile |
|------|-------|-----------------|
| **Magnate** | Makes. Builds works at a home port, buys inputs and sells outputs there | Fixed |
| **Trader** | Moves. Owns ships, carries goods between ports, profits on the difference across space | Mobile |
| **Mayor** | Permits. Bans, charters, quarantine, public works. Elected by the magnates of a port | Fixed |

**The magnate makes, the trader moves, the mayor permits.** Each needs the
others: a factory strangles itself unless somebody ships inputs in and outputs
out, and a trader has nothing worth sailing for unless somebody is turning cheap
things into dear ones. See [design/DESIGN_ROLES.md](design/DESIGN_ROLES.md).

Plus the world, which no player owns and which is always on:

| Service | Is |
|---------|-----|
| **The World** | What exists: goods, ports, regions, recipes. Append-only |
| **A Harbour** | One port's market, and its elections. One service per port |
| **The Ocean** | Distance, weather, storms and pirates. Holds ships in transit |

## Repositories

| Repo | Holds |
|------|-------|
| `hecate-tom-general` | This one. Plans, designs, guides, decisions |
| `hecate-tom-world` | What exists, and one of the places in it. One binary, run once per place. Always on, owned by nobody |
| `hecate-tom-player` | The person. Magnate, trader and mayor in one install, driven by a page or by a policy |
| `hecate-tom-ocean` | Travel, weather, storms and pirates. Holds ships in transit. **Dissolves** into the two above, see [DESIGN_VOYAGE.md](design/DESIGN_VOYAGE.md) |

**The world runs places. The player runs people.** One service per **owner**,
applied all the way: what nobody owns and must not go dark is one binary, what a
person owns and may switch off is the other. Executed 2026-08-13; the ocean is
the last piece and goes when the voyage lands. See
[DESIGN_TWO_SERVICES.md](design/DESIGN_TWO_SERVICES.md).

**There is still no shared library**, and the rule now sits on the boundary it
was written for. A player links `macula` and nothing of ours, because a player
upgrades when they feel like it and a new good must not mean eight people
redeploy on the same afternoon. A place is not a laptop: it is one of eight
instances under watchtower, owned by the steward, so between the world's data and
a port's market there is no boundary left for the rule to police.

## Documents

| Document | What it settles |
|----------|-----------------|
| [DECISIONS.md](DECISIONS.md) | What has been settled, when, and why |
| [design/DESIGN_TWO_SERVICES.md](design/DESIGN_TWO_SERVICES.md) | The world runs places, the player runs people, and a player can be a bot |
| [design/DESIGN_ROLES.md](design/DESIGN_ROLES.md) | Magnate, trader, mayor, and why they are one install |
| [design/DESIGN_PLACES.md](design/DESIGN_PLACES.md) | Waypoints, routes, and the forts that could hold them |
| [design/DESIGN_MARKET.md](design/DESIGN_MARKET.md) | The price mechanism, what the probes found, and why the world is half flat |
| [design/DESIGN_LOSS.md](design/DESIGN_LOSS.md) | What a wreck costs, and insurance |
| [design/DESIGN_MONEY.md](design/DESIGN_MONEY.md) | Where money comes from, where it goes, and why tax alone drains the world |
| [design/DESIGN_WORLD.md](design/DESIGN_WORLD.md) | What the world service owns, and the nine events it emits |
| [design/DESIGN_GOODS.md](design/DESIGN_GOODS.md) | The goods that can be traded |
| [design/DESIGN_HARBOURS.md](design/DESIGN_HARBOURS.md) | The eight harbours and the routes between them |
| [design/DESIGN_FACTORIES.md](design/DESIGN_FACTORIES.md) | Factories, recipes, and recipes as cargo |
| [design/DESIGN_DEPLOYMENT.md](design/DESIGN_DEPLOYMENT.md) | Which service runs on which box, dialling which station |

## Not related to

`reckon-db-org/reckon_traders_of_macao` shares the name and nothing else. TOM
inherits no rules, no map and no vocabulary from it.
