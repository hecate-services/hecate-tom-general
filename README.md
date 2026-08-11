# hecate-tom-general

**TOM, Traders of Macao.** A trading game played over the Macula mesh, where
ships and their goods move from harbour to harbour by physically migrating
between services.

This repository holds the **plans, designs, guides and decisions**. No code
lives here.

## The shape of the game

Two player roles, each one `hecate-om` service hosted by that player on their
own machine, each serving its own web UI:

| Role | Owns | Plays |
|------|------|-------|
| **Harbour Master** | A harbour | Taxes the market, sells and plans berths, rents storage, repairs ships, and pays to keep lanes open and docks dug |
| **Trader** | Capital, cargo and hulls | Buys and sells, and keeps the fleet of boats and ships that carries it |

The Trader carries both risks at once: what the cargo fetches, and what the hull
costs to keep afloat. Every florin put into another hull is a florin not put
into another lot, which is the tension the role is built on.

Plus the world, which no player owns:

| Service | Is |
|---------|-----|
| **The Ocean** | Distance, weather, storms and pirates. Holds ships in transit |

## Repositories

| Repo | Holds |
|------|-------|
| `hecate-tom-general` | This one. Plans, designs, guides, decisions |
| `hecate-tom-world` | Owns reference data: goods, harbours, recipes, regions. Publishes facts. Linked by nobody |
| `hecate-tom-harbour` | The Harbour Master's service |
| `hecate-tom-trader` | The Trader's service |
| `hecate-tom-ocean` | Travel, weather, storms and pirates. Holds ships in transit |

**There is no shared library.** One service owns a fact and the others consume
it. A shared domain model would couple every service to one shape and would mean
every player upgrading in lockstep to learn about a new good, which is exactly
what the mesh is supposed to avoid. What a service links is `macula`, like any
other client, and nothing of ours.

## Documents

| Document | What it settles |
|----------|-----------------|
| [DECISIONS.md](DECISIONS.md) | What has been settled, when, and why |
| [design/DESIGN_WORLD.md](design/DESIGN_WORLD.md) | What the world service owns, and the fifteen events it emits |
| [design/DESIGN_GOODS.md](design/DESIGN_GOODS.md) | The goods that can be traded |
| [design/DESIGN_HARBOURS.md](design/DESIGN_HARBOURS.md) | The eight harbours and the routes between them |
| [design/DESIGN_FACTORIES.md](design/DESIGN_FACTORIES.md) | Factories, recipes, and recipes as cargo |
| [design/DESIGN_DEPLOYMENT.md](design/DESIGN_DEPLOYMENT.md) | Which service runs on which box, dialling which station |

## Not related to

`reckon-db-org/reckon_traders_of_macao` shares the name and nothing else. TOM
inherits no rules, no map and no vocabulary from it.
