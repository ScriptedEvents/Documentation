---
description: Predefined player variables come in handy!
icon: scroll
metaLinks:
  alternates:
    - /broken/spaces/cuMKPytdZ4h8yad4Mib4/pages/5NQyRRYLUAEEnhnV9zzN
---

# Practical Script - Discourage Surface Camping

## Aim of the Script

Create a script that damages all players currently camping on the surface and broadcasts a message telling them to stop.

## Execution

This script requires only 3 components:

* `Broadcast` method - to send a message to players
* `Damage` method - to damage players
* **Predefined player variables** - to target only surface players

The last point is solved using **predefined player variables**. You can find the complete list using `serhelp variables`. Here are the facility zone variables:

```
--- Facility zone variables ---
> @lightContainmentPlayers
> @heavyContainmentPlayers
> @entrancePlayers
> @surfacePlayers
> @otherPlayers
```

The `@surfacePlayers` variable contains all players currently on the surface!

With that in mind, here's the basic structure:

```
# Damage each player on the surface zone (20 health)
# Send a broadcast telling them to stop camping
# Assumes an admin is running this command
```

### Damaging Players

The `Damage` method takes three arguments:

1. **players** - A player variable (e.g., `@surfacePlayers` or `*` for all players)
2. **amount** - A number representing damage (must be at least 0)
3. **reason** (optional) - Text explaining why they were damaged

Since we only want to damage surface campers, we use `@surfacePlayers` instead of `*`:

```
Damage @surfacePlayers 20 "Don't camp on the surface zone!"
```

### Sending a Broadcast

Add a broadcast to inform the players:

```
Broadcast @surfacePlayers 8s "<b><color=red>Stop camping on the surface zone!</color></b>"
```

## Final Result

```
# Damage each player on the surface zone (20 health)
# Send a broadcast telling them to stop camping
# Assumes an admin is running this command

Damage @surfacePlayers 20 "Don't camp on the surface zone!"
Broadcast @surfacePlayers 8s "<b><color=red>Stop camping on the surface zone!</color></b>"
```

This simple script automatically discourages surface camping by damaging offenders and notifying them.
