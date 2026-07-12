---
icon: user-magnifying-glass
metaLinks:
  alternates:
    - /broken/spaces/cuMKPytdZ4h8yad4Mib4/pages/plchmxYFy559tuFAVltt
---

# Player Variables

The first (out of four) type of variables we will be covering are **player variables**!

These are used to store players, which you can later use to target a certain group of people with a given method.

If you haven't read the [Variables](variables.md) tutorial yet, start there — it covers how prefixes and naming work.

## Predefined Player Variables

SER provides you with several predefined player variables! You will be using them frequently, so it's important to start with them first.

Using the `serhelp variables` command, you can find a list of predefined player variables. Here is a summary of the available categories (as of the latest version):

```
Hi! There are 47 variables available for your use!

--- Other variables ---
> @all
> @allPlayers
> @alivePlayers
> @npcPlayers
> @empty
> @emptyPlayers

--- Role variables ---
> @scp173Players
> @classDPlayers
> @spectatorPlayers
> @scp106Players
> @scientistPlayers
> @scp079Players
...

--- Facility zone variables ---
> @lightContainmentPlayers
> @heavyContainmentPlayers
> @entrancePlayers
> @surfacePlayers
> @otherPlayers

--- Team variables ---
> @scpPlayers
> @foundationForcePlayers
> @chaosInsurgencyPlayers
> @deadPlayers
```

## Understanding Predefined Variables

These variable names clearly describe the players they represent:

- `@alivePlayers` - All players who are currently alive
- `@classDPlayers` - Players with the ClassD role
- `@scpPlayers` - All players on the SCP team
- `@spectatorPlayers` - Players in spectator mode
- `@lightContainmentPlayers` - Players currently in Light Containment Zone
- `@all` - Every player on the server (alive or dead)
- `@empty` - An empty player variable (contains no players)

## Using Predefined Variables

You can use these variables directly in methods. For example:

```
# Give all alive players a keycard
GiveItem @alivePlayers KeycardO5

# Broadcast to all ClassD players
Broadcast @classDPlayers 5s "Attention ClassD personnel!"

# Teleport all SCP players to SCP-173 spawn location
TPSpawn @scpPlayers Scp173
```

## What's Next?

The next step is learning how to read information from one player with [Properties](properties.md).
