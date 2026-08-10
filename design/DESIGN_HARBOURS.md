# The harbours

*This exists so a trader has somewhere to sail to, and a reason to prefer one
place over another.*

**Status:** agreed 2026-08-10. A pool of twenty nine, of which eight play.

**Encoded in:** `hecate-tom-shared/priv/worlds/macao.world`, which is the
authority for what exists. This document carries the reasoning.

Each playing harbour is one `hecate-tom-harbour` service run by a player. Which
box it runs on and which station it dials are arbitrary and have nothing to do
with where it sits in the game. See [DESIGN_DEPLOYMENT.md](DESIGN_DEPLOYMENT.md).

## The pool

Twenty nine harbours, so that a game is a **selection** rather than the whole
world. Adding one is an edit to the world file.

| Region | Harbours |
|---|---|
| `china` | Macao |
| `japan` | Nagasaki, Hirado |
| `southeast_asia` | Malacca, Manila, Batavia, Bantam, Macassar, Ternate, Banda, Lifau, Ayutthaya, Hoi An, Jolo |
| `south_asia` | Goa, Surat, Cochin, Nagapattinam, Colombo |
| `west_asia` | Hormuz |
| `east_africa` | Mozambique |
| `europe` | Lisbon, Seville, Antwerp, Amsterdam |
| `north_america` | Acapulco, Havana |
| `south_america` | Bahia, Callao |

## Every harbour has a market

Every good can be bought and sold at every harbour, at the going price. So a
harbour has no stock list and no shopping list: both answers are all of them.

The only thing a harbour declares is what is **plentiful** there, which is what
the column below shows. Plentiful is cheap. Everything else is dear until
somebody sails it in.

Demand is the other side of the same fact and is never written down. A harbour
is short of whatever it does not make, so `tom_harbours:wanting/2` is simply the
complement of `producing/2`. When prices arrive this coarse split becomes a
number, and a harbour flooded with pepper stops being short of pepper without
anybody editing a file.

## The eight for the first game

| Harbour | Id | Where | Plentiful, so cheap |
|---|---|---|---|
| **Macao** | `macao` | Asia, the Pearl River | Raw silk, silk piece goods, porcelain, tea, gold, musk, rhubarb, sugar, tutenag, quicksilver |
| **Nagasaki** | `nagasaki` | Asia, Japan | Silver, copper, lacquerware |
| **Malacca** | `malacca` | Asia, the strait | Pepper, tin, cloves, nutmeg, mace, sandalwood, eaglewood, benzoin, trepang, tortoiseshell, beeswax, rice, ambergris, shark fin, birds' nests, camphor |
| **Goa** | `goa` | Asia, the Malabar coast | Cotton piece goods, opium, saltpetre, indigo, cinnamon, ivory, pearls, cowries, pepper |
| **Manila** | `manila` | Asia, the Philippines | Nothing. A pure entrepot, and rich anyway |
| **Lisbon** | `lisbon` | Europe | Lead, coral, broadcloth, wine, glassware and clocks |
| **Acapulco** | `acapulco` | North America, New Spain | Silver |
| **Bahia** | `bahia` | South America, Portuguese Brazil | Sugar, tobacco |

Five in Asia, one each in Europe, North America and South America.

## The shape this makes

The eight are not a ring. They form four routes with different characters, and
that is what gives a trader something to think about.

**The short rich run.** Macao to Nagasaki. Silk out, silver back. Days rather
than months, and the most profitable water in the game. Everyone will want it,
which is exactly why it should be crowded.

**The galleon.** Macao to Manila to Acapulco. Chinese goods meet New World
silver. Acapulco is a dead end: its only link is Manila. That makes it a port
with one route and an enormous prize on it, which is where the pirates belong.

**The long haul.** Macao to Malacca to Goa to Lisbon. Months, many hands, and
every leg a chance to sell early rather than hold out for Lisbon prices. The
patient trade.

**The Atlantic leg.** Lisbon to Bahia and on around the Cape to Goa. Sugar and
tobacco going one way, cloth and wine the other, and a long empty stretch in
between.

Malacca is the chokepoint. Almost everything moving between the Indian Ocean and
the China Sea passes it, which makes its Harbour Master the one everybody has to
deal with and the one best placed to be greedy.

## Notes

**Macao and Canton are one port here.** Canton is where the goods come from and
Macao is where a foreigner may buy them. Splitting them buys nothing yet.

**Bahia makes little.** Sugar and tobacco, out of forty five goods. It buys
everything, like every harbour, but there is not much reason to sail there to
load. Brazilwood is the obvious addition when it starts to matter.

**The pool answers what the eight could not.** Batavia and Bantam are the Dutch
rivals, Macassar is the free port where anything banned elsewhere is sold,
Hormuz supplies the horses and Mozambique is the Cape route's halfway house.
None of them play in the first game. They are there so the second game is a
different game.

**Every good is plentiful somewhere, and this is enforced.** A test in
`tom-shared` walks the world and fails the build if a good is produced nowhere,
because such a good could never enter the world at all. It caught camphor, which
forty five goods and twenty nine harbours had left with no source.
