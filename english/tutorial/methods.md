---
icon: command
metaLinks:
  alternates:
    - /broken/spaces/cuMKPytdZ4h8yad4Mib4/pages/z82x1UopunT8VxmQ9tE8
---

# Methods

Methods are commands that perform actions. Like all commands, they take certain arguments (parameters) and do something with them. Methods are the fundamental building blocks of your SER scripts.

## What Qualifies as a Method?

For something to be recognized as a method by the script engine, it must:

1. **Be an existing method** (findable in `serhelp methods`)

```
🚫 SendMassiveMessage "Hello, World!"
✅ Reply "Hello, World!"
```

2. **Be the first word in the line** (with rare exceptions)

```
🚫 test Reply "Hello, World!"
✅ Reply "Hello, World!"
```

3. **Match the exact case** (PascalCase)

```
🚫 reply "Hello, World!"
🚫 REPLY "Hello, World!"
✅ Reply "Hello, World!"
```

## Discovering Available Methods

Use the `serhelp` command to explore methods! Run `serhelp methods` to see all available methods organized by category.

There are currently **> 200 methods** available, organized into categories like:
- Audio methods
- Broadcast methods
- Door methods
- Health methods
- Item methods
- Player methods
- Teleport methods
- And many more!

## Getting Information About a Specific Method

Use `serhelp <methodName>` to get detailed information about any method. For example, `serhelp Broadcast`:

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

## Using Method Information

Let's say you want to send a broadcast saying `"cool broadcast"` to every player for 3 seconds. Here's how to break it down:

**Argument 1: players**
- We want all players, so we use `*`

```
Broadcast *
```

**Argument 2: duration**
- We want 3 seconds, so we use `3s`

```
Broadcast * 3s
```

**Argument 3: message**
- We provide our text in quotes: `"cool broadcast"`

```
Broadcast * 3s "cool broadcast"
```

## Important: Text Must Be Quoted

When providing text as an argument, you **MUST** enclose it in double quotes. Without quotes, each word is treated as a separate argument, causing an error.

```
            #1     #2    #3   #4
🚫 Reply example message to print

          - - - - -  #1  - - - - -
✅ Reply "example message to print"
```

## Putting It All Together

Open your script file and add the following:

```
Reply "Hello, World!"
Broadcast * 3s "cool broadcast"
```

When you run this script, you'll see:
- A reply message saying "Hello, World!"
- A broadcast to all players displaying "cool broadcast" for 3 seconds

And that's it! You now know how to use methods in SER!
