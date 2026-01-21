---
icon: user-pen
metaLinks:
  alternates:
    - /broken/spaces/cuMKPytdZ4h8yad4Mib4/pages/SYPENGhvwwAGf2YqEEjK
---

# Advanced player variables

At some point the predefined player variables will not be enough to achieve what you want. Fortunately, you can do much more!

## Creating your own player variable

There are 3 ways of creating player variables, each more powerful than the last.

### Creating an empty variable

```
# creates an empty player variable named @myPlayerVariable
@myPlayerVariable = ()
```

If you ever need to make an empty variable, here is a way to do that.

### Copying an existing variable

```
# creates a copy of the @scpPlayers variable
@myVar = @scpPlayers
```

You have now created a variable that has the exact same players as the `@scpPlayers` has in that moment!

#### Example usage

Take this script for example:

<pre><code># we want to kill all SCPs and make them CI
Kill @scpPlayers
<strong>SetRole @scpPlayers ChaosConscript
</strong></code></pre>

You should already be sus of this script. We can't set `@scpPlayers` to be Chaos Conscripts if all SCPs are dead!

Let's try using `@spectatorPlayers` instead:

<pre><code># we want to kill all SCPs and make them CI
Kill @scpPlayers
<strong>SetRole @spectatorPlayers ChaosConscript
</strong></code></pre>

It will now work, but other spectators - that weren't SCPs - will also be changed into CI. That is a bit of a pickle, but it can be resolved **by making a copy of `@scpPlayers`!**

<pre><code># here we create a copy of @scpPlayers and use that
<strong>@scpsToDie = @scpPlayers
</strong>Kill @scpsToDie
SetRole @scpsToDie ChaosConscript
</code></pre>

Why is this the correct solution to the problem?&#x20;

{% hint style="info" %}
## Custom variables don't update automatically!

This means that it doesn't matter that the `@scpPlayers` value has changed, because `@scpsToDie` variable's value **does not update** with it.&#x20;

In other words, the value of `@scpsToDie` only makes a "snapshot" of all players inside the `@scpPlayers` variable, and does not care if that value has changed later.   &#x20;
{% endhint %}
