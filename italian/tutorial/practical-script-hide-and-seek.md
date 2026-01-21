---
description: Finally making an event using Scripted Events Reloaded!
icon: scroll
metaLinks:
  alternates:
    - /broken/spaces/cuMKPytdZ4h8yad4Mib4/pages/1rjUQQnG1h0M17sJcRaV
---

# Practical script - Hide & Seek

## Aim of the script

When the script is ran, we want the following to happen:

1. Lock the round
2. Start the round
3. Turn off decontamination in LCZ
4. Lock checkpoints so people can't leave
5. Clear items generated so hiders don't try to abuse anything
6. Get a random person to be a SCP-939 seeker
7. Change every other person into a ClassD hider
8. Have the seeker wait for 1 minute for hiders
9. Once that minute passes, release him in LCZ

## Execution

### Setting up the round

First 5 points are done using very basic methods:

```
# lock the round so the admin can end it whenever he wants to
RoundLock true

# start the round 
# it's assumed that an admin will run this command before the round starts
StartRound

# turn off decontamination so people don't die 
Decontamination disable

# lock LCZ checkpoints so people don't try to escape
LockDoor LczCheckpointA 
LockDoor LczCheckpointB

# remove items from the map
CleanupPickups
```

You may be confused about the `LockDoor`'s arguments. We use `LczCheckpointA` and `LczCheckpointB`, but where did they come from? Let's see its documentation (as of `29.10.2025`):

```
=== LockDoor ===
> Locks doors.

This method expects the following arguments:
(1) 'doors' argument
 - Expected value: DoorName enum, FacilityZone enum, RoomName enum, reference to Door, reference to Room or * for every door

(2) optional 'lock' argument
 - Expected value: DoorLockReason enum value.
 - Default value: AdminCommand
```

The `Expected value` of the `doors` argument may be a little long, but we are interested in the `DoorName` enum.&#x20;

{% hint style="warning" %}
## About enums

Imagine enums as a set of options. In this case `DoorName` enum has a set of door names used in the map.&#x20;

The `serhelp` command provides you with more information about the used enums. Use `serhelp enums` to learn more, or use `serhelp EnumName` to learn about a given enum.&#x20;

In this case, you can use `serhelp DoorName` to access all door names.
{% endhint %}

### Defining the seeker

In order to have 1 random player be the seeker, we can use the `LimitPlayers` method like so:

```
# select a 1 random player and make him a seeker
@seeker = LimitPlayers * 1
SetRole @seeker Scp939
```

This method simply limits the amount of returned players with its last argument, because `*` means "every player."

### Defining the hiders

In order to have the rest be hiders, we can use the `RemovePlayers` method. Here is its documentation (as of `28.10.2025`):

```
=== RemovePlayers ===
> Returns players from the original variable that were not present in other variables.

This method returns players, which can be saved or used directly.

This method expects the following arguments:
(1) 'original players' argument
 - Expected value: Player variable e.g. @players or * for every player

(2) 'players to remove' argument
 - Expected value: Player variable e.g. @players or * for every player
 - This argument consumes all remaining values; this means that every value provided AFTER this one will ALSO count towards this argument's values.
```

This method may look intimidating, but it's a kind of "subtraction" that's performed on player values.

```
# select every player APART FROM the seeker
@hiders = RemovePlayers * @seeker
SetRole @hiders ClassD
```

Here we do an operation like `all players - seeker player`, which in turn leaves us with players that are not seekers.

### Finishing touches

Lastly, we need to add a countdown and teleport the seeker to LCZ.

```
# create a countdown until the release of the seeker
Countdown * 1m "<b>The seeker will be released in:<br><color=red>%seconds%"
Wait 1m

# by releasing we just mean teleporting him to LCZ
TPRoom @seeker LczClassDSpawn
```

## Final result

```
# lock the round so the admin can end it whenever he wants to
RoundLock true

# start the round 
# it's assumed that an admin will run this command before the round starts
StartRound

# turn off decontamination so people don't die 
Decontamination disable

# lock LCZ checkpoints so people don't try to escape
LockDoor LczCheckpointA 
LockDoor LczCheckpointB

# remove items from the map
CleanupPickups

# select a 1 random player and make him a seeker
@seeker = LimitPlayers * 1
SetRole @seeker Scp939

# select every player APART FROM the seeker
@hiders = RemovePlayers * @seeker
SetRole @hiders ClassD

# create a countdown until the release of the seeker
Countdown * 1m "<b>The seeker will be released in:<br><color=red>%seconds%"
Wait 1m

# by releasing we just mean teleporting him to LCZ
TPRoom @seeker LczClassDSpawn
```

Now you have a very simple way to run a hide and seek event!
