---
icon: clock
---

# Yielding Keywords

These allow your script to "wait" for a certain amount of time, allowing you to delay certain actions, instead of running everything at once.

{% hint style="info" %}
Yielding keywords only stop the execution of the script in which they are used in.
{% endhint %}

## How to use them?

#### The `wait` keyword

The simplest there is, its only argument is `duration`, meaning for how long should the script wait.

```
# Waits for 5 seconds
wait 5s

# Waits for half a second
wait 0.5s

# Waits for 15 milliseconds
wait 15ms

# Waits for 5 minutes
wait 5m

# Waits for half an hour
wait .5h
```

{% hint style="info" %}
## Comments

Have you noticed lines like this? What are they?

```
# Waits for 5 seconds
```

These are **comments**! If the first character in the line is a pound sign, the entire line will be ignored! This allows us to document what a given script does.
{% endhint %}

#### The `wait_until` keyword

This is a much more advanced keyword, which will wait until a certain condition evaluates to `true`.

```
# Waits until the method {RoundInfo hasEnded} will return true, meaning the end of a round
wait_until {RoundInfo hasEnded} 

# Waits until the method {AmountOf @scpPlayers} will return 0, meaning 0 alive SCPs
wait_until {AmountOf @scpPlayers} is 0
```

#### Other yielding

Yielding can also be achived with yielding **methods** - these usually end with "AndWait" e.g. `Discord.SendMessageAndWait`

### What's next?

Continue with [Loops](loops.md) to repeat instructions while still yielding safely.
