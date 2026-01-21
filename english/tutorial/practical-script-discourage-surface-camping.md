---
description: Predefined player variables come in handy!
icon: scroll
metaLinks:
  alternates:
    - /broken/spaces/cuMKPytdZ4h8yad4Mib4/pages/5NQyRRYLUAEEnhnV9zzN
---

# Practical script - Discourage Surface camping

## Aim of the script

Let's create a script that damages all players currently camping on surface, and will broadcast a message to them to stop camping.

## Execution

It's very simple! We only need 3 things:

* `Broadcast` method
* `Damage` method
* A way to specify that we only want to affect **players on the surface**

The last point can be easily solved using **predefined player variables**! If you take a closer look at the `serhelp variables` command output, you will find what we need (as of `28.10.2025`):

<pre><code>--- Facility zone variables ---
> @lightContainmentPlayers
> @heavyContainmentPlayers
> @entrancePlayers
<strong>> @surfacePlayers
</strong>> @otherPlayers
</code></pre>

The `@surfacePlayers` has players which are on the surface!&#x20;

With that out of the way, we can make a script and add some comments outlining what we want to achieve:

```
# we want to damage each player on the surface zone (e.g. 20 health)
# and send a broadcast telling these players to stop camping 
# it's assumed that an admin will be running this command
```

### Damaging players

We can begin with the `Damage` method. Here is its documentation (as of `27.10.2025`):

```
=== Damage ===
> Damages players.

This method expects the following arguments:
(1) 'players' argument
 - Expected value: Player variable e.g. @players or * for every player

(2) 'amount' argument
 - Expected value: A number which is at least 0 e.g. 2
 
(3) optional 'reason' argument
 - Expected value: Any text e.g. "Hello, World!"
 - Default value:
```

Because we do not want to damage every single player on the server, we cannot use the `*` character. That's why we will be using the `@surfacePlayers` variable!

```
Damage @surfacePlayers 20 "Don't camp on the surface zone!"
```

### Sending a broadcast

As we have already covered how broadcasts work, we can just add it without more explanation:

{% code overflow="wrap" %}
```
Broadcast @surfacePlayers 8s "<b><color=red>Stop camping on the surface zone!</color></b>"
```
{% endcode %}

## Final result

{% code overflow="wrap" %}
```
# we want to damage each player on the surface zone (e.g. 20 health)
# and send a broadcast telling these players to stop camping 
# it's assumed that an admin will be running this command

Damage @surfacePlayers 20 "Don't camp on the surface zone!"
Broadcast @surfacePlayers 8s "<b><color=red>Stop camping on the surface zone!</color></b>"
```
{% endcode %}

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

This simple script automatically discourages surface camping.
