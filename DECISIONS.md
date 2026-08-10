# Decisions

*This exists so that a settled question stays settled, and so that reopening one
is a deliberate act rather than a slow drift.*

| Date | Question | Decision |
|------|----------|----------|
| 2026-08-10 | How many player roles? | **Two.** Harbour Master and Trader. The Trader owns and maintains the fleet as well as trading the goods |
| 2026-08-10 | Which goods can be traded? | Forty five trade goods, recorded in [design/DESIGN_GOODS.md](design/DESIGN_GOODS.md). Sixty seven since the raw materials tier |
| 2026-08-10 | Are slaves tradeable? | **No.** Historically part of Macao's trade, excluded by decision |
| 2026-08-10 | What is `tom-general`? | Plans, designs, guides, decisions. No code |
| 2026-08-10 | One code library or two? | **One**, `tom-shared`. The rules are part of the contract, so a hazard table and a field name share a version number |
| 2026-08-10 | Application and module naming | App `hecate_tom_shared` agrees with the repo. Modules take the short `tom_` prefix, because they appear at every call site in every service |
| 2026-08-10 | What hazards does the ocean carry? | Travel, storms and pirates. **The word "dragons" is retired** |
| 2026-08-10 | What does a harbour trade? | **Everything.** Every harbour has a market where every good buys and sells at the going price. A harbour declares only what is plentiful there; demand is the complement and is never written down |
| 2026-08-11 | Do goods carry a `jobs` enum? | **No, deleted.** `contraband` is a harbour's decision, `money` is the medium of exchange, `bulk`/`floor`/`trap` are price facts, `exclusive` is derived. Only `fragile` and `perishable` were real, and both want a number, so they return with storms and time |
| 2026-08-11 | How are things named on the mesh? | **MRI**, `mri:class:{realm}/tom/{kind}/{name}`, built with `macula_mri`. World-file names are local and never leave the node as-is. `tom-shared` takes the `macula` dependency; TOM is a mesh application |
| 2026-08-11 | How do peers know they share a world? | **`tom_world:digest/1`**, a sha256 over the world's content. Exchange it, refuse to trade with a peer whose world is not yours |
| 2026-08-11 | `regions` or `origins` on a good? | **`origins`.** A harbour's `region` is where it is; a good's `origins` are where it comes from. Different relations, so different words |
| 2026-08-11 | Do we have ores? | **Two.** Silver ore and gold ore, both refined with Chinese quicksilver. The other six metals crossed oceans as metal, so they get none |
| 2026-08-10 | Are goods and harbours code or data? | **Data.** `tom-shared` owns the map a good is and the map a harbour is. The instances live in `priv/worlds/macao.world`. There is no closed vocabulary left in it |
| 2026-08-10 | Where does it all run? | Ocean on `msi00`, eight harbours two apiece on `beam00` to `beam03`, trader on Raf's workstation. Each harbour dials a different station. See [design/DESIGN_DEPLOYMENT.md](design/DESIGN_DEPLOYMENT.md) |

## 2026-08-10: two player roles, not three

The brief opened with three: Harbour Master, Trader, Ship Master. The Ship Master
is folded into the Trader, who now trades the goods and keeps the boats and ships
that carry them.

**What this buys.** A game needs two humans to start, not three. The hardest
moment in the whole protocol, handing a laden ship across the quay, drops from
three signatures to two, because the ship and the cargo now have the same owner.
And the sharpest decision in the game moves inside one player's head: every
florin put into another hull is a florin not put into another lot.

**What it costs.** The charter market is gone, and with it the negotiation of
freight rates between two strangers, and the clean split between price risk and
hull risk. Those were good, and they needed a third player who might be asleep.

**What is unaffected.** Title and custody stay separate exactly as before. The
Trader holds title to both ship and cargo; custody still moves harbour, ocean,
harbour, and still moves only against the title-holder's signature or a standing
order they pre-signed.

**Moot as a result.** Whether to rename `tom-ship-master`. There is no such repo
and no such role. For the record, the answer to the question that prompted it:
Dutch *rederij* is a shipowning firm, *reder* is a shipowner, and the English
term for the managing role, the party who provisions, repairs, crews and charters
a ship without sailing her, is *ship's husband*. Those functions now belong to
the Trader.

## 2026-08-10: no slaves

Macao's trade included them. They are excluded from the goods, recorded here so
the absence reads as a decision rather than an oversight, and so nobody adds them
back believing they were forgotten.
