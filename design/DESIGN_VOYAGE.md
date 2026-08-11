# The voyage

*This exists so a ship can sail Macao to Lisbon through three ports, with no
central sea.*

**Status:** designed 2026-08-11, nothing built. It dissolves `hecate-tom-ocean`,
which is running. It revises one row of [DESIGN_PLACES.md](DESIGN_PLACES.md) and
finishes an argument that document started.

## The concept that was missing

`tom_voyage` already existed in the ocean, as a pure record, sitting in a map,
inside another process's state, keyed `{ship, hop}`. It could not do anything. It
had no agency at all.

So every question you can ask about a ship under way had to be asked of the
ocean, and the ocean grew one answer per question. How long until she is there,
has she sunk, where is she, has the far port got her yet, what did she look like
when she left. Six responsibilities, and every one of them is really a question
about a voyage that had nobody to ask.

**An ocean is not somebody you give a ship to.** It is where the ship is. Water
has no delivery obligation. But everywhere else in this game a service is a
party, so when the ocean was made a service it inherited that shape: a party
needs custody, so it took custody; a party that holds your goods needs a ledger,
so it grew one that never forgets; a party that owes you a delivery needs an
outbox, so it grew `landings_at`, a `taken` flag and a second durable write to
remember what it had already handed over.

The hole was filled once before, the other way round. The brief had a Ship
Master, folded into the Trader on 2026-08-10 because a game needs two humans and
not three. Good reason, but folding the role did not remove the job. Somebody
still has to know where she is, when she is due, and when she has arrived. With
nobody aboard, the sea did it.

## Where the six pieces go

| The ocean owned | Goes to | Because |
|---|---|---|
| Custody of the hull in transit | **the voyage** | She is nobody's guest. Macao is done with her, Nagasaki has not got her |
| The clock, `passage_ms`, flat 90s | **the world**, as leagues per leg | Distance is geography. Duration is not: see below |
| Hazard and the fate draw | **the world**, as exposure and a published rule | Everyone must agree, and anyone must be able to check |
| A log of every crossing since the world began | **nobody** | That is the archive of a party. A house remembers her own ships; a port remembers its own quay |
| The delivery queue | **deleted** | She presents herself. There is nothing to offer, page, mark taken or prune |
| Three published facts | **the harbour**, on its own topic | The port she sailed from says what became of her |

## Where a passage runs

**She runs at the port she sailed from, for the leg she is on.** Macao holds the
passage to Malacca, Malacca holds the passage to Goa, Goa holds the passage to
Lisbon.

Nothing in the domain has a claim on hosting her, which is exactly why it looked
like a free choice and got answered by accident. She is not at either port and
she is not anywhere else. So the choice is operational, and operationally:

**No singleton.** Today one box, msi00, carries every ship in the world. That
box down means nothing sails anywhere, from any port to any port. It is the one
centralised component in a game whose point is the mesh. The test is not whether
a thing is a singleton but whether the game stops when it is down. The ocean
fails it.

**One hop per leg instead of two.** The hull crosses the wire once, port to port,
rather than port to sea to port.

**The mesh traffic gets better.** Eight harbours on four boxes, each dialling a
different station, handing hulls to each other directly, instead of hub and spoke
through one box.

**`hop` becomes geography.** It stops being a custody sequence number and becomes
the leg. A ship handed forward Macao, Malacca, Goa, Lisbon genuinely migrates
across three services, which is the thing this game was built to demonstrate.

Hosting is not owning, and the two must not be run together again. **The voyage
is the custodian of the hull; the port is only the host of the process.** Macao
hosting a ship four hundred leagues away is not a lie about where she is, because
her position is a fact on the voyage and not an implication of her host.

## Most of it is already built

`tom_hand_over_ship` in the harbour is one process per consigned hull that
retries every five seconds forever, resumes at boot from its own record, sends a
byte-identical payload every attempt so the receiver dedupes on `{ship, hop}`,
and lives in its own process because the call blocks. It is generic over a
destination and a procedure, and it currently points at the ocean.

On the other side `tom_receive_ship` already takes a hull idempotently. And
`tom_sail_ship:consigned/4` freezes the berth and **keeps the hull in the port's
own `ships` map** until the receiver says held.

So the harbour already does port-to-port handover, in both directions, durably,
with retry, and already holds a hull it has consigned. **The ocean is a delay
inserted between two halves that already exist.** What the harbour is missing is
exactly what the ocean owned and nothing else: a clock and a fate.

That is the whole rework. A consigned hull stops being handed over immediately
and instead sits at sea for the length of her leg, and at the end of it she is
either handed over by the machinery that is already there, or she is not, because
she sank.

**The knocking comes back, and it is fine now.** It was ugly as a worker pool the
sea ran per undelivered landfall, with a sweep above it to kill the ones the
previous sea left behind, and it was ugly again as an outbox with a cursor and a
`taken` flag. As her own behaviour it is not ugly at all: a ship that reaches a
dark port lies in the roads and waits for them to open. She is the delivery state.
There is no side table because there is nothing beside her.

