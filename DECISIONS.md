# Decisions

*This exists so that a settled question stays settled, and so that reopening one
is a deliberate act rather than a slow drift.*

| Date | Question | Decision |
|------|----------|----------|
| ~~2026-08-10~~ **revised 2026-08-11** | How many player roles? | ~~Two: Harbour Master and Trader~~ → **Three: Magnate, Trader, Mayor**, in one install. Affordable again because the harbour became infrastructure, so a mayor's seat may stand empty and the port still runs |
| 2026-08-10 | Which goods can be traded? | Forty five trade goods, recorded in [design/DESIGN_GOODS.md](design/DESIGN_GOODS.md). Sixty seven since the raw materials tier |
| 2026-08-10 | Are slaves tradeable? | **No.** Historically part of Macao's trade, excluded by decision |
| 2026-08-10 | What is `tom-general`? | Plans, designs, guides, decisions. No code |
| 2026-08-11 | Is there a shared domain library? | **No.** One service owns an artifact, the others consume it. Shared domain types couple every service to one shape and force lockstep upgrades. Services link `macula` and nothing of ours |
| ~~2026-08-10~~ **reversed 2026-08-11** | One code library or two? | ~~One, `tom-shared`~~ → **None.** A shared domain library is DRY gone wild, and it forces the lockstep upgrade an event stream exists to avoid. `tom-shared` became `hecate-tom-world`, which owns reference data and publishes facts |
| 2026-08-10 | Application and module naming | App name agrees with the repo (`hecate_tom_world`). Modules take the short `tom_` prefix, because they appear at every call site in every service |
| 2026-08-10 | What hazards does the ocean carry? | Travel, storms and pirates. **The word "dragons" is retired** |
| 2026-08-10 | What does a harbour trade? | **Everything.** Every harbour has a market where every good buys and sells at the going price. A harbour declares only what is plentiful there; demand is the complement and is never written down |
| 2026-08-11 | **Is price ever fixed data?** | **No. Price is always circumstantial.** A law. Nothing in world data is ever a price, and anything that looks like one is a market fact in the wrong file |
| 2026-08-11 | Can a good be withdrawn or a harbour closed? | **No.** The world is strictly append-only. Withdrawing a good somebody holds forty tons of is the one change that would break a running game |
| 2026-08-11 | Can a recipe be retuned or retired? | **No.** You cannot un-invent a process. A better one is a new recipe beside the old, and the old keeps working for whoever holds a copy |
| 2026-08-11 | Is a harbour a player or infrastructure? | **Infrastructure.** A port's market must be one number everyone agrees on and must not go dark when somebody shuts a laptop. One service per port, owned by nobody |
| 2026-08-11 | What replaces the Harbour Master? | **Magnate** (makes) and **Mayor** (permits), alongside the Trader (moves). The Harbour Master was a rentier taxing other people's work; tax is now a sink and nobody's lever |
| 2026-08-11 | How many services does a player install? | **One**, `hecate-tom-house`. One service per **owner**, not one per role. A mayor is elected by magnates and is one of them, so he cannot live in a different binary |
| 2026-08-11 | Who may mint money? | **Anyone with silver, by default.** A mayor's power is to *reserve* the mint to himself, which is a plank he stands on. A monopoly leaks to the nearest free port |
| 2026-08-11 | What holds inflation down? | **The mint par.** A coin is a fixed weight of silver, so striking pays only while silver is below par. Nobody sets it, and a weight is not a price |
| 2026-08-11 | What is an election about? | **Policy.** Tax rate, mint stance, bans, works. The platform is binding and discretionary acts happen inside it |
| 2026-08-11 | Do goods carry a `jobs` enum? | **No, deleted.** `contraband` is a harbour's decision, `money` is the medium of exchange, `bulk`/`floor`/`trap` are price facts, `exclusive` is derived. Only `fragile` and `perishable` were real, and both want a number, so they return with storms and time |
| 2026-08-11 | How are things named on the mesh? | **MRI**, `mri:class:{realm}/tom/{kind}/{name}`, built with `macula_mri`. World-file names are local and never leave the node as-is |
| 2026-08-11 | How do peers know they share a world? | **`tom_world:digest/1`**, a sha256 over the world's content. Exchange it, refuse to trade with a peer whose world is not yours |
| 2026-08-11 | `regions` or `origins` on a good? | **`origins`.** A harbour's `region` is where it is; a good's `origins` are where it comes from. Different relations, so different words |
| 2026-08-11 | Do we have ores? | **Two.** Silver ore and gold ore, both refined with Chinese quicksilver. The other six metals crossed oceans as metal, so they get none |
| 2026-08-10 | Are goods and harbours code or data? | **Data.** `tom-world` owns the map a good is and the map a harbour is. They live in `hecate-tom-world/priv/worlds/macao.world`. There is no closed vocabulary left in it |
| 2026-08-11 | Is every key on the wire a binary? | **On the way out, yes. On the way in, no, and no contract can make it so.** macula encodes a binary key as a CBOR text string and `binary_to_existing_atom`s it back, so a key arrives as an **atom** or as **`{text, Binary}`** depending on what the receiving node has loaded. Each service folds inbound payloads back to binary keys at its own edge. See below |
| 2026-08-11 | How does a refusal carry its reason? | **As a successful reply, `{ok, #{<<"refused">> => Reason}}`.** ~~`{error, Binary}`~~ loses the reason: macula renders it into a BOLT#4 `detail` the SDK's caller path drops, so every refusal arrives as one `{call_error, 15, unknown_error}`. Changed on the **harbour** (producer) and the **house** (consumer). The ocean keeps `{error, _}`, because nothing reads its reasons |
| ~~2026-08-10~~ **revised 2026-08-11** | Where does it all run? | ~~Ocean on `msi00`~~, eight harbours two apiece on `beam00` to `beam03`, trader on Raf's workstation. Each harbour dials a different station. **The ocean is gone; there is nothing on `msi00`.** See [design/DESIGN_DEPLOYMENT.md](design/DESIGN_DEPLOYMENT.md) |
| 2026-08-11 | Is there a service for the sea? | **No. `hecate-tom-ocean` is dissolved.** An ocean is a place, and a place is not a party. Made a service, it had to become one, and grew custody, an archive and an outbox to suit. See [design/DESIGN_VOYAGE.md](design/DESIGN_VOYAGE.md) |
| 2026-08-11 | What was missing? | **The voyage, as a live thing.** She was a record in another process's state, so every question about a ship under way had to be asked of the sea, and the sea grew one answer per question |
| 2026-08-11 | Where does a passage run? | **At the port she sailed from, for the leg she is on.** Nothing in the domain has a claim on hosting her, so the choice is operational, and operationally: no singleton, one hop per leg, and `hop` becomes geography instead of a custody counter |
| 2026-08-11 | Custody, or hosting? | **Two words, never merged again.** The voyage is the custodian of the hull; the port is only the host of the process. A port hosting a ship four hundred leagues away is not a lie about where she is |
| 2026-08-11 | How far does one voyage go? | **One leg.** The house orders the next port at each stop. The route graph already chains, so Macao to Lisbon is three legs. No itineraries, no path-finding, and every stop is a market and a decision |
| ~~2026-08-11~~ **revised same day** | Who owns "how long"? | ~~The ocean~~ → **distance is the world's, duration is the passage's.** [DESIGN_PLACES.md](design/DESIGN_PLACES.md) was right that a passage time is weather and hull, but distance was never separated from duration, so both went to the sea and the map got neither |
| 2026-08-11 | Where do measure and exposure live? | **On a leg, not a route.** A route already carries `via`, so it is already segmented. Length is then derived, adding a waypoint recomputes it, and the dangerous part can be the strait rather than the whole crossing |
| 2026-08-11 | What belongs in the world? | **What everyone must agree on. The service holds the computation.** The market already worked this way by accident: `tom_crossing`'s eleven constants are agreements, the bisection is the harbour's business. Leagues, exposure, tempo and hazard are the same |
| 2026-08-12 | How many kinds of service are there? | **Two. `tom-world` runs places, `tom-player` runs people.** One service per **owner**, applied all the way: what nobody owns and must not go dark is one binary, what a person owns and may switch off is the other. See [design/DESIGN_TWO_SERVICES.md](design/DESIGN_TWO_SERVICES.md) |
| 2026-08-12 | Is a harbour, a fort or a trading post a different service? | **No. Same binary, different configuration**, which [design/DESIGN_PLACES.md](design/DESIGN_PLACES.md) had already settled for waypoints. A harbour is a place with a market and an electorate, a fort is a place with a garrison and no market. The binary is the world; an instance is a place |
| 2026-08-12 | Is `tom-world` one process? | **Never.** One binary, one instance per place, each dialling a different station. A singular name invites the singleton the ocean just died of: `msi00` down meant nothing sailed anywhere |
| 2026-08-12 | Does world data reach a place by facts or by a function call? | **By a function call, because after this they are one service.** The no-shared-library rule is *unchanged*: it was written because services run on their owners' laptops, and places do not. Places are eight instances under watchtower, owned by the steward, rolled in seconds. The rule hardens where it earns its keep, at the player, who links `macula` and nothing of ours |
| 2026-08-12 | How does a player learn what exists? | **A versioned artifact, checked by `tom_world:digest/1`.** Not the nine events of [design/DESIGN_WORLD.md](design/DESIGN_WORLD.md), which are unbuilt and now have no consumer. Permanent, additive, never-deleted data does not need a log to be caught up on. The events return the day a good is introduced at runtime without rolling the fleet |
| 2026-08-12 | Bot or human? | **One binary, one command surface, two drivers.** A page or a policy, both calling the same desks. The seam exists already: the page posts to `/act`. Two code paths get written twice, drift, and the bot quietly becomes the one that works |
| 2026-08-12 | What is the bot for? | **It is an instrument before it is an opponent.** A bot arbitraging two places drives the gap to the crossing, so the expectation is that it flattens the map in an hour and the world goes quiet. That finding decides whether the magnate is the next build, and it costs a day instead of a fortnight |
| 2026-08-13 | Which repository survived the merge? | **The harbour**, renamed to `hecate-tom-world`, because its history stays attached to the code that gets worked on next. Archiving frees no name on GitHub, so the old one went to `hecate-tom-world-superseded` and was archived there. Local checkout in `hecate-services/.attic/` |
| 2026-08-13 | Does `house` survive inside `hecate-tom-player`? | **Yes, as the estate.** A player is the person; a house is what they keep. Only the service was renamed: app, repo, release, container. `tom_house` is still the aggregate and `keep_house` still owns the purse |
| 2026-08-13 | Does the mesh name of a port change? | **No.** `tom/harbour/<name>` is an MRI, which three services agree on, and a place with a market is a harbour. `TOM_HARBOUR`, `priv/harbours/` and the node name stay with it. The rename was of the service, not of the world |
| ~~2026-08-11~~ **revised 2026-08-12** | How many services does a player install? | **One**, ~~`hecate-tom-house`~~ → **`hecate-tom-player`**. One service per **owner**, not one per role. A mayor is elected by magnates and is one of them, so he cannot live in a different binary. Renamed because the binary now holds bots as well as houses, and a bot keeps no house |

