# Places and routes

*This exists so a ship has somewhere to be between two ports, and so that
somewhere can eventually belong to somebody.*

**Status:** routes and waypoints built 2026-08-11 in `hecate-tom-world`. Holders,
forts and tolls are written down here and deliberately not built.

## The split, which took three goes to get right

| Says | Owner | Because |
|---|---|---|
| **Where** | the world | Geography is permanent and shared |
| **How long** | the ocean | A passage time is weather, season and hull |
| **Whether to stop** | the ship | Calling at a place costs time, and the cost is the player's to accept |

A waypoint carries a name and a line of character and **nothing else**. A route
carries which waters lie between two ports, in order, and nothing else. Two tests
in `hecate-tom-world` assert the exact key set of each, so the moment a duration
appears on the map the build fails.

**Routes are directional.** Both directions are written separately, because the
way home was not the way out. Manila to Acapulco runs north into the Kuroshio and
east for weeks; Acapulco to Manila runs downwind and is far quicker. That is why
the quicksilver goes west and the silver comes east, and it now falls out of the
map instead of a comment.

**A harbour is a waypoint that happens to have a market**, so a route may name
either kind. A route past a port is a route a ship may put in at.

## What was got wrong on the way

**Passability was called circumstantial, like a price.** It is not. A price is a
measurement: continuous, emergent, set by nobody. A closure is a **decision**:
discrete, caused, with a date and an agent. Reasoning that put duration in the
ocean does not reach passability.

**Append-only was confused with immutable.** Append-only means no event is
removed. It does not mean the derived state cannot move. A closed strait has not
stopped existing; it is on the chart, and it is shut. `good_withdrawn` was cut
because it *destroyed* something a player held, which is a different thing.

## The four events

| Event | Says |
|---|---|
| `waypoint_charted_v1` | It exists. Somebody found it and wrote it down |
| `waypoint_opened_v1` | It is passable |
| `waypoint_closed_v1` | It is not passable now |
| `waypoint_decommissioned_v1` | It will not be passable again |

All additive. Current passability is a projection over the log.

**Route closure is derived, never declared.** A route is shut if any place on it
is shut. Two truths that can disagree is the mistake that left stale Americas on
silver's origins.

**Weather is not politics.** A strait shut by a storm for six hours is the
ocean's business and never reaches the world's record. A strait shut by a war
does. Same word, two lifetimes.

## The second game: a waypoint that belongs to somebody

A waypoint is not only water. It is a **trading post, a fort, a bunker point**,
and whoever holds it can open or close it.

That is the historically exact shape. The Estado da Índia was never territory. It
was a chain of fortified posts holding chokepoints and taxing what passed.

**A waypoint with an occupier is a harbour without a market.** Same service,
different configuration: a fort is that service with no market and a garrison, a
trading post is that service with a small one. And it repeats a relationship
already in the game:

| | Infrastructure | Who sets policy | How they got it |
|---|---|---|---|
| Harbour | the market | the mayor | elected by the magnates |
| Waypoint | the passage | the holder | took it, or was given it |

A mayor bans a good at his quay. A holder closes a strait. The same power at a
different chokepoint.

**Holders can be bots**, which answers the cold start. The world begins with every
post held by a bot and a player takes one. That is one `hecate-tom-house` release
again, some instances driven by a human through a page and some by a policy. No
new kind of service anywhere.

## Why it is not being built

**Taking a fort is conflict, and there is no conflict in this game.** Not a gun
fired, not a garrison, not a way to lose one. Cannon exist as a good and nothing
shoots them.

So this is not four events. It is a war layer, and a war layer is larger than
everything built so far put together.

The four events are worth having now, with the steward as the actor, because they
are small and they make the mechanism real. Holders, forts and tolls are the
**second game**, and it will be a better second game if the first one survives
being played twice.
