---
icon: arrow-right-to-bracket
metaLinks:
  alternates:
    - /broken/spaces/cuMKPytdZ4h8yad4Mib4/pages/BFcciiPMqWqx0m0CHNTA
---

# Returning Methods

Methods aren't just for performing actions-many can also **return values** that you can store in variables. This is one of the most powerful features in SER, allowing you to retrieve data from the game and use it in your scripts.

## Understanding Returning Methods

When you run `serhelp methods`, you'll notice some methods have a `[rets]` marker next to their name. This indicates the method returns a value that can be captured and stored.

For example:

```
> LimitPlayers [rets]           Returns a player variable with amount of players being equal or lower than the limit.
> RandomNum [rets]              Returns a randomly generated number.
> AmountOf [rets]               Returns the amount of players in a given player variable.
> GetRoomByName [rets]          Returns a reference to a room which has the provided name.
```

## The Exception to the Method Rule

Normally, methods must be the first word on a line. However, **returning methods are the exception**-they can appear on the right side of a variable assignment using the `=` operator.

## How to Use Returning Methods

To capture a return value, assign it to a variable with the appropriate prefix:

```
@player = LimitPlayers @classDPlayers 1
$randomNumber = RandomNum 1 100 int
$playerCount = AmountOf @all
*room = GetRoomByName "LczToilets"
```

### Breaking Down the Syntax

Each assignment follows this pattern:

```
$variableName = MethodName argument1 argument2 ...
```

The variable prefix (`$`, `@`, `*`, or `&`) must match the type the method returns:
- `$` for literal values (numbers, text, booleans)
- `@` for player variables
- `*` for references (rooms, doors, items)
- `&` for collections

## Practical Examples

**Get a random player from Class-D:**
```
@randomClassD = LimitPlayers @classDPlayers 1
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
$randomValue = RandomNum 1 100 int
```

**Check if a player has a specific effect:**
```
$hasEffect = HasEffect @sender Ensnared
```

## Chaining Returning Methods

You can use the result of one returning method as an argument to another:

```
# Get a random player from all alive players, then limit to 1
@target = LimitPlayers @alivePlayers 1

# Get the count of all players, then use it in a broadcast
Broadcast @all 5s "There are {AmountOf @all} players online!"
```

## Common Returning Methods

Here are some frequently used returning methods:

**Player Operations:**
- `LimitPlayers` - Select a limited number of players (useful for random selection)
- `AmountOf` - Count players in a variable
- `RemovePlayers` - Get players excluding specific ones
- `FilterPlayers` - Get players matching a condition

**References:**
- `GetRoomByName` - Find a room by its name
- `GetRandomDoor` - Get a random door

**Numbers:**
- `RandomNum` - Generate random numbers
- `Chance` - Get a true/false result based on probability

**Text:**
- `TextLength` - Get the length of text
- `JoinText` - Combine multiple text values

**Data:**
- `GetPlayerData` - Retrieve stored player data
- `GetFromDB` - Retrieve database values

## Verifying Method Return Types

To check what a method returns, use `serhelp MethodName`. The output will show:

```
=== LimitPlayers ===
> Returns a player variable with amount of players being equal or lower than the limit.

This method returns players, which can be saved or used directly.
```

The first line tells you exactly what type is returned, helping you choose the correct variable prefix.

