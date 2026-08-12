# The layout

*This exists so a game of TOM runs on real boxes across a real mesh, and not on
one machine pretending to be many.*

**Status:** stated 2026-08-10.

**Stations are infrastructure. They have nothing to do with where a harbour is
in the game.** A harbour sitting in Macao may dial a station in Helsinki. The
station is how its service reaches the mesh, and that is the whole of its
involvement. Do not read a station name as a place in the story.

## The layout as asked for

| What | Where | Runtime |
|------|-------|---------|
| `hecate-tom-ocean`, one instance | `msi00.lab` | podman, Quadlet unit, `podman auto-update` |
| `hecate-tom-world`, eight instances | `beam00.lab` to `beam03.lab`, two per node | docker, watchtower |
| `hecate-tom-player`, one per player | the player's own machine | whatever is convenient. It dials out |

⚠ **Revised 2026-08-13.** The row that read `hecate-tom-harbour`, eight
instances, is now `hecate-tom-world`: same eight processes, same two per node,
one binary that carries the world's data with it. The separate one-instance
world row is gone, and with it the question of where it ran. The ocean row goes
when [DESIGN_VOYAGE.md](DESIGN_VOYAGE.md) lands. See
[DESIGN_TWO_SERVICES.md](DESIGN_TWO_SERVICES.md).

Each harbour dials a **different** `macula-station`, so that eight harbours are
genuinely separate peers on the mesh rather than eight processes sharing one
station and calling it distributed.

**The harbours are infrastructure, not players.** A port's market has to be one
number everyone agrees on and it must not go dark when somebody shuts a laptop.
What a player installs is `hecate-tom-house`, which holds their works, their
ships and their seat if they hold one.

The eight harbours are placed around the world in the game: North America, South
America, Europe, Asia. That is the map, and it costs nothing.

## Stations

Seven exist. Source of truth is
`macula-io/macula-demo/infrastructure/FLEET.md`.

`station-de-falkenstein`, `station-de-nuremberg`, `station-de-frankfurt`,
`station-fi-helsinki`, `station-fr-paris`, `station-it-milan`,
`station-se-stockholm`.

Eight harbours over seven stations means either one pair shares a station, which
changes nothing that matters, or an eighth station goes up in the lab, which is
free. Assignment is arbitrary. Any harbour can dial any station.

One fault to route around: `FLEET.md` records that `station-it-milan` and
`station-se-stockholm` currently resolve to the wrong boxes, and that the
retired-name prune has not run. Check what a name resolves to before pinning a
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
