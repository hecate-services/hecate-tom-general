# Two services

*This exists so that who owns a thing decides which service it is, and so a
player can be a bot.*

**Status:** proposed 2026-08-12. Classified **BUILD**. It makes no claim about
the world, so it gets tests and commits and no adversarial gate.

**Steps 1 and 3 executed 2026-08-13**, in one sitting: the world's six modules
came into the harbour as `know_the_world/`, the harbour became
`hecate-tom-world` and the house became `hecate-tom-player`. 183 tests in the
world and 128 in the player, elvis and dialyzer clean on both. **The ocean is
still up and still a service**, because step 2 is the voyage and that has not
been done, so the count is four repositories today and three when it lands.

It finishes what [DESIGN_VOYAGE.md](DESIGN_VOYAGE.md) started, revises the
repository table in the [README](../README.md) and the layout in
[DESIGN_DEPLOYMENT.md](DESIGN_DEPLOYMENT.md), and generalises a shape that
[DESIGN_PLACES.md](DESIGN_PLACES.md) had already found twice.

## The rule

**The world runs places. The player runs people.**

A place's policy is set by a person who does not run it. That relationship is
already in the game twice: a mayor sets policy at a quay he does not host, and a
holder closes a strait he does not host either.

| | Runs | Owned by | Uptime |
|---|---|---|---|
| **`tom-world`** | Places. Harbours, trading posts, forts, and the passages that leave them | Nobody. Operated by the steward | Always on |
| **`tom-player`** | People. A magnate, a trader, a mayor, a holder | One person, or one policy | Off whenever they like |

Neither is one process. `tom-world` is one binary run once per place, eight or
more instances across `beam00` to `beam03`, each dialling a different station.
`tom-player` is one binary run once per player, on a laptop or on a lab box.

## What this actually changes

| | Repositories |
|---|---|
| Today | 5: `general`, `world`, `harbour`, `house`, `ocean` |
| After [DESIGN_VOYAGE.md](DESIGN_VOYAGE.md), already designed | 4. The ocean dissolves |
| After this | 3: `general`, `world`, `player` |

One repository, and two renames. The consolidation is nearly free and nearly
already done. **The substance of this document is the role model and the bot,
and those are additions rather than a restructure.**

## Why the boundary goes here

`hecate-tom-world` justified itself like this, and the sentence is right:

> adding a good does not require eight people to redeploy their laptops on the
> same afternoon

The harbours are not laptops. [DESIGN_DEPLOYMENT.md](DESIGN_DEPLOYMENT.md) puts
eight of them two apiece on `beam00` to `beam03`, under watchtower, owned by the
steward. Adding a good means rolling four boxes, which watchtower does in seconds
without asking anybody's permission.

| Boundary | Same owner | Same release train | So |
|---|---|---|---|
| world ↔ place | yes | yes, watchtower | a library is fine, and facts are ceremony |
| world ↔ player | no | no, their whim | facts are mandatory |

The rule was written for the second row and applied to both. **This does not
reverse "no shared domain library".** It removes the boundary that rule was
policing, between the world's reference data and a port's market, because after
this they are one service. Where the rule earns its keep, at the player, it
hardens: a player learns what exists over the mesh and links nothing of ours.

## A place is one binary in several configurations

[DESIGN_PLACES.md](DESIGN_PLACES.md) got here first, for waypoints:

> A waypoint with an occupier is a harbour without a market. Same service,
> different configuration: a fort is that service with no market and a garrison,
> a trading post is that service with a small one.

Generalised, that is the whole world side:

| A place with | Is | Policy set by |
|---|---|---|
| a market and an electorate | a **harbour** | its mayor |
| a small market and an occupier | a **trading post** | its holder |
| no market and a garrison | a **fort** | its holder |
| neither | a **waypoint** | the steward |

So "which service runs Lisbon" has an answer that reads properly: a `tom-world`
instance, running one place, which happens to have a market. The binary is the
world. An instance is a place.

The voyage is unaffected. [DESIGN_VOYAGE.md](DESIGN_VOYAGE.md) runs a passage at
the port she sailed from, which is now the **place** she sailed from, and a
route may already name either kind.

## A player is one binary, with roles and two drivers

**Roles are slices, switched on by configuration.** Adding a fourth is a
directory, which is what "currently three, but this could be extended" has to
mean if it is to mean anything.

| Slice | Role | Built |
|---|---|---|
| `run_fleet` | Trader. Ships, voyages, cargo | ✅ as `buy_cargo`, `sell_cargo`, `sail_ship`, `find_ship` |
| `keep_works` | Magnate. Factories, recipes, what is being made | ❌ |
| `hold_office` | Mayor. The seat, and what is done with it | ❌ |
| `hold_post` | Holder. A fort or a trading post, and who passes | ❌ second game |