## 2026-08-10: two player roles, not three

The brief opened with three: Harbour Master, Trader, Ship Master. The Ship Master
is folded into the Trader, who now trades the goods and keeps the boats and ships
that carry them.

**What this buys.** A game needs two humans to start, not three. The hardest
moment in the whole protocol, handing a laden ship across the quay, drops from
three signatures to two, because the ship and the cargo now have the same owner.
And the sharpest decision in the game moves inside one player's head: every
florin put into another hull is a florin not put into another lot.

**What it costs.** The charter market is gone, and with it the negotiation of
freight rates between two strangers, and the clean split between price risk and
hull risk. Those were good, and they needed a third player who might be asleep.

**What is unaffected.** Title and custody stay separate exactly as before. The
Trader holds title to both ship and cargo; custody still moves harbour, ocean,
harbour, and still moves only against the title-holder's signature or a standing
order they pre-signed.

**Moot as a result.** Whether to rename `tom-ship-master`. There is no such repo
and no such role. For the record, the answer to the question that prompted it:
Dutch *rederij* is a shipowning firm, *reder* is a shipowner, and the English
term for the managing role, the party who provisions, repairs, crews and charters
a ship without sailing her, is *ship's husband*. Those functions now belong to
the Trader.

## 2026-08-10: no slaves

