# Factories

*This exists so that something in the world consumes, and so a trader has a
reason to sail somewhere beyond guessing at prices.*

**Status:** agreed 2026-08-10. Recipes encoded in
`hecate-tom-world/priv/worlds/macao.world`. Factories as harbour state are not
built yet.

## Why

A harbour can build factories. A factory eats goods and makes other goods.

The reason is not depth, it is that **nothing in the world currently consumes**.
Every price move comes from a player, so the economy is a closed loop of traders
trading with each other. A factory that eats raw silk is a permanent bid for raw
silk at that harbour, whether or not any human wants silk that day.

## The property that makes it work

A factory arbitrages against its own market. Buy silk at Macao, weave it, sell
the cloth at Macao. If that margin were fixed it would print money forever.

It is not fixed, because **the factory moves the prices it trades against**. Its
buying pushes raw silk up and its selling pushes cloth down, and it strangles
itself at equilibrium within a few cycles.

To keep running it needs silk shipped **in** and cloth shipped **out**. That is
the whole value of the idea: a factory converts a price differential into a
standing demand for shipping. Factories generate routes. Nothing else in the
design does.

## Where each piece lives

| Thing | Is | Lives in |
|---|---|---|
| The recipe: two raw silk become one silk piece goods | Permanent, the same in every game | The world file, beside the goods |
| Knowing a recipe at a harbour | Changes every game | That harbour's service |
| A **copy** of a recipe | Cargo | A hold, a warehouse, a market |

`produces` in the world file stays what it is, the harbour's natural endowment.
A factory adds to it.

## Recipes as cargo

A recipe can be traded on a harbour market and carried across an ocean, so
knowledge diffuses the way it actually did. What travels is a **copy**, not the
recipe itself, exactly as a lot of pepper travels and the idea of pepper does
not.

**A copy is consumed when a factory is built from it.** Without that, copying is
free, the market floods and the price is zero by the afternoon. Consumed on
build, each copy is a real object with real demand.

**It behaves like no commodity.** Worth a fortune in a port that lacks the
knowledge, worthless in one that has it, and the value collapses the moment the
first copy lands. That is a ninth job for the enum, something like `singular`.

**And it is what makes the raw materials tier load-bearing.** If knowledge
travels, every harbour eventually knows everything and a uniform world has no
trade in it. What saves the map is that you can weave anywhere but silk only
grows in China. Geography binds the inputs even when the knowledge is universal.
Without a raw materials tier, recipe diffusion flattens the world.

## The cost, which was paid

Checked against the original forty five goods, **exactly one recipe was
possible**: raw silk becomes silk piece goods.

Everything else the world called a good was already finished. Porcelain had no
clay. Broadcloth had no wool. Cotton piece goods had no raw cotton. Gunpowder
needed sulphur, cordage needed hemp, cannon needed iron, and none of them
existed.

The goods list had been written as things worth carrying across an ocean, which
is close to the opposite of things worth making. So factories meant adding a raw
materials tier, and it was added in one deliberate act rather than creeping in a
recipe at a time. See [What was added](#what-was-added).

## What is validated, on load

- Inputs and outputs are goods the world knows.
- No recipe has the same good on both sides. That is a pump.
- Every input is obtainable, either plentiful at some harbour or made by a
  factory whose own inputs are obtainable. This is the check that caught camphor,
  applied one tier up.
- A cycle needs no separate check. It fails the rule above on its own, because a
  cycle never resolves, and the error names the inputs that went missing.

## The shipyard, which turned out to be an ordinary factory

This section used to say a shipyard was **not** a factory, because its output is
not a good, and to keep it separate so the recipe schema stayed simple.

That was a choice presented as a fact, and it is the choice that forced the
replacement hull to be free, since a thing that is not a good has no market and
therefore no price. Reversed 2026-08-11: **a hull is a good**, a shipyard is an
ordinary factory, and the recipe schema needs no change at all.

    build_hull: teak 40, ironwork 8, cordage 4, sailcloth 6 -> hull 1, 30 ticks

It also gives teak, oak and pine the consumer they have been waiting for since
they went in. One new thing is needed and only one: a hull is a good that cannot
be carried. See [DESIGN_LOSS.md](DESIGN_LOSS.md).

## Settled

| Question | Answer |
|---|---|
| What caps the number? | **Cost.** Factories are expensive to raise and goods cost money to make. Money is the wall, so `build` and `cost` sit on the recipe |
| Who owns one? | **The town.** The Harbour Master funds it and takes the tax on the traffic it draws. He never owns the output, so he never becomes a trader |
| Recipes as cargo? | **Yes, and the copy is destroyed on use.** One copy raises one factory |
| Raw materials tier? | **Yes**, including kinds of wood |
| Rate? | **On the recipe**, as `ticks` per batch |

## What was added

Eleven raw materials nobody would ship for their own sake: raw cotton, wool,
hemp, iron, kaolin, sulphur, and five kinds of wood.

**The woods are five, because timber is not one thing.** Teak from Malabar and
Siam, which the worm will not touch and which is why hulls were built at Goa and
Cochin. Oak from Europe. Pine for masts and spars. Ebony as a luxury cargo in its
own right. And brazilwood, the red dyewood, which incidentally repairs Bahia,
a harbour that until now made almost nothing.

Nine manufactured goods that come out of a factory and nowhere else: chintz,
cordage, sailcloth, gunpowder, cannon, ironwork, candles, incense, arrack.

Fourteen recipes. Forty five goods became sixty five.

**Ores for the two money metals.** There were none at all, and the hole showed
up as quicksilver, a good whose own description said it refines silver and which
nothing consumed.

Acapulco and Callao dig silver ore. Mozambique and Bantam dig gold ore, from the
reefs of Monomotapa and the Sumatran fields. Each refinery turns four ore and one
quicksilver into one metal.

So gold and silver each enter the world two ways: **found**, which is limited and
needs nobody, and **refined**, which needs ore, mercury and a works. Japanese
silver and river gold arrive from the first minute. American silver and reef gold
wait on somebody building the refinery, which is the order it happened in.

The second ore is not there for symmetry. **Macao is the only source of
quicksilver in the world**, and now two refineries bid against each other for it.
That is a bottleneck with a decision in it, which is the test any new content
should have to pass.

The other six metals get no ore, deliberately. Ore did not cross oceans and metal
did, since Malayan tin was smelted at the mine and shipped as ingots and Japanese
copper as bar. An ore tier for those would invent a trade that never existed and
add a step with nothing to decide.

Teak, oak and pine have no recipe yet. They are honest trade goods in the
meantime, as timber genuinely was, and they are waiting for the shipyard.

## Still open

**Units.** A recipe is a ratio, so goods must be measured in comparable units.
Proposed and not yet taken: one unit for everything, with price carrying all the
value difference. A hold of silver and a hold of pepper then take the same space
and are worth wildly different money, which gives value density for free and
needs no second field. This would also settle the open question in
[DESIGN_GOODS.md](DESIGN_GOODS.md).