**Bot and human are two drivers of one command surface, never two code paths.**
The seam already exists: the page posts to `/act`, so the commands are already
separate from the page that sends them. A bot is a policy calling the same
desks. Built as two paths they get written twice and drift, and the bot quietly
becomes the one that works.

[DESIGN_PLACES.md](DESIGN_PLACES.md), again, already:

> Holders can be bots, which answers the cold start. The world begins with every
> post held by a bot and a player takes one. That is one release again, some
> instances driven by a human through a page and some by a policy. No new kind of
> service anywhere.

## What this deletes

[DESIGN_WORLD.md](DESIGN_WORLD.md) sketches nine events, nine commands, nine
handlers and a read model per consumer. None of it is built. Most of it exists to
carry reference data from the world to a port, which after this is a function
call inside one binary.

What is left is carrying it to a **player**, and an event log is the wrong
instrument for that. The world is strictly append-only, and `DESIGN_WORLD`
records that it kept shrinking, from fifteen events to nine, as goods, harbours
and recipes each turned out to be permanent. Data that is permanent, additive and
never deleted does not need a log to be caught up on. It needs a **versioned
artifact and a digest**, and `tom_world:digest/1` already exists for exactly the
question a peer has to ask.

| Instead of | The player |
|---|---|
| subscribing to nine event types and folding a read model | fetches the world artifact from any place and checks its digest |

The nine events come back the day somebody wants to introduce a good at runtime
without rolling the fleet. That day is not near, and nothing is lost by waiting,
because the world file is checked on load today and the check reports every
problem rather than the first.

## Three conditions

**1. `tom-world` is one binary run N times, never one process.** This is the one
way the proposal fails badly. [DESIGN_VOYAGE.md](DESIGN_VOYAGE.md) has just spent
a day killing the central sea because `msi00` down meant nothing sailed anywhere,
in a game whose point is the mesh. A singular name invites a singleton. One place,
one instance, one station.

**2. The fact discipline survives at the player boundary.** Once the world's
modules sit in the same tree as a market, the temptation is to drop the rule in
both directions. A player links `macula` and nothing of ours, and that is not
negotiable, because a player upgrades when they feel like it.

**3. One command surface, two drivers.** As above.

## What this does not fix

**Money.** The purse lives on the player and nothing checks it. Bot mode makes a
cheat structurally identical to a bot, since both are the same binary with the
same config. There is no better home for the purse on the world side either,
because money is not local to a place, which is why it went to the house in the
first place.

This is accepted rather than overlooked. `tom_buy_cargo` already says the
ownership check is "a check against a mistake, not an attacker". The game is
playable among people who know each other, and it is stated rather than
pretended.

## The work

| | What | Size |
|---|---|---|
| 1 | Move the six world modules into the harbour tree as a slice. Rename the result `hecate-tom-world`, archive the old repository. Delete the `rebar.config` comment forbidding the dependency, with the reason | half a day |
| 2 | [DESIGN_VOYAGE.md](DESIGN_VOYAGE.md) steps 1 to 4, now inside one tree instead of across two | two days |
| 3 | Rename `hecate-tom-house` to `hecate-tom-player` | two hours |
| 4 | Roles as configuration-selected slices. The trader exists; this is the seam, not a new role | half a day |
| 5 | The bot driver, against the command surface the page already uses | a day |
| 6 | Run it and watch the market | half a day |

**Do 1 before 2.** `DESIGN_VOYAGE` steps 1 to 3 straddle the world/harbour
boundary, and after the merge they are one tree's work.

**Step 6 is an instrument, not a demo.** A bot trader arbitraging two places will
buy until the price rises and sell until it falls, and drive the gap down to the
crossing. [DESIGN_MARKET.md](DESIGN_MARKET.md) already says the world it makes is
half flat. The expectation is therefore that **a bot flattens the map in an hour
and the world goes quiet**, and that this is the finding: trading alone converges
to nothing, and the magnate is what regenerates the gradient a trader lives on.

That costs a day to learn and it decides whether the magnate is the next build.
Cheaper than building the magnate and finding out.

## Open

~~**Which repository survives the merge.**~~ **Settled 2026-08-13: the harbour
survives and takes the name.** Its history stays attached to the code that will
be worked on next, which the world's six modules will not be. Archiving does not
free a name on GitHub, so the old repository was renamed to
`hecate-tom-world-superseded` first and archived under that; its seven commits
are readable there, and the local checkout is in `hecate-services/.attic/`.

The alternative, letting the world repository absorb the harbour, was better on
the naming and worse where it counts: it would have left the market, the
crossing and the four probes with a one-line history saying "moved".

**Where a bot's policy lives.** A module in `tom-player` and a line of config is
enough for one arbitrageur. It is not obviously enough for a holder deciding
whether to close a strait.

**Whether a place carries the whole world or its own slice.** The whole world is
601 lines and simpler. A slice is defensible the day a place should not know what
another place produces, and nothing today wants that.
