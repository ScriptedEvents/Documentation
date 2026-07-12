---
icon: crown
---

# Custom roles with CRole

`CRole` is SER's custom-role system. It is separate from EXILED custom roles and UCR: the registration, spawn systems, callbacks, and assignment are all handled through SER methods. It lets you register roles with a display name, choose the base-game role they replace, assign custom equipment, and control how players receive the role.

This tutorial uses the current `CRole.*` methods listed by `serhelp methods`.

## How a custom role is built

A useful custom role normally has two scripts:

1. A registration script, usually triggered by `WaitingForPlayers`.
2. A setup script, triggered when a player spawns with the custom role.

Keeping registration and player setup separate makes the role easier to maintain and prevents the registration code from running once per player.

## Register a role with a chance-based spawn

The following script registers a Janitor role. It replaces `ClassD`, and each Class-D spawn has a 20% chance to become a Janitor.

```ser
!-- OnEvent WaitingForPlayers

*spawnSystem = CRole.CreateChanceSpawnSystem ClassD 20%
CRole.Register janitor "LCZ Janitor" ClassD *spawnSystem
```

`CRole.Register` takes:

- a role ID (`janitor`) used by other CRole methods;
- a display name shown to players;
- the base-game role to replace;
- an optional spawn system.

The role ID has no spaces. If you omit the spawn system with `_`, the role is registered but is not spawned automatically.

## Configure the role after spawning

Use the `OnCRole spawned` flag to give the player role-specific equipment or move them to a role-specific location:

```ser
!-- OnCRole spawned
-- forRoles janitor

TPRoom @evPlayer LczToilets
GiveItem @evPlayer KeycardJanitor
```

The shipped examples use `@evPlayer` for the player and `*evCRole` for the custom-role reference:

```ser
!-- OnCRole spawned

wait 3s
AnimatedBroadcast @evPlayer 10s "Your custom role is:<br><size=60>{*evCRole -> displayName}</size>"
```

`OnCRole` supports two inline events:

- `spawned` runs when a player receives the custom role;
- `removed` runs when the custom role is taken away.

Use `-- forRoles` to limit the script to specific role IDs. Without it, every custom role triggers the script:

```ser
!-- OnCRole removed
-- forRoles seniorGuard janitor

Print "A tracked custom role was removed."
```

## Procedural spawning at round start

For round-start role conversion, use `CRole.CreateProceduralSpawnSystem`:

```ser
!-- OnEvent WaitingForPlayers

# Each Facility Guard has a 70% chance to become a Senior Guard.
# Convert at most one player, and only when at least three guards exist.
*spawnSystem = CRole.CreateProceduralSpawnSystem FacilityGuard 70% 1 3
CRole.Register senior_guard "Senior Guard" FacilityGuard *spawnSystem
```

Its arguments are:

1. the base-game role to replace;
2. the per-player conversion chance;
3. an optional conversion limit;
4. an optional minimum number of eligible players.

This spawn system runs at round start. The chance applies independently to each eligible player until the conversion limit is reached.

## Assign a role manually

After registration, assign the role from a command with `CRole.Set`:

```ser
!-- CustomCommand makeJanitor
-- availableFor Player RemoteAdmin

CRole.Set @sender janitor
```

To remove a player's custom role, omit the role ID with `_`:

```ser
!-- CustomCommand removeCustomRole
-- availableFor Player RemoteAdmin

CRole.Set @sender _
```

You can check whether a role is registered before using it:

```ser
if {CRole.IsRegistered janitor} is false
    Reply "The Janitor role is not registered."
    stop
end
```

## Bracket-based spawning

When the number of custom-role players should depend on the number of eligible players, create brackets:

```ser
!-- OnEvent WaitingForPlayers

*smallGroup = CRole.CreateSpawnBracket 3 5 1
*largeGroup = CRole.CreateSpawnBracket 6 20 2
*spawnSystem = CRole.CreateBracketSpawnSystem ClassD *smallGroup *largeGroup
CRole.Register scout "Scout" ClassD *spawnSystem
```

The first two values of a bracket are its inclusive lower and upper bounds. The third value is the number of players to convert when the bracket applies. Pass one or more bracket references after the base-game role. Brackets must not overlap.

## Callbacks and cleanup

For a callback-based setup instead of a separate `OnCRole` script, `CRole.SetCallbacks` accepts function names. The callback functions must receive `@player` and `*role`:

```ser
func OnScoutSpawned with @player *role
    GiveItem @player Radio
end

CRole.SetCallbacks scout OnScoutSpawned _
```

The second callback argument is called when the custom role is removed. Use `_` when you do not need a callback.

To remove a role definition completely:

```ser
CRole.Unregister scout
```

Do this only when no other script still expects that role to exist.

## Common mistakes

- Register the role from `WaitingForPlayers`, not from a per-player event.
- Use the role ID (`janitor`) in `CRole.Set`, not the display name (`LCZ Janitor`).
- Keep the `*` prefix for spawn-system and role references.
- Use `@all`, `@classDPlayers`, or another player variable for player arguments; current methods do not use `*` as a player wildcard.
- Avoid registering the same ID repeatedly. `CRole.Register` reports an error when the ID is already registered.

## Useful commands and methods

Use these on the server while developing:

```text
serhelp methods
serhelp OnCRole
serhelp CRole.Register
serhelp CRole.CreateChanceSpawnSystem
serhelp CRole.CreateProceduralSpawnSystem
serhelp CRole.CreateBracketSpawnSystem
serhelp CRole.SetCallbacks
```

### What's next?

See `examples/custom roles/` for complete Janitor and Senior Guard implementations.
