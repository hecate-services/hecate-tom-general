# The world service

*This exists so that adding a good does not require eight people to redeploy
their laptops on the same afternoon.*

**Status:** stormed 2026-08-11, then cut down the same day. Nothing built beyond
the model it will own. Five hotspots at the bottom, all open.

Eleven events, not fifteen. Recipes turned out to be permanent, which deleted
three of them and the whole edition mechanism with them.

Two of the eleven are still doubtful. `good_withdrawn_v1` and `harbour_closed_v1`
are the only destructive things left, and withdrawing a good somebody is holding
forty tons of is the one change that really would break a running game. The world
may want to be strictly append-only.

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
| `recipe_published_v1` | A process was invented. Carries inputs, outputs and how long a batch takes. **This is the only recipe event there will ever be** |

Commands are the present tense of each, with the usual handlers:
`introduce_good_v1` and `maybe_introduce_good`, `open_harbour_v1` and
`maybe_open_harbour`, `publish_recipe_v1` and `maybe_publish_recipe`. One desk
per capability.

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

**A recipe cannot be un-invented, so the world only grows, so editions are not
needed.** There was going to be an `edition_sealed_v1`, freezing a numbered
snapshot for a game to pin, protecting a running game from a change that might
break it.

Nothing can break it. A recipe is permanent: a better process is a new recipe
published beside the old, and the old keeps working for whoever holds a copy. No
retuning, no reformulating, no retiring. Nothing else is destroyed either.

So a peer that is behind simply knows fewer things. It can still trade everything
it knows about, and it cannot trade the new good until it catches up. That is a
soft failure, and it needs no version pinning, no digest agreement and no
adoption ceremony.

It also makes "which gunpowder recipe do you hold" a real question, since an
older, hungrier process still runs and still competes.

## What gets published, which is not the log

Two facts, not a firehose of domain events. The log is this service's business.

| Fact | Carries |
|---|---|
| `tom.world.catalogue` | The whole catalogue as it stands, in one answer |
| `tom.world.grew` | What was added, since that is the only thing that ever happens |

A newcomer asks for the catalogue and gets sixty seven goods in one call rather
than replaying five hundred events. After that it follows what was added.

## Genesis

`macao.world` is not gospel, it is **genesis**. The service replays it once at
founding into `world_founded`, `region_named`, `good_introduced`,
`harbour_opened` and `recipe_published`, and from that moment the log is the
truth and the file is history.

The file stays, because it is the readable place to author a new world.

## Hotspots

All open. Each one changes what gets built.

**1. Who is the steward?** One key, the realm, or a rotating referee. Governance,
not engineering. And if recipes are inventions rather than decrees, could players
invent them in play rather than receiving them from a curator?

**2. Where does a refusal go?** `good_withdrawn` can be refused because a recipe
still eats it. A refusal is not an event, so the steward needs to be told, which
means the command side needs a reply path and not just a stream.

**3. Do harbours belong here at all?** The map of twenty nine ports is reference
data and clearly does. "Raf runs Macao this game" is session state and clearly
does not. The line is obvious in those two cases and needs stating for the ones
in between.

**4. Genesis idempotency.** Replaying the file twice must not double the world.
A founding guard, probably, but it should be named rather than assumed.

**5. Is a region an entity or a value?** It has an id and a name and nothing
else, and exists only to be referenced and validated. Thin either way, and worth
deciding before something hangs off it.
