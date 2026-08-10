# hecate-tom-general

**TOM, Traders of Macao.** A trading game played over the Macula mesh, where
ships and their goods move from harbour to harbour by physically migrating
between services.

This repository holds the **plans, designs, guides and decisions**. No code
lives here.

## The shape of the game

Three player roles, each one `hecate-om` service hosted by that player on their
own machine, each serving its own web UI:

| Role | Owns | Plays |
|------|------|-------|
| **Harbour Master** | A harbour | Taxes the market, sells and plans berths, rents storage, repairs ships, and pays to keep lanes open and docks dug |
| **Trader** | Capital and cargo | Buys and sells, forms a trading party, leases storage in harbours |
| **Ship Master** | A ship | Charters her out, provisions her, sets her orders and lets her sail |

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
| `hecate-tom-ship-master` | The Ship Master's service |
| `hecate-tom-ocean` | The world service |

## Documents

| Document | What it settles |
|----------|-----------------|
| [design/DESIGN_GOODS.md](design/DESIGN_GOODS.md) | The goods that can be traded |

## Not related to

`reckon-db-org/reckon_traders_of_macao` shares the name and nothing else. TOM
inherits no rules, no map and no vocabulary from it.
