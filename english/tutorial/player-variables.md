---
icon: user-magnifying-glass
metaLinks:
  alternates:
    - /broken/spaces/cuMKPytdZ4h8yad4Mib4/pages/plchmxYFy559tuFAVltt
---

# Player Variables

The first (out of four) type of variables we will be covering are **player variables**!

These are used to store players, which you can later use to target a certain group of people with a given method.

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

{% hint style="info" %}
## Variable Naming Convention

Each variable type has a **prefix**, and player variables use `@` as their prefix.

The part after the prefix is the **variable name**. A variable name can only use:
- Letters
- Digits
- Underscores

While these are all allowed, SER follows the `camelCase` convention for naming variables.

For example: `@alivePlayers`, `@classDPlayers`, `@scpPlayers`
{% endhint %}

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

# Teleport all SCP players to a location
TPSpawn @scpPlayers
```

## What's Next?

We will cover more advanced concepts about player variables in later tutorials, including:
- Creating custom player variables
- Filtering and combining player variables
- Using player variables with properties
