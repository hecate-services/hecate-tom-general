# The market

*This exists so that a trader can look at a price and know why it is that
number.*

**Status:** built and probed 2026-08-11, in
[`hecate-tom-harbour`](https://github.com/hecate-services/hecate-tom-harbour).
The mechanism behaves. The world it produces is half flat, and the fix is
already in the code.

## What was built

Marshallian curve intersection. The town's downward demand curve crossed with
the hinterland's upward supply curve, with the quay's heap as the short-run
shifter. Chosen over a constant-product invariant and a power-law bonding curve.

A harbour declares three things and not one of them is about worth: a **town**
size, which is a headcount and multiplies demand identically for every good; a
**hinterland** extent, which multiplies every yield identically; and a **yield**
per good, which is a rate, the same kind of fact as a recipe's `ticks`.

Two more are derived rather than declared: `produces`, which the world service
already publishes, and a **census** of how many other harbours are known to
produce each good and whether they are near.

## Why the other two lost, which is the useful part

**The power law had no per-good term at all**, so at an empty heap every good
quotes the same price. The nine goods that come only from factories have no
world yield, so their heaps drain to empty, and they would live permanently in
the regime where musk and rice cost the same. It also wanted a yield per harbour
per good, roughly two hundred separately tunable numbers, each of which sets one
good's price at one port. No authoring discipline closes a knob that specific.

**The invariant had two per-good knobs multiplying linearly** into the resting
price, so any target is two keystrokes away. And its town size cancelled out, so
every non-producing port on earth would quote an identical number: two prices
per good in the whole world, with no geography between Lisbon, Manila and
Ternate.

The winner has one per-good knob whose effect on price is compressed by an
exponent of 0.556. Making musk a thousand times rice needs a 250,000 to 1 yield
ratio, so you cannot hit a price by nudging.

## What the probes established

**It settles.** 192 cases, six ports by eight goods by four starting stocks
including empty and glutted, 1200 ticks each. Zero non-monotone steps, zero
overshoots, zero out-of-band prices, worst residual 9.87e-13. Pure exponential
relaxation, no ringing. Half-life six ticks, at rest by tick 220 to 284.

**There is no money pump.** A round trip loses exactly 3.921569% at every size
in both directions, and a 20,000-sequence search for a closing cycle found best
net minus 0.056 coin.

**Relative value emerged and nobody wrote a price.** Musk is 96.5x rice at their
home ports. Silver ore runs 0.112 at Callao to 1.997 at Macao. Quicksilver 7.94
at Macao to 57.24 at Callao. Musk 13.4x from Macao to Lisbon, nutmeg 11.4x from
Banda to Lisbon.

**The factory strangles itself**, exactly as [DESIGN_FACTORIES.md](DESIGN_FACTORIES.md)
argued it would: a gun foundry takes cannon from 77.22 to 51.45 and copper from
13.21 to 15.16. That claim had been an argument since the day it was written.
It is now a measurement.

## The finding that matters: half a world

**A trader learns one scalar per port and knows all sixty seven of its prices.**

Town and hinterland cancel out of any ratio, so the price of one good in terms of
another is identical at every port that imports both. Cannon in nutmeg is
9.3587 at Callao, Lisbon and Macao alike. Macao and Ternate happen to share a
town to hinterland ratio and therefore quote bit-identical numbers, so there is
literally nothing to carry between them.

At full scale: musk costs exactly 3.513227 silver at all twenty six harbours
that produce neither. For the nine goods produced nowhere, the sale ranking of
all twenty nine harbours is one identical list, so route choice collapses to
picking the richest reachable port once and using it for everything. Distance is
two buckets, so Lisbon is exactly as far from Banda as Nagasaki is.

Ties are visible on one screen. At Malacca horses equals cannon, lacquerware
equals coral, tin equals ironwork equals benzoin. Any two goods with the same
yield are the same good economically.

This is the price the design knowingly paid for the law, and it is too high.

## The fix is already built

**An inelastic consumer.** A garrison, a temple, a shipyard: a works that eats
and yields nothing. It is the same mechanism as a factory and needs no new law
and no new field, because a headcount of institutions is a physical fact.

A works eating 2.0 nutmeg per tick at Lisbon takes it from 8.5526 to 15.6026.
One eating 1.0 tin at Macao takes it from 16.5497 to 30.3731. That is a port
wanting something in particular, which is the thing the flat surface cannot do.

**It needs a hand on it.** The response is steep once a consumer exceeds the
local flow: a garrison eating 0.05 cannon per tick at Ternate, against a base
flow of 0.0068, multiplies the price by 145, and 0.10 multiplies it by 821.

## Two other things to fix

**Godown capacity is backwards.** It is eighty ticks of the town's own
consumption, so the scarcer and dearer a good is, the less of it can be sold
there. Lisbon wants musk more than anywhere on earth, at 172.90, and absorbs
2.54 units before refusing, for 209 coin. Meanwhile Macao absorbs 1640 silver
ore. That is 626 to 1 on the route the world file's own comment calls the
galleon full in both directions.

**Recipe viability is emergent and unchecked.** With the probe's yield table the
silver refinery loses money at Callao and Acapulco, the only two places the ore
exists, and pays only at Macao where there is none. That is the yield table's
doing rather than the code's, but nothing anywhere tells an author that a recipe
has become unrunnable.

## Faults in the code

Three, recorded in the harbour's README rather than left to be found: a horizon
snap that deletes goods, a census that moves a price the wrong way on its first
piece of news, and a settling gate advertised as sufficient that is not.
