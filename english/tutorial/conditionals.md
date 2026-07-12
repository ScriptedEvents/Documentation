---
icon: code-branch
---

# Conditionals

Not every player should be treated the same! **Conditionals** let your script make decisions — running different code depending on whether something is true or false.

---

## A Practical Example

Imagine you want to send a different welcome message based on a player's role. Without conditionals, you'd have to send the same message to everyone.

---

## The `if` Statement

The simplest conditional checks one thing. If it's true, the code inside runs.

```ser
!-- CustomCommand myrole
-- availableFor player

if {@sender -> role} is "ClassD"
    Broadcast @sender 5s "You are a Class-D personnel!"
end
```

Every `if` must end with `end`. The code between them only runs when the condition is true.

---

## Comparison Operators

You can compare values using these operators:

| Operator | Meaning | Example |
|----------|---------|---------|
| `is` | Equal to | `if $health is 100` |
| `isnt` | Not equal to | `if $health isnt 0` |
| `>` | Greater than | `if $count > 5` |
| `<` | Less than | `if $count < 10` |
| `and` | Both must be true | `if $a is 1 and $b is 2` |
| `or` | At least one is true | `if $a is 1 or $b is 2` |

```ser
if {@sender -> health} > 50
    Hint @sender 3s "You're in good shape!"
end
```

{% hint style="danger" %}
`!` and `not` are **illegal** in SER. Use `isnt` instead.

🚫 `if not $alive`  
✅ `if $alive is false`
{% endhint %}

---

## `elif` and `else`

When you need to check multiple things, use `elif` (else if). If nothing matches, `else` runs as a fallback.

```ser
if {@sender -> role} is "ClassD"
    Broadcast @sender 5s "Escape while you can!"
elif {@sender -> role} is "Scientist"
    Broadcast @sender 5s "Find a keycard and get out!"
else
    Broadcast @sender 5s "Good luck out there!"
end
```

The script checks from top to bottom and stops at the first match.

---

## Combining Conditions

Use `and` and `or` to check multiple things at once.

```ser
# Both must be true
if {@sender -> role} is "ClassD" and {@sender -> health} < 25
    Broadcast @sender 5s "You're badly hurt, Class-D!"
end

# At least one must be true
if {@sender -> team} is "SCPs" or {@sender -> team} is "ChaosInsurgency"
    Broadcast @sender 5s "You're on the hostile team!"
end
```

{% hint style="info" %}
When a condition uses properties (`->`), wrap it in brackets:

✅ `if {@sender -> role} is "ClassD"`  
🚫 `if @sender -> role is "ClassD"`
{% endhint %}

---

## Random Chance

The `chance` statements executes based on its probability. Great for random events.

```ser
chance 25%
    Broadcast @all 5s "A rare event has occurred!"
end
```

If you need a more advanced chance system, use `Chance` method instead:

```ser
if {Chance 50%} and {@sender -> team} is "SCPs"
    Heal @sender 10
end
```

---

## Quick Reference

| What you want | How to do it |
|---------------|--------------|
| Check if equal | `if $var is "value"` |
| Check if not equal | `if $var isnt "value"` |
| Check greater/less | `if $var > 10` |
| Multiple conditions (all) | `if {cond1} and {cond2}` |
| Multiple conditions (any) | `if {cond1} or {cond2}` |
| Random chance | `chance 50%` |
| Fallback case | `else` at the end |

---

## What's Next?

Conditionals let you make decisions. Before repeating code, learn how to pause an event safely with [Yielding](yielding-keywords.md).

### [Yielding](yielding-keywords.md)