## A voyage is one leg

The house orders "sail to Malacca". At Malacca the ship sits at the quay until
the house orders the next leg.

The route graph already says this. Fourteen routes, and they chain: Macao to
Malacca to Goa to Lisbon to Bahia, plus Macao to Nagasaki and Macao to Manila to
Acapulco. Macao to Lisbon is three legs through three ports.

No itineraries, no re-planning after a wreck, no path-finding in a harbour. Every
stop is a market you can trade in and a decision you have to make, which is the
better game as well as the smaller program.

## What this changes in DESIGN_PLACES

That document splits the map three ways, and one row was wrong:

> | **How long** | the ocean | A passage time is weather, season and hull |

The reasoning is right and the custodian is not. A passage time *is* weather and
hull, so it is not the world's. But **distance is**, and distance was never
separated from duration, so both ended up in the ocean and the map got neither.

| Says | Owner |
|---|---|
| Where, and how far | the world |
| How long, given this hull and this weather | the passage |
| Whether to stop | the ship |

Two tests in `hecate-tom-world` assert the exact key set of a route so that the
build fails the moment a duration appears on the map. **Keep them.** Leagues are
not a duration. They are the same kind of fact as a good's origins: permanent,
checkable against a real map, and true whoever is sailing.

The same line settles the hazard. A leg carries its **exposure**, which is
permanent and belongs to the water: the Formosa Strait is shallow, crowded and
blowing hard half the year whoever is in it. Whether *this* crossing ends badly
is drawn at sailing time, from exposure and the hull and the moment, by a rule
everybody holds.

**Measure and exposure belong on a leg, not on a route.** A route already carries
`via`, so it is already segmented. Put both on the hop between consecutive places
and a route's length is derived rather than declared, adding a waypoint
recomputes it, the dangerous part can be the strait rather than the whole
crossing, and a ship at sea has a position instead of only a due time.

## What the world holds, and what it does not

One rule covers geography, the market and the sea: **the world holds what
everyone must agree on, and the service holds the computation.**

The market already works this way by accident. `tom_crossing`'s eleven constants
must be identical at every port or the game is incoherent, while the bisection
that uses them is plainly the harbour's own business. The sea is the same shape:
leagues, exposure, the tempo constant and the hazard constant are agreements, and
they belong in the world and therefore in its digest. Applying them to one hull
on one afternoon is the passage's business.

The fate rule stays as it is: a sha256 over the five facts published at
departure, thirty-two bits of fortune and eight of weather. Its inputs come off
the world instead of out of a `-define`, and the rule itself is documented so
that anyone who saw a departure can check that what was reported is what the
arithmetic says it must be. That verifiability is what makes it safe for a port
to run passages at all.

## The cost, and it is real

**A port that hosts your passage also runs a market you trade in.** The ocean was
neutral by being nobody's, and no port is.

It is bounded. The fate is a hash of five published facts, so a port cannot lie
about whether you sank or make a bad crossing worse. What it can do is stall or
go quiet, and both are visible to anyone watching the departure fact.

It does not bite while one operator runs every port. It bites the day they are
run by different people, and the answer then is not to bring the ocean back but
to make the passage checkable end to end, since the departure is already
published and the draw is already public.

## Open

**A house with no memory cannot find her ship.** She owns her, ordered the
sailing and holds the facts, so this is a recovery case rather than the common
path, but there is no answer for it yet short of asking every port.

**What a wreck does to a leg that has not started.** A voyage is one leg, so a
ship lost between Malacca and Goa never had a Goa-to-Lisbon leg to cancel. This
is probably nothing, and it should be confirmed rather than assumed.

**Whether the passage is `tom_hand_over_ship` extended at the front or a sibling
that starts it.** One grep on who else spawns that worker settles it at
implementation time.

## The work

Classified **BUILD**. It makes no claim about the world, so it gets tests and
commits and no adversarial gate.

| | What | Size |
|---|---|---|
| 1 | World: legs carry measure and exposure, the passage constants and the fate rule move in from the ocean | half a day |
| 2 | Harbour: slice `keep_the_sea/`. A consigned hull draws her fate at departure, sits for her leg, then hands over or founders | most of a day |
| 3 | Harbour: `tom_take_landings` and the ocean subscription deleted, the three facts published on the port's own topic | half a day |
| 4 | House: drop `ocean` from `tom_names`, point `find_ship` at the port she sailed from, drop `tom/ocean` from the service resources, delete the line about the ocean knocking at her door | two hours |
| 5 | Stop what is running on msi00, pull the quadlet, archive `hecate-tom-ocean` | half an hour |

The game is broken between 2 and 4, so those three want to be one sitting.
Nothing is in production and there is nothing to be compatible with, so it is a
cutover and not a migration.

**Acceptance is the line at the top, run for real.** She sails Macao to Malacca
to Goa to Lisbon across three harbour instances on three boxes, one of which is
restarted mid-passage, and one of which is dark when she arrives and comes up ten
minutes later to find her waiting.
