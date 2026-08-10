# Factories

*This exists so that something in the world consumes, and so a trader has a
reason to sail somewhere beyond guessing at prices.*

**Status:** proposed 2026-08-10. Not agreed. Nothing built. Five open questions
at the bottom.

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

## The cost nobody should discover later

Checked against the forty five goods, **exactly one recipe is possible today**:
raw silk becomes silk piece goods.

Everything else the world calls a good is already finished. Porcelain has no
clay. Broadcloth has no wool. Cotton piece goods have no raw cotton. Gunpowder
needs sulphur, cordage needs hemp, cannon needs iron, and none of those exist.

The goods list was written as things worth carrying across an ocean, which is
close to the opposite of things worth making. So factories mean adding a **raw
materials tier** that nobody would ship for its own sake: raw cotton, wool,
timber, iron, clay, sulphur, hemp. Seven or eight. Plus the outputs they justify:
cordage, canvas, gunpowder, candles, incense, arrack, cannon.

That is the real price of the idea. It should be one deliberate decision, not
something that creeps in a recipe at a time.

## What to validate

- Inputs and outputs are goods the world knows.
- No recipe has the same good on both sides. That is a pump.
- The recipe graph is acyclic.
- Every input is obtainable, either plentiful at some harbour or made by another
  recipe. This is the check that caught camphor, applied one tier up.

## Not a factory

A **shipyard**, turning timber and iron and cordage and canvas into a hull, is
the strongest possible link between the Harbour Master and the Trader. It is not
a factory, because its output is not a good. Keep it a separate thing so the
recipe schema stays simple.

## Open

1. **What caps the number?** Free factories mean the optimal play is build
   everything and the decision disappears. The wall should be ground: factories
   compete with berths and warehouses for the same finite quay.
2. **Who owns one?** Proposed: the town owns it, the Harbour Master funds and
   licenses it, and his return is the tax on the traffic it creates. If he owns
   the output he becomes a trader and the two roles blur.
3. **The raw materials tier.** Yes or no, and if yes, which.
4. **Units.** A recipe is a ratio, so goods must be measured in comparable
   units. Proposed: one unit for everything, with price carrying all the value
   difference. A hold of silver and a hold of pepper then take the same space and
   are worth wildly different money, which gives value density for free and needs
   no second field. This also settles the open question in
   [DESIGN_GOODS.md](DESIGN_GOODS.md).
5. **Rate.** A factory presumably converts so much per unit of time, and time is
   not decided.
