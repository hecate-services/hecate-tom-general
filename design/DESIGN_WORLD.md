# The world service

*This exists so that adding a good does not require eight people to redeploy
their laptops on the same afternoon.*

**Status:** stormed 2026-08-11. Nothing built beyond the model it will own.
Six hotspots at the bottom, all open.

`hecate-tom-world` owns reference data: what goods exist, what ports exist, what
can be made from what. It publishes facts. **Nobody links it.** Harbours and
traders consume those facts and build whatever read model suits them, which is
why there is no shared library.

## The events

Every one of these is a statement about what the world contains. None of them is
about a game in progress.

| Event | What it means |
|---|---|
| `world_founded_v1` | This world exists, with an id and a name. Happens once, from the genesis file |
| `region_named_v1` | A region exists, and goods and harbours may now refer to it |
| `good_introduced_v1` | A good can be traded. Carries its id, name, origins and character |
| `good_described_v1` | Its display name or its line of character changed. Its identity did not |
| `good_origins_revised_v1` | The regions it comes out of changed |
| `good_withdrawn_v1` | It can no longer be traded. Refused while any recipe eats it or any harbour produces it |
| `harbour_opened_v1` | A port exists on the map, in a region. Carries its name and character |
| `harbour_described_v1` | Its display name or line of character changed |
| `harbour_produce_revised_v1` | What is plentiful there changed, so what is cheap there changed |
| `harbour_closed_v1` | The port is off the map. Refused while it is the only source of a good |
| `recipe_published_v1` | A factory of this kind can be built. Carries inputs, outputs, build, cost, ticks |
| `recipe_reformulated_v1` | What it eats or what it makes changed |
| `recipe_retuned_v1` | Its numbers changed: what it costs to build, what a batch costs, how long a batch takes |
| `recipe_retired_v1` | No new factory of this kind can be built |
| `edition_sealed_v1` | The catalogue as it stands is frozen and numbered. A game pins one of these and is unaffected by later changes until it adopts a newer one |

Commands are the present tense of each, with the usual handlers:
`introduce_good_v1` and `maybe_introduce_good`, `open_harbour_v1` and
`maybe_open_harbour`, `seal_edition_v1` and `maybe_seal_edition`. One desk per
capability.

There was a `good_renamed_v1` and a `good_recharacterised_v1` and they were the
same event twice. The id is the identity; everything else is display. One
`good_described_v1` covers both.

## Two things the storm decided

**The invariants force one aggregate.** "Every recipe input must be obtainable"
and "every good is plentiful somewhere" cannot be checked from inside a Good.
They are world-level truths, so the consistency boundary is the **World**, and
goods, harbours and recipes are entities inside it rather than child aggregates.
The cost is one long stream with a single writer, which for reference data that
changes a few times a week is not a cost at all.

**Editions answer mid-game change.** `edition_sealed_v1` names an immutable
point: a position, a digest, a label. A game **pins an edition**. The steward
keeps curating, changes land in the stream, and a running game is untouched until
it deliberately adopts a newer edition.

That is the thing that started all of this. A player who is behind is not broken;
they are on an older edition and can see exactly how far behind they are.

## What gets published, which is not the log

Two facts, not a firehose of domain events. The log is this service's business.

| Fact | Carries |
|---|---|
| `tom.world.edition_sealed` | World, edition, digest, stream position |
| `tom.world.catalogue` | The whole catalogue at a given edition, in one answer |

A newcomer asks for the catalogue at the current edition and gets sixty seven
goods in one call rather than replaying five hundred events. After that it
follows changes.

## Genesis

`macao.world` is not gospel, it is **genesis**. The service replays it once at
founding into `world_founded`, `region_named`, `good_introduced`,
`harbour_opened` and `recipe_published`, and from that moment the log is the
truth and the file is history.

The file stays, because it is the readable place to author a new world.

## Hotspots

All open. Each one changes what gets built.

**1. A retuned recipe under a running factory.** A harbour built a powder mill at
edition 3, the game adopts edition 4, and the mill's costs moved underneath it.
Grandfather the mill on the edition it was built at, or apply the new numbers
immediately? This needs an answer before any of it is built.

**2. Who is the steward?** One key, the realm, or a rotating referee. Governance,
not engineering.

**3. Where does a refusal go?** `good_withdrawn` can be refused because a recipe
still eats it. A refusal is not an event, so the steward needs to be told, which
means the command side needs a reply path and not just a stream.

**4. Do harbours belong here at all?** The map of twenty nine ports is reference
data and clearly does. "Raf runs Macao this game" is session state and clearly
does not. The line is obvious in those two cases and needs stating for the ones
in between.

**5. Genesis idempotency.** Replaying the file twice must not double the world.
A founding guard, probably, but it should be named rather than assumed.

**6. Is a region an entity or a value?** It has an id and a name and nothing
else, and exists only to be referenced and validated. Thin either way, and worth
deciding before something hangs off it.
