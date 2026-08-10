# The harbours

*This exists so a trader has somewhere to sail to, and a reason to prefer one
place over another.*

**Status:** proposed 2026-08-10. Eight harbours.

Each is one `hecate-tom-harbour` service run by a player. Which box it runs on
and which station it dials are arbitrary and have nothing to do with where it
sits in the game. See [DESIGN_DEPLOYMENT.md](DESIGN_DEPLOYMENT.md).

## The eight

| Harbour | Id | Where | Sells cheap | Wants dear |
|---|---|---|---|---|
| **Macao** | `macao` | Asia, the Pearl River | Raw silk, silk piece goods, porcelain, tea, gold, musk, rhubarb, sugar, tutenag, quicksilver | Silver, pepper, sandalwood, eaglewood, ivory, birds' nests, cotton |
| **Nagasaki** | `nagasaki` | Asia, Japan | Silver, copper, lacquerware | Raw silk, silk piece goods, deer hides, sugar, porcelain |
| **Malacca** | `malacca` | Asia, the strait | Pepper, tin, cloves, nutmeg, mace, sandalwood, eaglewood, benzoin, trepang, tortoiseshell, beeswax, rice, ambergris, shark fin, birds' nests | Cotton piece goods, opium, silver, porcelain |
| **Goa** | `goa` | Asia, the Malabar coast | Cotton piece goods, opium, saltpetre, indigo, cinnamon, ivory, pearls, horses, cowries, pepper | Gold, silk, porcelain, copper, cloves, coral |
| **Manila** | `manila` | Asia, the Philippines | Silver, tobacco | Everything Chinese, above all silk and porcelain |
| **Lisbon** | `lisbon` | Europe | Lead, coral, broadcloth, wine, glassware and clocks | Everything eastern |
| **Acapulco** | `acapulco` | North America, New Spain | Silver | Silk, porcelain, and little else |
| **Bahia** | `bahia` | South America, Portuguese Brazil | Sugar, tobacco | Broadcloth, wine, cotton piece goods, tools |

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

**Bahia is thin.** Of the forty five goods it only sells sugar and tobacco.
Brazilwood would be the obvious addition when it starts to matter.

**No Dutch port.** Batavia or Bantam would give the map a rival and a second
European power. Worth having later. Eight is enough to start.
