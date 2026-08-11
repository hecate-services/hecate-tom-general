# Losing a ship

*This exists so that a wreck is a setback rather than a wall.*

**Status:** replacement hull built 2026-08-11 as a **stopgap**. Hulls as goods,
insurance, and the ways back into business are written down and not built.

**The rule this whole document serves: NO DEAD ENDS.** A state a player can reach
with no action available to them is a bug, not a difficulty setting. The floor
must not be zero. It is testable in that form: every reachable state has at least
one thing you can do.

## What a wreck costs

**The cargo, and the voyage.** Everything in the hold goes down with her, and the
weeks she spent at sea are gone.

**Not the game.** The house takes up a new hull at its home port and carries on.
Before this, a loss was terminal: ship building is out of scope, so once she sank
nothing could ever happen again, and the page sat there with a fully armed helm
refusing every press. A game that can only end in a dead stop leaves a player
holding a broken toy rather than a defeat.

## Why the replacement is free, for now

Not generosity, and not permanent. **There was nowhere to get a price from.**

Price is always circumstantial: it comes out of a market or it does not exist.
There was no market in hulls, so any figure would have been the one invented
number in a game that has refused to invent them.

**A hull should be a good, and then there is a price.** A shipyard is then an
ordinary factory and nothing needs inventing:

    build_hull: teak 40, ironwork 8, cordage 4, sailcloth 6 -> hull 1, 30 ticks

That was a choice made and then reasoned around. The earlier note that "a
shipyard is not a factory, because its output is not a good" was a decision, not
a fact, and it is the decision that forced everything after it. Making a hull a
good collapses the special case, gives **teak, oak and pine the consumer** they
have been waiting for since the raw materials tier went in, and turns "here, have
one" into "buy one", which is better.

It needs exactly one new thing: **a hull is a good that cannot be carried.** You
do not stow a ship in a ship. That is one boolean, and unlike `contraband` or
`money` or `bulk` it is a genuine physical fact about the thing, in the same
family as fragile and perishable.

**The free hull stays until the magnate exists.** Buying a replacement is the
terminal wall again for a player who is broke, and a shipless house earns by
being a magnate: works ashore, producing and selling. Factories as harbour state
do not exist yet. Until they do, "buy a hull" means a wreck can still end the
game, which is the fault this is fixing.

That ordering is written down deliberately, because a free hull is exactly the
kind of temporary thing that quietly becomes permanent.

## Getting back into business

A player can be broke without a wreck: a bad voyage, a market that moved, a
harbour that banned what was in the hold. The rule above says there must always
be a way back, and it should be a way that reads as part of the world rather than
as a refund.

**Freight is the purest one.** Carry another house's cargo for a fee. It needs no
capital at all, only a hull and time, and it is exactly what the Ship Master role
was for before it was folded into the Trader. A player with nothing but a ship is
a carrier, which is a real trade and was most people's.

**Bottomry is the period one.** A loan secured on the ship, repaid at a high rate
on safe arrival and **forgiven if she sinks**. It is the actual instrument of the
era and the direct ancestor of marine insurance, so it shares machinery with the
policies above: a contract between two houses, verified against the ocean's own
record of what happened.

**Wages ashore are the true floor.** A house with nothing works for a port. Dull
on purpose: it should be the least attractive way back, and it should always be
available, because it is what makes the floor not zero.

What to avoid: a handout with no story in it, and a fresh start that wipes the
record. Both turn a defeat into an inconvenience, and a defeat that costs nothing
was never a risk.

## Insurance, written down and not built

A wreck should be insurable. It is the oldest mechanic in this trade and it needs
no new machinery: a policy is a contract between two houses, and this game
already has houses, coin and a public record of what sank.

The shape, when it is time:

**Anyone with capital may underwrite.** A magnate with a full treasury insuring
other people's voyages is Lloyd's coffee house, and it is a second economy laid
over the first at almost no cost in mechanism.

**A policy is written before departure**, on a named voyage, for a stated sum,
against a premium paid at once. The premium is a price and therefore a
negotiation between two players, which is exactly right: what a crossing is worth
insuring depends on the season, the route, the cargo and how much the underwriter
knows.

**It pays out on the ocean's word**, not the claimant's. The ocean already
publishes a loss, and the fate is drawn at sailing from a hash over the departure
facts, so an underwriter can verify a wreck happened and that the sea was not
cheating. That is the part that usually makes insurance hard, and here it is
already done.

**It makes the hazard model matter.** Without insurance a player either takes the
risk or does not. With it, risk has a price, and a route everybody thinks is safe
becomes cheap to insure, which is information.

**And it gives a bad player a way to be interesting.** Underwriting voyages you
know are doomed is a strategy.

## What is not wanted

**A wreck that costs nothing.** If the replacement were instant and the cargo
survived, there would be no reason to care about the sea, and the ocean is the
only antagonist this game has.

**A wreck that ends everything.** Which is what it did until today.
