---
icon: user-magnifying-glass
metaLinks:
  alternates:
    - /broken/spaces/cuMKPytdZ4h8yad4Mib4/pages/plchmxYFy559tuFAVltt
---

# Player variables

The first (out of four) type of variables we will be covering are **player variables**!

These are used to store players, which you can later use to target a certain group of people with a given method.

## Predefined player variables

SER provides you with some predefined player variables! You will be using them a lot, so it's important to start with them first.

Using the `serhelp variables` command, you can find a list of predefined player variables. Here is a small part of the return message (as of `28.10.2025`):

```
Hi! There are 44 variables available for your use!

--- Other variables ---
> @all
> @alivePlayers
> @npcPlayers
> @empty

--- Role variables ---
> @scp173Players
> @classDPlayers
> @spectatorPlayers
> @scp106Players
...
```

{% hint style="info" %}
## Notice how these variables are named

Each variable type has a **prefix**, and player variables use `@` as their prefix.&#x20;

The part after the prefix is the **variable name**. A variable name can only use:

* letters
* digits&#x20;
* underscores&#x20;

While these are all allowed, SER follows the `camelCase` convention for naming variables.

![a camel with camelCase written on it](<../.gitbook/assets/image (3).png>)
{% endhint %}

These variable names clearly describe the players they represent. It shouldn't surprise anyone that a `@alivePlayers` variable stores alive players, and the `@classDPlayers` represents players which have the ClassD role.

We will cover more advanced concepts about player variables in later tutorials.
