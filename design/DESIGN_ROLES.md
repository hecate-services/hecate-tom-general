# The roles

*This exists so that a player installs one thing, and so that what they can do
in the world is obvious from what they are called.*

**Status:** proposed 2026-08-11. The mayor especially. Nothing built.

## The law this rests on

**Price is always circumstantial.** No role sets what anything is worth. Every
lever below is a permission, a construction or a movement, never a number
attached to value.

## Three roles, one install

| Role | Power | Fixed or mobile |
|---|---|---|
| **Magnate** | Makes. Builds works at a home port, buys inputs and sells outputs on that market | Fixed |
| **Trader** | Moves. Owns ships, carries goods between ports, profits on the difference across space | Mobile |
| **Mayor** | Permits. Bans, charters, quarantine, public works | Fixed, and elected |

**The magnate makes, the trader moves, the mayor permits.**

Each needs the others. A magnate's factory strangles itself unless somebody
ships inputs in and outputs out, since its own buying lifts the input price and
its own selling depresses the output price. A trader has nothing worth sailing
for unless somebody somewhere is turning cheap things into dear ones.

## All three in one service

`hecate-tom-house`. A player installs one thing.

**One service per owner, not one service per role.** `tom-world`, `tom-harbour`
and `tom-ocean` are separate because they are owned by different parties and have
different availability needs. Magnate, trader and mayor are the same person's
stuff: same box, same identity, same money, same web page. Splitting them buys
nothing and costs an install.

The mayor settles it on his own. He is elected by the magnates of a port and is
one of them. Nobody can be elected by their peers from a different binary.

Vertical slices inside, not a mush:

| Slice | Holds |
|---|---|
| `keep_works` | Factories, recipes held, what is being made |
| `run_fleet` | Ships, voyages, cargo |
| `hold_office` | The seat, and what is done with it |

A trading house owns works, owns ships and sometimes holds a seat, which is what
the Portuguese and Dutch houses were. `hecate-tom-player` is the plain
alternative if the flavour is not worth it.

## What a mayor holds

Never a price. Permissions and public works only.

**Bans.** Contraband is a harbour's decision and not a good's property: opium is
banned in China and legal in Bengal. Banning is real politics. Ban imported cloth
and the weavers at your port are protected while every trader is worse off.

**Charters.** Grant one magnate the exclusive right to weave silk here for a
season.

**Quarantine.** Admit the plague ship and risk the port, refuse it and lose the
trade.

**Public works.** Dredging, a lighthouse, harbour defence.

**The mint.** Coinage is **free by default**: in an ungoverned port anyone with
silver may strike it. A mayor's power is to **reserve** the mint to himself, and
then tax buys silver and the mint turns it into money, which is the engine the
seat was lacking. Reserving it is a plank he stands on, and a monopoly leaks,
because silver can always be carried to the nearest free port. See
[DESIGN_MONEY.md](DESIGN_MONEY.md).

**The tax rate.** Which was the Harbour Master's lever and was cut with him,
because a rentier setting his own toll is not a game. An elected mayor standing
on a rate and answering for it is a different thing.

**Public works consume goods**, bought with coin the mayor struck. Timber,
ironwork, stone. That is how new money reaches circulation and how the works get
built, in one act.

## The empty seat

**A port with no mayor must work.** Default policy is everything permitted and
nothing built, which makes an ungoverned port a **free port**.

That is Macassar, exactly as it was: the place where whatever was banned
elsewhere got sold, and where anyone with silver could strike their own coin. So an empty seat is not a gap in the game, it is a kind of
port, and the absence of a player is part of the fiction rather than a hole in
it.

This is also why a third role is affordable now and was not before. The harbour
is infrastructure, so the seat can stand empty. When the harbour was a player,
an absent player meant a dead port.

## Elections are fought on policy

**A candidate stands on a platform**, and financial policy is on it like
everything else: the tax rate, the mint stance, what is banned, what gets built.
Magnates vote for the policy they want, not the person they like.

**The platform is binding.** Winning enacts it, and changing it needs another
election. The mayor's discretionary acts happen inside that frame: which charter
to grant, whether to admit the plague ship, which work to raise next.

The alternative is an advisory platform, which lets a mayor simply lie. That is
realistic and it needs a recall mechanism, so it is a second system rather than
the first one.

The port runs the election, because it is neutral, always on, and the magnates
based there are exactly its register of voters. Houses cast votes. The winner's
house gains the office.

So the mayor's game logic lives in the house and only the authority comes from
the port.

## The loop that closes it

**The magnates vote. The traders can sail elsewhere.**

A port that taxes hard and bans freely mints more coin and builds more works, and
loses the traffic that made both possible. The magnates who elected that mayor
feel it first, and they elect somebody else.

Nobody designed that. It falls out of who holds which power, which is the sign
the roles are cut in the right places.

## Open

**The franchise.** One magnate one vote, or weighted by works, or by trade
passing through? Weighted by works makes the port's biggest builder its
governor, which is honest about where power came from and unpleasant in the way
that is interesting.

**The term.** Fixed seasons, indefinite until challenged, or removable by the
same electorate that installed him.

**Can a mayor also be a magnate at his own port?** Almost certainly yes, since he
was elected by them and is one of them, and the conflict of interest is the game
rather than a bug in it.

**What happens to a charter when the mayor changes.** A granted monopoly outlives
the granter or it does not, and that changes how much one is worth.

## What died with the Harbour Master

Owning the market, which the port owns now. Building berths and dredging as a
private investment, which becomes a public work if it returns at all.

The tax rate came back, but as something a candidate stands on rather than a dial
its holder turns for his own profit.

The Harbour Master was a rentier whose game was taxing other people's work. The
magnate is a producer and the mayor is a politician, and neither of them collects
rent for existing.