Macao's trade included them. They are excluded from the goods, recorded here so
the absence reads as a decision rather than an oversight, and so nobody adds them
back believing they were forgotten.

## 2026-08-11: what the wire actually does, found by running it

The three services were built in parallel against a frozen contract and none of
them had spoken to a station. Running all four together for the first time broke
on two things the contract asserts and the wire does not honour. Both fail
**silently**: every service reports perfect health and nothing works.

### A key does not arrive in the shape it was sent

The contract says *every map key on the wire is a BINARY*. That is true of what a
sender writes and false of what a receiver gets.

macula encodes a binary key as a CBOR text string (major 3). On the way back in,
`macula_frame:from_wire_envelope/1` runs `binary_to_existing_atom` over every
key: one whose name is already in the **receiving node's** atom table comes back
as an **atom**, one whose name is not comes back as **`{text, Binary}`**. A
single receipt carries both — `coin` as an atom beside `{text, <<"price_after">>}`.

The nasty part is that this is a property of the receiver, not of the message.
Load any module that happens to mention the atom `good` and every payload
afterwards is shaped differently, with no version change and no error.

**Decision: each service folds inbound payloads back to binary keys at its own
edge, and nowhere else.** No shared library, no change to macula. The fold mints
no atom — it only ever unmakes one the decoder already had, so the atom table
cannot be walked from the wire.

