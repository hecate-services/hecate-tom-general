# The goods

*This exists so that a manifest is worth reading. It is the canonical set of
goods a ship can carry in TOM.*

**Status:** agreed 2026-08-10. Forty five goods.

**Encoded in:** `hecate-tom-shared`, module `tom_goods`. The `Id` column below
is the atom used there, and it is a permanent commitment. Every signed fact
that names a good names it by that atom, so renaming one invalidates every
fact that ever carried it.

A good earns its place only if it makes some decision interesting that no other
good makes. Anything that is merely another name for "cargo" is texture, and
texture is welcome, but the mechanics ride on the handful listed under
[What carries which job](#what-carries-which-job).

---

## From China

Canton, Nanking, Jingdezhen, Fujian. Region atom `china`.

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

Region atom `japan`.

| Good | Id | Goes to | Character |
|---|---|---|---|
| Silver | `silver` | China, always | The money good. No bulk, immense value |
| Copper | `copper` | China, India | Heavy, steady, unglamorous |
| Lacquerware | `lacquerware` | Goa, Lisbon | Novelty. Fragile, dear, demand fades |

## From the archipelago and mainland Southeast Asia

Region atom `southeast_asia`.

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

Region atom `india`.

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

Region atom `west`.

| Good | Id | Goes to | Character |
|---|---|---|---|
| Silver | `silver` | China | New Spain via the Manila galleon. The other silver tap |
| Lead | `lead` | China, India | Heavy, cheap, shot and sheathing |
| Coral | `coral` | India | Mediterranean. Light, dear, a genuine India favourite |
| Broadcloth | `broadcloth` | Nowhere warm | English and Flemish woollens. The trap good. Nobody wants it |
| Wine | `wine` | Goa, Macao | Portuguese, for Portuguese. Spoils, and the crew knows where it is |
| Tobacco | `tobacco` | Manila, China | New and fashionable. Demand rising, not yet established |
| Glassware and clocks | `glassware_and_clocks` | Canton | The curiosity trade. Fragile, and novelty wears off |

Silver appears in two tables. It is one good with two taps, not two goods, and
carries both region atoms.

---

## What carries which job

The mechanics ride on a small number of these. When building, wire the job
before the flavour. A job nothing carries is a mechanic nothing exercises, and
the test suite in `hecate-tom-shared` fails the build if one appears.

| Job | Atom | Carried by |
|-----|------|-----------|
| Money and arbitrage | `money` | Silver, gold |
| Tests hull condition and weather routing | `fragile` | Porcelain, glassware and clocks, lacquerware |
| Tests speed | `perishable` | Tea, deer hides, wine, horses |
| Tests capacity | `bulk` | Pepper, rice, cowries, tutenag |
| Tests route exclusivity | `exclusive` | Sandalwood, eaglewood |
| Gives the Harbour Master's tax and ban real teeth | `contraband` | Opium, saltpetre |
| The floor that keeps a bad voyage from being ruinous | `floor` | Cotton piece goods, tin |
| Teaches that demand is local | `trap` | Broadcloth |

The other twenty six goods carry no job. That is the design. Texture is what
makes a manifest worth reading, and a list where every entry is a special case
is a list nobody can hold in their head.

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
