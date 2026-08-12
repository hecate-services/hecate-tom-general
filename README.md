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
| `hecate-tom-world` | Owns reference data: goods, harbours, recipes, regions. Publishes facts. Linked by nobody |
| `hecate-tom-harbour` | One port's market and elections. Infrastructure, owned by nobody |
| `hecate-tom-house` | The player's service. Magnate, trader and mayor in one install |
| `hecate-tom-ocean` | Travel, weather, storms and pirates. Holds ships in transit |

**One service per owner, not one service per role.** World, harbour and ocean
are separate because different parties own them and they must stay up. Magnate,
trader and mayor are one person's stuff on one laptop, so they are one service.

**There is no shared library.** One service owns a fact and the others consume
it. A shared domain model would couple every service to one shape and would mean
every player upgrading in lockstep to learn about a new good, which is exactly
what the mesh is supposed to avoid. What a service links is `macula`, like any
other client, and nothing of ours.

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
