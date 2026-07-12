---
icon: rotate
---

# Loops

Loops let you run the same block of code multiple times. Whether you need to repeat something a fixed number of times, iterate over every player, or run forever, SER has a loop for the job.

---

## `repeat` — Fixed Iterations

Use `repeat` when you know exactly how many times something should run.

```ser
repeat 5
    Broadcast @all 2s "This message appears 5 times!"
    wait 3s
end
```

### The `with` keyword

You can name the current iteration number using `with`:

```ser
repeat 3 with $iter
    Broadcast @all 3s "Iteration number: {$iter}"
    wait 3s
end
```

`$iter` will be `1`, then `2`, then `3`.

### Using a variable

SER is very flexible - instead of hardcoding the iteration count, you can use a variable:

```ser
repeat $count with $iter
    Print "iteration {$iter}/{$count}"
end
```

---

## `while` — Condition-Based

Use `while` when you want to loop as long as a condition is true.

```ser
while {RoundInfo hasEnded} is false
    wait 10s
    Broadcast @all 3s "The game is still on"
end
```

{% hint style="warning" %}
Make sure your `while` loop eventually becomes false! If the condition never changes, the loop will run forever and may freeze your script.
{% endhint %}

---

## `over` — Iterate Over Collections

Use `over` to loop through every item in a player variable or collection.

```ser
over @all with @plr
    $name = @plr -> name
    Print "Player: {$name}"
end
```

This runs once for every player in `@all`, with `@plr` being the current player each time.

---

## `forever` — Infinite Loop

Use `forever` when you want something to run... well, forever. This is perfect for background events that should last the entire round.

```ser
forever
    wait 30s
    Broadcast @all 5s "This broadcasts every 30 seconds!"
end
```

{% hint style="danger" %}
**Every `forever` loop MUST contain a `wait` or `wait_until`.**

Without a yielding keyword, the loop would run as fast as possible and **freeze the server**.
{% endhint %}

---

## Loop Control

Sometimes you need to exit a loop early or skip an iteration.

### `break` — Exit the loop

```ser
over @all with @plr
    if {@plr -> role} is "Scp173"
        Broadcast @plr 5s "Found SCP-173!"
        break
    end
end
```

### `continue` — Skip to next iteration

```ser
over @scpPlayers with @scp
    if {@scp -> health} >= 500
        continue
    end
    
    # This only runs for SCPs that have less than 500 HP
    Heal @scp 10
end
```

## Practical Example — Give Every Player a Random Effect

Loop through every alive player and have a random chance to explode:

```ser
over @alivePlayers with @plr
    # each player has a 20% chance to explode
    chance 20%
        Explode @plr
    end
end
```

---

## Quick Reference

| Loop Type | Use When | Syntax |
|-----------|----------|--------|
| `repeat` | Fixed number of times | `repeat 5 with $i` |
| `while` | Condition is true | `while $count > 0` |
| `over` | Every item in a group | `over @all with @plr` |
| `forever` | Infinite (with `wait`!) | `forever with $i` |
| `break` | Exit loop early | `break` |
| `continue` | Skip to next iteration | `continue` |

---

## What's Next?

Loops can also iterate over generic lists of values. Those are represented by collections.

### [Collections](collections.md)
