---
icon: arrow-right-to-bracket
metaLinks:
  alternates:
    - /broken/spaces/cuMKPytdZ4h8yad4Mib4/pages/BFcciiPMqWqx0m0CHNTA
---

# Returning methods

There is one more way of creating variables, and that's using methods. Some methods can return values, which you can later use to make a new variable!

## How to find a returning method

These can be found when running the `serhelp methods` command. In order to destinguish if a method returns a value or not, there is the `[rets]` marker. Here is a part of the output (as of `28.10.2025`):

```
--- PlayerVariable methods ---
> ContainsPlayer [rets]         Returns a true/false value indicating if the provided player is in the list.
> GetPlayerFromReference [rets] Returns a player variable with a single player from a reference.
> JoinPlayers [rets]            Returns all players that were provided from multiple player variables.
> LimitPlayers [rets]           Returns a player variable with amount of players being equal or lower than the limit.
> RemovePlayers [rets]          Returns players from the original variable that were not present in other variables.
```

## How to use a returning method

Do you remember that exception about methods being the first word in a line?

> &#x20;[#what-classifies-as-a-method](methods.md#what-classifies-as-a-method "mention")

Well, this is the exception. Let's say we want to use the `LimitPlayers` method to get one random ClassD player. Let's check it's documentation using `serhelp LimitPlayers` (as of `28.10.2025`):

<pre><code>=== LimitPlayers ===
> Returns a player variable with amount of players being equal or lower than the limit.

<strong>This method returns players, which can be saved or used directly.
</strong>
This method expects the following arguments:
(1) 'players' argument
 - Expected value: Player variable e.g. @players or * for every player

(2) 'limit' argument
 - Expected value: Value must be at least 1 e.g. 421
</code></pre>

In order to save the result to a variable, we need to do this:

```
# creates @player variable with 1 random player from the @classDPlayers variable
@player = LimitPlayers @classDPlayers 1
```

You have now successfully saved the return value of `LimitPlayers` method to a variable!
