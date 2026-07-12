---
icon: function
---

# Functions

Functions group reusable instructions under a name. They reduce duplicated code and make larger scripts easier to read.

This tutorial covers inline functions created with `func`. The legacy `!-- Function` flag and `RunFunc` are separate, older systems.

## A function without a return value

Define the function before calling it:

```ser
func AnnounceStart
    Broadcast @all 5s "The event has started!"
end

run AnnounceStart
```

A function without a prefix performs actions but does not return a value.

## Function arguments

Use `with` to declare arguments:

```ser
func Welcome with @player $duration
    Broadcast @player $duration "Welcome, {@player -> name}!"
end

run Welcome @all 5s
```

The argument prefix describes the required value type. Pass arguments in the same order as the declaration.

## Return a value

The function name prefix defines its return type:

| Prefix | Return type |
|---|---|
| `$` | Literal value |
| `@` | Player value |
| `*` | Reference |
| `&` | Collection |
| none | No return value |

A literal-returning function:

```ser
func $Add with $a $b
    return $a + $b
end

$sum = run $Add 5 3
Print "Result: {$sum}"
```

A player-returning function:

```ser
func @Humans
    return Except @alivePlayers @scpPlayers
end

@humans = run @Humans
Broadcast @humans 5s "You are human."
```

The value after `return` must match the prefix of the function name.

## Temporary function variables

Use `ephm` for helper variables that should disappear when the function returns:

```ser
func $HealthPercent with @player
    ephm $health = @player -> health
    ephm $maxHealth = @player -> maxHealth
    return Round (($health / $maxHealth) * 100)
end
```

Player properties require exactly one player. Call this function with a single-player value such as `@sender` or a value returned by `Take ... 1`.

## Returning early

`return` immediately exits a returning function:

```ser
func $SafeName with @player
    if {AmountOf @player} isnt 1
        return "Unknown player"
    end

    return @player -> name
end
```

For a function without a return value, use `stop` only when you intend to stop the entire script. Structure helper functions with conditions when only the function's work should be skipped.

## Inline functions versus function scripts

| Inline function | Legacy function script |
|---|---|
| Defined with `func` | File starts with `!-- Function` |
| Called with `run` | Called with `RunFunc` |
| Lives in the same script | Lives in a separate script file |
| Recommended for new code | Kept for compatibility |

Use inline functions for new code. Use a separate utility script when multiple unrelated scripts must share the same behavior.

## Common mistakes

- Define a function above its first call.
- Include the correct prefix in both the function name and receiving variable.
- Match argument prefixes and order.
- Do not confuse `run FunctionName` with the `RunFunc` method.
- Do not use a property requiring one player with a multi-player value.

### What's next?

Continue with [Error handling](error-handling.md) to recover from runtime failures.
