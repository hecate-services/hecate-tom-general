# The goods

*This exists so that a manifest is worth reading. It is the canonical set of
goods a ship can carry in TOM.*

**Status:** agreed 2026-08-10, extended 2026-08-11. Sixty seven goods: the
original forty five trade goods, plus the raw materials tier and the ores and
manufactures that came with factories. See [DESIGN_FACTORIES.md](DESIGN_FACTORIES.md).

**Encoded in:** `hecate-tom-shared/priv/worlds/macao.world`, which is the
authority for what exists. `tom_goods` owns the shape a good has, not the list.
A good in the data is an id, a name, its origins and a line of character, and
nothing else. This document carries the reasoning, the "goes to"
column and the raw materials tier, none of which the data does.

An id is a permanent commitment. Every stored fact that names a good names it,
so renaming one orphans every fact that ever carried it.

The id in the table below is a **local name**, not an identifier. It means
something inside this world file and nothing outside it. On the mesh a good is
`mri:class:{realm}/tom/good/{id}`, built by `tom_mri` at runtime, because the
realm is the game and one world file serves many games. Nothing resolves a name
a world has not declared, and nothing turns a stranger's name into an atom.

A good earns its place only if it makes some decision interesting that no other
good makes. Anything that is merely another name for "cargo" is texture, and
texture is welcome. Which good was meant to make which decision, and where that
decision actually turned out to live, is in
[What each good is for](#what-each-good-is-for).

---

## From China

Canton, Nanking, Jingdezhen, Fujian. Origin `china`.

| Good | Id | Goes to | Character |
|---|---|---|---|
| Raw silk | `raw_silk` | Japan, Goa, Manila, Lisbon | The flagship. Dear, moderate bulk |
| Silk piece goods | `silk_piece_goods` | Japan, Manila, Lisbon | Damask, satin, taffeta. Finished, dearer, same stowage |
| Porcelain | `porcelain` | Everywhere | Cheap by the ton, very bulky, breaks in a storm |
| Tea | `tea` | Lisbon, Europe | Bulky, loses value with every week aboard |
| Gold | `gold` | Goa, India | Trades at a different rate in India. Pure arbitrage |
| Musk | `musk` | Goa, Lisbon | A pouch is a cargo |
| Rhubarb | `rhubarb` | Lisbon, Persia | Medicinal, light, keeps indefinitely |
| Camphor | `camphor` | India, Arabia | Also Borneo and Japan. Wastes if badly stowed |
| Sugar | `sugar` | Japan, Manila, India | Bulk, cheap, ruined by wet |
| Tutenag | `tutenag` | Goa, Lisbon | Zinc. Heavy, dull. Ballast that pays a little |
| Quicksilver | `quicksilver` | Manila, New Spain | Small casks, dear, refines silver |

## From Japan

Origin `japan`.

| Good | Id | Goes to | Character |
|---|---|---|---|
| Silver | `silver` | China, always | The money good. No bulk, immense value |
| Copper | `copper` | China, India | Heavy, steady, unglamorous |
| Lacquerware | `lacquerware` | Goa, Lisbon | Novelty. Fragile, dear, demand fades |

## From the archipelago and mainland Southeast Asia

Origin `southeast_asia`.

| Good | Id | Goes to | Character |
|---|---|---|---|
| Sandalwood | `sandalwood` | China | Timor and nowhere else. The one route with no substitute |
| Eaglewood | `eaglewood` | China, Arabia | Calambac. The finest incense, absurd value by weight |
| Cloves | `cloves` | China, Europe | Moluccas. Small, dear, hoarded |
| Nutmeg | `nutmeg` | China, Europe | Banda. Same |
| Mace | `mace` | Europe | The aril of the nutmeg. Rarer than the nut |
| Pepper | `pepper` | China, Europe | Sumatra and Malabar. Heavy, cheap, pays only at volume |
| Tin | `tin` | China, India | Malaya. Heavy, honest, always a buyer |
| Birds' nests | `birds_nests` | China | The islands' luxury. Tiny bulk, absurd price |
| Shark fin | `shark_fin` | China | Same market, coarser |
| Trepang | `trepang` | China | Sea cucumber. Bulky for a luxury, must be dried hard |
| Tortoiseshell | `tortoiseshell` | China, Europe | Light, dear, worked into combs and boxes |
| Benzoin | `benzoin` | China, Europe | Gum benjamin. Incense and medicine |
| Deer hides | `deer_hides` | Japan | Siam and Formosa. Rots if the hold is wet |
| Beeswax | `beeswax` | China, Manila, Goa | Candles for churches and temples. Dull and steady |
| Rice | `rice` | Everywhere | Siam and Java. The bulk staple, and the thing crews eat |
| Ambergris | `ambergris` | Lisbon, Arabia | Found, not produced. A windfall, never a plan |

## From India, Ceylon, Persia and Arabia

Origin `south_asia`, except horses, which are `west_asia`, and ivory, which is
also `east_africa`.

| Good | Id | Goes to | Character |
|---|---|---|---|
| Cotton piece goods | `cotton_piece_goods` | Everywhere | Gujarat and Coromandel. The floor. Always a buyer, thin margin |
| Opium | `opium` | China, illicitly | Bengal and Malwa. Small, dear, bannable |
| Saltpetre | `saltpetre` | Everywhere at war | Bengal. Munitions, so its legality follows the politics |
| Indigo | `indigo` | Europe | The great dye. Bulky for its price, keeps forever |
| Cinnamon | `cinnamon` | China, Europe | Ceylon. Light, fragrant, jealously controlled |
| Ivory | `ivory` | China, India | Heavy tusks, carved in Canton, sold on |
| Pearls | `pearls` | China, Europe | Gulf of Mannar, Persian Gulf, Sulu. No bulk at all |
| Horses | `horses` | India | Persia and Arabia. Livestock. Eats, drinks, dies |
| Cowries | `cowries` | Bengal, Africa | Maldives. Money by the ton. Bulk currency |

## From Europe and the New World, via Lisbon or Manila

Origin `europe`, except tobacco, which is `south_america` and `north_america`,
and silver, which comes out of Japan and both Americas.

| Good | Id | Goes to | Character |
|---|---|---|---|
| Silver | `silver` | China | New Spain via the Manila galleon. The other silver tap |
| Lead | `lead` | China, India | Heavy, cheap, shot and sheathing |
| Coral | `coral` | India | Mediterranean. Light, dear, a genuine India favourite |
| Broadcloth | `broadcloth` | Nowhere warm | English and Flemish woollens. The trap good. Nobody wants it |
| Wine | `wine` | Goa, Macao | Portuguese, for Portuguese. Spoils, and the crew knows where it is |
| Tobacco | `tobacco` | Manila, China | New and fashionable. Demand rising, not yet established |
| Glassware and clocks | `glassware_and_clocks` | Canton | The curiosity trade. Fragile, and novelty wears off |

Silver appears in two tables. It is one good with three taps, Japan, New Spain
and Peru, not three goods, and carries all three origins.

The nine regions are `china`, `japan`, `southeast_asia`, `south_asia`,
`west_asia`, `east_africa`, `europe`, `north_america` and `south_america`. Goods
and harbours name the same set, but not the same relation: a harbour's `region`
is where it **is**, and a good's `origins` are where it **comes from**. The field
was called `regions` on both until 2026-08-11, which read fine and meant two
things.

---

## What each good is for

A good earns its place by making one decision interesting that no other good
makes. This table is the reasoning, and it is **reasoning only**. It was briefly
a `jobs` field on each good in the world file, and that field has been deleted,
because none of the eight names survived being asked where they actually belong.

| The decision | Made interesting by | Where it really lives |
|---|---|---|
| Money and arbitrage | Silver, gold | **The medium of exchange**, not a property of the metal |
| Hull condition and weather routing | Porcelain, glassware and clocks, lacquerware | Real. Returns as a **damage number** when storms exist |
| Speed | Tea, deer hides, wine, horses, arrack | Real. Returns as a **decay number** when time exists |
| Capacity | Pepper, rice, cowries, tutenag, ore, timber | A **price** fact. Heavy means cheap per unit, once a hold takes one unit of anything |
| Route exclusivity | Sandalwood, eaglewood, nutmeg | **Derived.** One source, which `tom_harbours:producing/2` answers |
| The Harbour Master's tax and ban | Opium, saltpetre, gunpowder | **A harbour's decision.** Opium is banned in China and legal in Bengal |
| The floor under a bad voyage | Cotton piece goods, tin, ironwork | A **price** fact |
| Demand is local | Broadcloth | A **price** fact |

The lesson is worth keeping: a property of a good and a property of a market are
different things, and an enum on the good will happily hold both until somebody
asks it to mean something.

## Deliberately excluded

**Slaves.** Historically part of Macao's trade. Excluded by decision, 2026-08-10.
Not an oversight, and not to be added back.

## Open

**The period.** Macao in 1590 is a different game from Macao in 1750. Early, it
is the Great Ship to Nagasaki, silk out and Japanese silver back: one
fabulously profitable run with one obvious risk. Late, it is Canton, tea and
opium, and the Japan trade is gone. The list above spans both, so it is not yet
internally consistent. Tea, opium and tobacco are late. Japanese silver, copper
and lacquer are early. If the earlier window is chosen, saltpetre becomes the
contraband and deer hides the perishable, and the three late goods come out.

**Units.** Not settled. The period units are piculs for goods, taels for
silver, chests for opium, bahars for pepper. A unit implies a lot size, and a
lot size implies how a hold is filled, so this is the next thing to decide.

**Where each good is produced.** The "Goes to" column above names markets, not
the hinterlands that make the stuff. Producing hinterlands sit behind harbours
and are a separate decision. This is why `tom_goods` encodes regions of origin
but not markets: there are no ports yet for a market to resolve against.
