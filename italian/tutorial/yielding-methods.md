---
icon: clock
metaLinks:
  alternates:
    - /broken/spaces/cuMKPytdZ4h8yad4Mib4/pages/IASvs8rIJ713hM0m2ePw
---

# Yielding Methods

These allow your script to "wait" for a certain amount of time, allowing you to delay certain actions, instead of running everything at once.

{% hint style="info" %}
Yielding methods only stop the execution of the script in which they are used in.
{% endhint %}

## How to find them?

Very simple! The `serhelp methods` command has a category called `Yielding`, where you can find yielding methods.

{% hint style="info" %}
There are some methods that are yielding, but are **not in the category** e.g. the `RunScriptAndWait` method.
{% endhint %}

## How to use them?

#### The `Wait` method

The simplest there is, its only argument is `duration`, meaning for how long should the script wait.

```
# Waits for 5 seconds
Wait 5s

# Waits for half a second
Wait 0.5s

# Waits for 15 milliseconds
Wait 15ms

# Waits for 5 minutes
Wait 5m

# Waits for half an hour
Wait .5h
```

{% hint style="info" %}
## Comments

Have you noticed lines like this? What are they?

```
# Waits for 5 seconds
```

These are **comments**! If the first character in the line is a pound sign, the entire line will be ignored! This allows us to document what a given script does.
{% endhint %}

#### The `WaitUntil` method

This is a much more advanced method, which will wait until a certain condition evaluates to `true`.

```
# Waits until the method {RoundInfo hasEnded} will return true, meaning the end of a round
WaitUntil ({RoundInfo hasEnded} == true)

# Waits until the method {AmountOf @scpPlayers} will return 0, meaning 0 alive SCPs
WaitUntil ({AmountOf @scpPlayers} == 0)
```

{% hint style="info" %}
`WaitUntil` method uses conditions and value returning methods, which will be covered later down the tutorial series. These examples simply demonstrate what's possible.
{% endhint %}
