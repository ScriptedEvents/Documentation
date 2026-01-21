---
icon: command
metaLinks:
  alternates:
    - /broken/spaces/cuMKPytdZ4h8yad4Mib4/pages/z82x1UopunT8VxmQ9tE8
---

# Methods

Methods are like commands. Like commands, these can take certain arguments/parameters and do something with them. These are the building blocks of your scripts.

## What classifies as a method?

For something to be classified as a method by the script, it needs to:

1. Be an existing method (findable in `serhelp methods`)

```
🚫 SendMassiveMessage "Hello, World!"
✅ Reply "Hello, World!"
```

2. Be the first word in the line (exceptions apply, explained later)

```
🚫 test Reply "Hello, World!"
✅ Reply "Hello, World!"
```

3. Be the exact same case-wise

```
🚫 reply "Hello, World!"
🚫 REPLY "Hello, World!"
✅ Reply "Hello, World!"
```

## What methods can I use?

The `serhelp` command will tell you! If you do `serhelp methods`, you will get a list of all methods you have at your disposal.

{% hint style="warning" %}
By the time you're reading this tutorial, the command could've changed a little. I advise you to verify by yourself if the command matches what is shown here.
{% endhint %}

Here's a small part of the output:

```
...

--- Broadcast methods ---
> ClearCountdown                Removes an active countdown for players if one is active.
> Countdown                     Creates a countdown using broadcasts.
> Broadcast                     Sends a broadcast to players.
> ClearBroadcasts               Clears broadcasts for players.
> Hint                          Sends a hint to players.

...
```

## How to get information about a specific method?

You can do `serhelp <methodName>` to get info about a specific method. Let's run the `serhelp Broadcast` command and see what it gives us:

```
=== Broadcast ===
> Sends a broadcast to players.

This method expects the following arguments:
(1) 'players' argument
 - Expected value: Player variable e.g. @players or * for every player

(2) 'duration' argument
 - Expected value: Duration in format #ms (milliseconds), #s (seconds), #m (minutes) etc., e.g. 5s or 2m

(3) 'message' argument
 - Expected value: Any text e.g. "Hello, World!"
```

## How to use that information?

So, let's say we want a broadcast `cool broadcast` to every player for 3 seconds, how to do that?

Well, we have 3 arguments:

1. `players` argument

If we want this argument to mean "all players", we can just use `*`, which represents all players.

```
Broadcast *
```

2. `duration` argument

This argument provides an example of how to use it. We need to provide seconds, so we can use the `#s` format, where we replace `#` with our number, so we can use `3s`.

```
Broadcast * 3s
```

3. `message` argument&#x20;

This will be the text that will be displayed, so we provide `"cool broadcast"`

```
Broadcast * 3s "cool broadcast"
```

{% hint style="danger" %}
## Providing text in SER

When providing text, you MUST put it inside quotes. If not, **each word** will be assumed to be a **different argument**, causing an error.

```
            #1     #2    #3   #4
🚫 Reply example message to print

          - - - - -  #1  - - - - -
✅ Reply "example message to print"
```
{% endhint %}

Using this information we can quickly make a player broadcast! Let's open the `myScript.txt` file in your `SER` folder, and add the following:

```
Reply "Hello, World!"
Broadcast * 3s "cool broadcast"
```

Now if you run this script, you should get a broadcast like this:

<figure><img src="https://github.com/user-attachments/assets/126d0612-4b1d-4d83-b492-78def6ca546b" alt="" width="563"><figcaption></figcaption></figure>

And that's it, you now know how to use methods!
