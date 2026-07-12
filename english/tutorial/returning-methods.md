---
icon: arrow-right-to-bracket
metaLinks:
  alternates:
    - /broken/spaces/cuMKPytdZ4h8yad4Mib4/pages/BFcciiPMqWqx0m0CHNTA
---

# Returning Methods

Methods aren't just for performing actions - many can also **return values** that you can store in variables. This is one of the most powerful features in SER, allowing you to retrieve data from the game and use it in your scripts.

## Understanding Returning Methods

When you run `serhelp methods`, you'll notice some methods have a `[rets]` marker next to their name. This indicates the method returns a value that can be captured and stored.

For example:

```
> Take [rets]          ~ Takes a specified amount of players from a player variable, lower or equal to the limit.
> Random [rets]        ~ Returns a randomly generated number.
> AmountOf [rets]      ~ Returns the amount of players in a given player variable.
> GetRoomByName [rets] ~ Returns a reference to a room which has the provided name.
```

## The Exception to the Method Rule

Normally, methods must be the first word on a line. However, **returning methods are the exception** - they can appear on the right side of a variable assignment using the `=` operator.

## How to Use Returning Methods

To capture a return value, assign it to a variable with the appropriate prefix:

```
@player = Take @classDPlayers 1
$randomNumber = Random 1 100
$playerCount = AmountOf @all
*room = GetRoomByName "LczToilets"
```

### Breaking Down the Syntax

Each assignment follows this pattern:

```
~variableName = MethodName argument1 argument2 ...
```

The variable prefix must match the type the method returns. See the [Variables](variables.md) tutorial if you need a refresher on prefixes.

## Practical Examples

**Get a random player from Class-D:**
```
@randomClassD = Take @classDPlayers 1
```

**Count all players on the server:**
```
$totalPlayers = AmountOf @all
```

**Get a specific room by name:**
```
*toilets = GetRoomByName "LczToilets"
```

**Generate a random number between 1 and 100:**
```
$randomValue = Random 1 100
```

**Check if a player has a specific effect:**
```
$hasEffect = HasEffect @sender Ensnared
```

## Chaining Returning Methods

You can use the result of one returning method as an argument to another:

```
# Get one random player from all alive players
@target = Take @alivePlayers 1

# Get the count of all players, then use it in a broadcast
Broadcast @all 5s "There are {AmountOf @all} players online!"
```

## Common Returning Methods

Here are some frequently used returning methods:

**Player Operations:**
- `Take` - Select a limited number of players (useful for random selection)
- `AmountOf` - Count players in a variable
- `Except` - Get players excluding specific ones
- `Filter` - Get players whose chosen property matches a value

**References:**
- `GetRoomByName` - Find a room by its name
- `GetRandomDoor` - Get a random door

**Numbers:**
- `Random` - Generate random numbers
- `Chance` - Get a true/false result based on probability

**Text:**
- `Text.Contains` - Get a true/false result if a value is in text
- `Text.Replace` - Replace a value in text

**Data:**
- `GetPlayerData` - Retrieve stored player data
- `DB.Get` - Retrieve database values

## Verifying Method Return Types

To check what a method returns, use `serhelp MethodName`. The output will show:

```
=== Take ===
> Takes a specified amount of players from a player variable, lower or equal to the limit.

This method returns player value.
You can save it to a variable with a '@' prefix.
@myVariable = Take ...

This method expects the following arguments:
 (1) 'players' argument
 - Expected value: Player variable (e.g. @all, @classDPlayers)

 (2) 'limit' argument
 - Expected value: Value must be at least 1 e.g. 3
```

If possible, the method will show you information regarding the return type and how to save it.

### What's next?

Continue with [Properties](properties.md) to inspect data returned by players and game objects.
