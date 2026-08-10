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
| **The Ocean** | Distance, season, weather, and where dragons be. Holds ships in transit |

## Repositories

| Repo | Holds |
|------|-------|
| `hecate-tom-general` | This one. Plans, designs, guides, decisions |
| `hecate-tom-shared` | The library every service links: fact schemas, the custody handover, signing, the conservation auditor, goods, price curves, hazard tables |
| `hecate-tom-harbour` | The Harbour Master's service |
| `hecate-tom-trader` | The Trader's service |
| `hecate-tom-ocean` | The world service |

## Documents

| Document | What it settles |
|----------|-----------------|
| [DECISIONS.md](DECISIONS.md) | What has been settled, when, and why |
| [design/DESIGN_GOODS.md](design/DESIGN_GOODS.md) | The goods that can be traded |

## Not related to

`reckon-db-org/reckon_traders_of_macao` shares the name and nothing else. TOM
inherits no rules, no map and no vocabulary from it.