| Service | Fold | Applied at |
|---|---|---|
| harbour | `tom_wire:accept/1` | `tom_port:ask/1` (all seven desks), and the handover reply in `tom_hand_over_ship` |
| ocean | `tom_wire:accept/1` | `take_ship_to_sea`, `tell_voyage`, and the reply in `tom_ocean_mesh` |
| house | `tom_wire_accept:payload/1` | every reply in `tom_wire_macula:call/3`, every fact in `watch_ports` |

### A refusal's reason does not survive `{error, Binary}`

macula turns a handler's `{error, Reason}` into a BOLT#4 frame with code `0x0F`,
renders the reason into the frame's `detail`, and the SDK's caller path reads
only `code` and `name`. `quay_empty`, `hold_full`, `not_here`, `not_yours`,
`ship_consigned`, `godown_full`, `not_in_hold`, `bad_destination` and
`already_bound` all arrive at a house as one indistinguishable
`{call_error, 15, unknown_error}`, so a player is told an order failed and never
why.

**Decision: a refusal travels as a successful reply carrying its reason.**

```erlang
{ok, #{<<"refused">> => <<"hold_full">>}}
```

The harbour's desks still return `{error, Binary}` internally, because that is
what a refusal is to a port; `tom_wire:answer/1` translates at the edge, once.
The house reads the shape in `tom_wire_macula:classify/1` and still calls it
**refused**, so it is still final and the retry loop is unchanged.

