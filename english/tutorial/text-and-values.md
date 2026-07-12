---
icon: font
---

# Text, values, and expressions

SER scripts pass values to methods. A value can be text, a number, a duration, a boolean, a color, an enum, a player value, a reference, or a collection.

Understanding how values are written prevents most beginner syntax errors.

## Text

Put text containing spaces in double quotes:

```ser
Reply "Hello, World!"
Broadcast @all 5s "The round has started."
```

Without quotes, every word is parsed as a separate argument.

Use `<br>` for a new line in broadcasts and hints:

```ser
Broadcast @all 5s "First line<br>Second line"
```

Broadcasts and hints also support TextMeshPro rich-text tags:

```ser
Hint @all 4s "<b><color=yellow>Warning!</color></b>"
```

## Insert values into text

Use braces to evaluate an expression inside text:

```ser
$online = AmountOf @all
Broadcast @all 5s "There are {$online} players online."
```

Properties and returning methods can be evaluated directly:

```ser
Reply "Your name is {@sender -> name}."
Reply "Players online: {AmountOf @all}."
```

Use `~` before a brace when it should be printed literally:

```ser
Print "This prints the expression without evaluating it: ~{$value}"
```

## Numbers and mathematics

SER supports `+`, `-`, `*`, `/`, and `%` in expressions:

```ser
$damage = 20
$doubleDamage = $damage * 2
$remaining = 100 - $doubleDamage
Print "Remaining health: {$remaining}"
```

Parentheses make the order explicit:

```ser
$healAmount = Round ((100 + 50) * 0.25)
```

A percentage literal is divided by 100, so `25%` represents `0.25`:

```ser
$quarter = 25%
```

For random numbers, `Random` returns integers by default. Add `real` for decimal results:

```ser
$dice = Random 1 6
$scale = Random 0.5 1.5 real
```

## Durations

Write known durations with a suffix:

| Value | Meaning |
|---|---|
| `250ms` | 250 milliseconds |
| `5s` | 5 seconds |
| `2m` | 2 minutes |
| `1h` | 1 hour |

When the number is calculated at runtime, use `ToDuration`:

```ser
$seconds = Random 10 30
$delay = ToDuration $seconds seconds
wait $delay
```

## Booleans

Boolean values are `true` and `false`:

```ser
$enabled = true

if $enabled is true
    Print "The feature is enabled."
end
```

SER does not use `!` or `not`. Compare with `false` or use `isnt`.

## Enums

Enums are predefined sets of choices such as roles, items, teams, and rooms.

Pass enum values directly to methods:

```ser
SetRole @sender ClassD
GiveItem @sender Medkit
TPRoom @sender LczToilets
```

Properties expose enums as text, so compare them with quoted values:

```ser
if {@sender -> role} is "ClassD"
    Reply "You are Class-D."
end
```

Use `serhelp enums` to list enum types and `serhelp RoleTypeId` to inspect one.

## Colors

Colors can be passed as hexadecimal values where a method expects a color:

```ser
SetLightColor LczToilets #ff0000
```

Inside text, use a rich-text color tag:

```ser
Broadcast @all 5s "<color=#ff0000>Red alert!</color>"
```

## Comments

A comment begins with `# ` and is ignored by the script:

```ser
# Explain why the next instruction is needed.
SetRoundLock true
```

Comments should explain intent or a non-obvious decision, rather than repeat the code.

## Quick reference

| Need | Syntax |
|---|---|
| Text | `"Hello"` |
| Interpolation | `"Hello {$name}"` |
| Property in text | `"{@sender -> role}"` |
| Duration | `5s` |
| Runtime duration | `ToDuration $amount seconds` |
| Boolean | `true`, `false` |
| Percentage | `25%` |
| Comment | `# Explanation` |

### What's next?

Continue with [Variables](variables.md) to store and reuse these values.
