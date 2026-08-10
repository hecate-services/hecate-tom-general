# The layout

*This exists so a game of TOM runs on real boxes across a real mesh, and not on
one machine pretending to be many.*

**Status:** stated 2026-08-10. One constraint unresolved, see [Stations](#stations).

## The layout as asked for

| What | Where | Runtime |
|------|-------|---------|
| `hecate-tom-ocean`, one instance | `msi00.lab` | podman, Quadlet unit, `podman auto-update` |
| `hecate-tom-harbour`, eight instances | `beam00.lab` to `beam03.lab`, two per node | docker, watchtower |
| `hecate-tom-trader`, one instance | Raf's workstation | whatever is convenient. It dials out |

Each harbour dials a **different** `macula-station`. That is the point of the
exercise: eight harbours that are genuinely separate peers on the mesh, not
eight processes sharing one station and calling it distributed.

The harbours are meant to sit in North America, South America, Europe and Asia.

## Stations

Seven stations exist. All seven are in Europe. Source of truth is
`macula-io/macula-demo/infrastructure/FLEET.md`.

| Station | Box | Real location |
|---------|-----|---------------|
| `station-de-falkenstein` | stations-hetzner-falkenstein | Germany |
| `station-de-nuremberg` | relays-hetzner-nuremberg | Germany |
| `station-de-frankfurt` | macula.io | Germany. The name is a station name, not a location claim |
| `station-fi-helsinki` | relays-hetzner-helsinki | Finland |
| `station-fr-paris` | relays-linode-paris | France |
| `station-it-milan` | stations-linode-milan | Italy |
| `station-se-stockholm` | stations-linode-stockholm | Sweden |

Two things follow.

**Eight harbours need an eight station.** The options, cheapest first:

1. **Run seven harbours.** Four nodes carry two each except one, which carries
   one. Costs nothing and delays nothing.
2. **Stand a station up in the lab**, on a beam node or on `msi00`. Free, and
   the harbour dialling it gets lab-local latency while the other seven get WAN
   latency, which makes one harbour quietly different from the rest.
3. **Add an eighth box.** Real money, roughly five euros a month.

**Real geography is a separate decision from game geography.** If the four
continents are where the harbours *are in the story*, nothing further is needed
and the story is free. If they are meant to be real, so that sailing from Asia
to Europe costs real milliseconds, that is four to eight new boxes outside
Europe at roughly five euros a month each. Linode has Singapore, Tokyo, Mumbai,
São Paulo, Newark and Toronto, so it is possible, and it is the only part of
this layout that costs money.

**One known fault to route around.** `FLEET.md` records that `station-it-milan`
and `station-se-stockholm` currently resolve to the wrong boxes, and that the
retired-name prune has not run. Confirm what a name resolves to before pinning a
harbour to it.

## Ports

Health ports already bound across the fleet: 8450, 8471, 8481, 8482, 8483. The
beam nodes run host networking, so a collision is a silent bind failure that
looks exactly like a successful deploy. Two harbours per node means two free
ports per node, and they must be checked, not assumed.

## Storage

Application data goes on the `/bulk` drives, never on the eMMC root.

- `beam00.lab` has `/bulk0` only, plus `/fast`. It also has 16 GB of RAM against
  32 GB on the others, so if any node carries a single harbour rather than two,
  it is this one.
- `beam01.lab` to `beam03.lab` have `/bulk0` and `/bulk1`.

## Deployment paths, which are not the same

The two runtimes in this layout are genuinely different and have bitten before.

- **beam00 to beam03 run docker with watchtower.** CI pushes `:latest` to
  ghcr.io and watchtower recreates the container within seconds. Do not ssh in
  and restart things by hand.
- **msi00 runs podman with Quadlet units and `podman auto-update`**, driven by a
  timer. Do not put watchtower on it. Two supervisors fighting over one
  container is how the unit and the running thing drift apart.

A push to a default branch that is not path-filtered rebuilds `:latest` and
rolls every box watching it. Put `paths-ignore` for `**.md` on the image build
before the first harbour ships.

## The ocean

`hecate-tom-ocean` mimics travel, storms and pirates.

Not dragons. The word is retired.