**Which side changed:** the **harbour** (producer) and the **house** (consumer).
The **ocean is unchanged** and still answers `{error, <<"malformed_handover">>}`,
deliberately: a malformed handover is a sender with a bug, the custody rule
forbids refusing a well-formed one, and every consigner retries on anything that
is not `held`, so that reason has no reader.

**The alternative, not taken.** Carrying `detail` through to the caller in
`macula_station_link:on_frame/2` is one line and is arguably the better fix. It
changes the published SDK the rest of the fleet runs, and it would put this
game's contract on an unreleased macula. Worth doing in macula on its own merits;
this game does not wait for it.

## 2026-08-11: dissolving the ocean is smaller than it sounds

Reading the harbour before rewriting it turned a rebuild into a rewiring.

`tom_hand_over_ship` is already one process per consigned hull that retries every
five seconds forever, resumes at boot from its own record, and sends a
byte-identical payload every attempt so the receiver dedupes on `{ship, hop}`. It
is generic over a destination and a procedure, and it happens to point at the
ocean. `tom_receive_ship` already takes a hull idempotently on the other side.
And `tom_sail_ship:consigned/4` freezes the berth and keeps the hull in the
port's own `ships` map until the receiver says held.

So the harbour already does port-to-port handover, in both directions, durably,
with retry, and already holds a hull it has consigned. **The ocean is a delay
inserted between two halves that already exist**, and what the harbour lacks is
exactly what the ocean owned: a clock and a fate.

The knocking comes back with it, and that is not a regression. It was ugly as a
worker pool the sea ran per undelivered landfall, and ugly again as an outbox
with a cursor and a `taken` flag, because in both shapes a delivery obligation
was a side table on a central actor. As the ship's own behaviour there is no side
table, because there is nothing beside her: she reaches a dark port, lies in the
roads, and waits for them to open.

## 2026-08-12: two services, and the boundary that was in the wrong place

**The world runs places. The player runs people.** Full reasoning in
[design/DESIGN_TWO_SERVICES.md](design/DESIGN_TWO_SERVICES.md); what belongs
here is why it is not a reversal, and how small it is.

### The rule that looked broken is not

"No shared domain library" was decided on 2026-08-11 with this justification: a
harbour that must link a new schema to understand a new good means every player
upgrades in lockstep, and in a game whose services run on their owners' laptops
that is a standstill.

The premise is true and it does not describe a harbour.
[design/DESIGN_DEPLOYMENT.md](design/DESIGN_DEPLOYMENT.md) puts eight of them two
apiece on `beam00` to `beam03`, under watchtower, owned by the steward. Rolling
them is one push and a few seconds, and nobody is asked. The laptops in that
sentence are the players, and only the players.

So the rule was written for one boundary and enforced at two. Merging the world
into the place does not weaken it. It deletes a boundary the rule was policing
for no one, and leaves the rule standing where the whole argument came from.

### It is one repository

Five today. [design/DESIGN_VOYAGE.md](design/DESIGN_VOYAGE.md) already takes it
to four. This takes it to three, of which one holds no code. Anyone reading
"reduce to two services" as a large consolidation should read it again as what it
is: the last step of one already under way, plus two renames.

**The substance is the role model and the bot**, and both are additions rather
than a restructure.

### The shape was already found twice, in the same document

[design/DESIGN_PLACES.md](design/DESIGN_PLACES.md) got there on 2026-08-11
without generalising it. A fort is a harbour without a market, same service and
different configuration. Holders can be bots, one release, some instances driven
by a human through a page and some by a policy, no new kind of service anywhere.

That is exactly this decision, stated about waypoints. A design that keeps
arriving at the same shape from different directions is usually being told
something.

### What is deliberately not fixed

The purse is on the player and nothing checks it, so a cheat and a bot are the
same binary with different configuration. There is no better home for it: money
is not local to a place. Recorded so the absence reads as a decision, exactly as
`tom_buy_cargo` already records that `not_yours` is a check against a mistake and
not against an attacker.
